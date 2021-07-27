Fecmall GA扩展插件 - 二次开发
===============

> 基于GA，进行二次开发



### GA扩展插件文件说明

1.GA扩展插件,@fecga对应的文件路径：`./addons/fecmall/fecga/` ，

2.`@fecga/config.php`，可以看到`event` services配置

GA追踪代码的添加，是通过fecmall `event`机制完成的，关于Fecmall Event具体参看：[Fecmall Event 事件](https://www.fecmall.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_event.html)

3.具体event文件：@fecga\event\Fecga.php

`ga event`都是在该文件中实现的，当fecmall触发event，就会执行这里的代码，进而将ga对接的部分执行。



### 对接流程分析，以分类页面发送产品数据为例子

以fecmall开源系统，pc入口（appfront）为例子


1.打开文件：@fecshop/app/appfront/theme/base/front/catalog/category/index.php

页面底部可以看到如下代码：

```
<?= Yii::$service->page->trace->getTraceCategoryJsCode($this, $categoryM, $products)  ?>
```

下面我们打开`page trace service`

2.打开文件：@fecshop/services/page/Trace.php，找到这个函数

```
public function getTraceCategoryJsCode($view, $categoryM, $products)
    {
        // 加入事件event
        $metaAfterEventName = 'event_after_trace_category_js_code';
        Yii::$service->event->trigger($metaAfterEventName, [
            'view' => $view,
            'categoryM' => $categoryM,
            'products' => $products,
        ]);
        
        $categoryName = Yii::$service->fecshoplang->getDefaultLangAttrVal($categoryM['name'], 'name');
        if ($this->traceJsEnable && $categoryName) {
            
            return "<script type=\"text/javascript\">
    var _maq = _maq || [];
    _maq.push(['category', '".$categoryName."']);
</script>";
        } else {
            
            return '';
        }
    }

```

可以看到，这里触发了一个`event`事件:`event_after_trace_category_js_code`

3.进入已经安装了的GA插件文件目录，打开配置文件：
`./addons/fecmall/fecga/config.php`

可以看到事件event的配置

```
    // category页面，添加ga 电子商务代码，用于发送分类产品数据
    'event_after_trace_category_js_code' => [
        ['fecga\event\Fecga','addTraceCategoryJsCodeConfig'],
    ],
```

这里添加了event，因此会执行类`fecga\event\Fecga`的函数`addTraceCategoryJsCodeConfig()`


4.打开@fecga\event\Fecga (就是文件`./addons/fecmall/fecga/event/Fecga.php`)

找到函数`addTraceCategoryJsCodeConfig()`,内容如下：


```
/**
     * @param $data | array
     * category页面，添加ga 电子商务代码，用于发送分类数据
     * 包含2部分
     * 1.分类页面，产品列表信息
     * 2.点击的产品数据，用户点击分类页面的某个商品，会将该商品的数据发送给ga
     */
    public static function addTraceCategoryJsCodeConfig($data)
    {
        // GA是否开启
        if (!Yii::$service->ga->isGaEnable()) {
            
            return;
        }
        
        $view = $data['view'];
        $categoryM = $data['categoryM'];
        $products = $data['products'];
        $categoryName = Yii::$service->fecshoplang->getDefaultLangAttrVal($categoryM['name'], 'name');
        $itemArr = [];
        if (is_array($products) || !empty($products)) {
            $i = 0;
            foreach ($products as $product) {
                $i++;
                $productName =  $product['name'];
                $productPrice = Yii::$service->product->price->getFinalPrice($product['price'],$product['special_price'],$product['special_from'],$product['special_to'] );
                $productBrandName = Yii::$service->product->brand->getBrandNameByIdWithAll($product['brand_id']);
                $productSku =  $product['sku'];
                $itemArr[] = [
                    "id" => $productSku,
                    "name" => $productName,
                    "list_name" => "Category Results",
                    "brand" => $productBrandName,
                    "category" => $categoryName,
                    // "variant": "Black",
                    "list_position" => $i,
                    "quantity" => 1,
                    "price" => (string)$productPrice,
                    "url" => $product['url'] ,
                ];
            }
        }
        // google analysis
        $view->registerExternalJs('<script>
    var items = '.json_encode($itemArr).';
    gtag("event", "view_item_list", {
      "items": items
    });
</script>', \yii\web\View::POS_END);
        
        $view->registerExternalJs('
<script>
    var quickBuyItemUrl = "";
    function createFunctionWithTimeout(callback, opt_timeout) {
      var called = false;
      function fn() {
        if (!called) {
          called = true;
          callback();
        }
      }
      setTimeout(fn, opt_timeout || 1000);
      return fn;
    }
    var category_product_click_func = function(e){
        //alert(1);
        e.preventDefault();
        e.stopImmediatePropagation();
        var self = $(this);
        
        var currentUrl = self.attr("href");
        if (!currentUrl) {
            currentUrl = self.attr("rel");
        }
        var currentItem = {};
        for (var x in items) {
            itemOne = items[x];
            if (itemOne.url == currentUrl) {
                currentItem = itemOne;
            }
        }
        console.log(currentItem);
        
        gtag("event", "select_content", { 
            "event_callback": 
                createFunctionWithTimeout(function() {
                    var productUrl = self.attr("href");
                    if (!productUrl) {
                        productUrl = self.attr("rel");
                    }
                    
                    window.location.href = productUrl;
                })
            ,
            "content_type": "product",
            "items": currentItem
        });
    };
    $(document).ready(function(){
        $(document).on("click", ".category_product a", category_product_click_func);
        $(".category_product .span_click").click(category_product_click_func);
        
    });     
</script>', \yii\web\View::POS_END);
        
        
        // google analysis - quick view add to cart
        $view->registerExternalJs('<script>
    var quickBuyAddToCart = function(e){
        e.stopImmediatePropagation();
        
        var currentItem = "";
        for (var x in items) {
            itemOne = items[x];
            if (itemOne.url == quickBuyItemUrl) {
                currentItem = itemOne;
            }
        }
        
        var gaQty = $(".qty").val();
        // show loading icon
        $(this).addClass("dataUp");
        $(this).addClass("position-relative");
        $("#loading141286").addClass("show");
        
        currentItem["quantity"] = gaQty ? gaQty : 1;
        console.log(currentItem);
        // 【ga event: add_to_cart】
        gtag("event", "add_to_cart", { 
            "event_callback": 
                createFunctionWithTimeout(function() {
                    addToCart();
                })
            ,
            "items": [
                currentItem
            ]
        });
    };
$(document).ready(function(){
    // ga: add to cart
    
    $(".product_quick_view").on("click", ".product-info__add-cart-btn-container", quickBuyAddToCart);
    $(".add_to_bag").click(quickBuyAddToCart);
}); 
</script>', \yii\web\View::POS_END);
        
        // function end
    }
```


5.可以看到函数`$view->registerExternalJs()`，将js代码传递进去

对于变量view，就是yii2框架的组件view，也就是  `yii\web\View`, 但是打开文件这个文件
（./vendor/yiisoft/yii2/web/View.php），你会发现没有
registerExternalJs()方法

这是因为fecmall对view组件进行了重写，添加了函数

打开`@fecshop/yii/web/View.php`(@fecshop就是文件路径./vendor/fancyecommerce/fecshop) 可以看到里面重写和添加的函数

```
<?php
/**
 * @link http://www.yiiframework.com/
 * @copyright Copyright (c) 2008 Yii Software LLC
 * @license http://www.yiiframework.com/license/
 */

namespace fecshop\yii\web;

use yii\helpers\Html;

class View extends \yii\web\View
{
    /**
     * 第三方js数组
     */
    public $externalJs;
    
    public function registerExternalJs($jsScriptStr, $position = self::POS_HEAD, $key = null)
    {
        $key = $key ?: md5($jsScriptStr);
        $this->externalJs[$position][$key] = $jsScriptStr;
    }
    
    /**
     * Renders the content to be inserted in the head section.
     * The content is rendered using the registered meta tags, link tags, CSS/JS code blocks and files.
     * @return string the rendered content
     */
    protected function renderHeadHtml()
    {
        $lines = [];
        if (!empty($this->metaTags)) {
            $lines[] = implode("\n", $this->metaTags);
        }

        if (!empty($this->linkTags)) {
            $lines[] = implode("\n", $this->linkTags);
        }
        if (!empty($this->cssFiles)) {
            $lines[] = implode("\n", $this->cssFiles);
        }
        if (!empty($this->css)) {
            $lines[] = implode("\n", $this->css);
        }
        if (!empty($this->externalJs[self::POS_HEAD])) {
            $lines[] = implode("\n", $this->externalJs[self::POS_HEAD]);
        }
        if (!empty($this->jsFiles[self::POS_HEAD])) {
            $lines[] = implode("\n", $this->jsFiles[self::POS_HEAD]);
        }
        if (!empty($this->js[self::POS_HEAD])) {
            $lines[] = Html::script(implode("\n", $this->js[self::POS_HEAD]));
        }
        
        return empty($lines) ? '' : implode("\n", $lines);
    }
    
    /**
     * Renders the content to be inserted at the beginning of the body section.
     * The content is rendered using the registered JS code blocks and files.
     * @return string the rendered content
     */
    protected function renderBodyBeginHtml()
    {
        $lines = [];
        
        if (!empty($this->externalJs[self::POS_BEGIN])) {
            $lines[] = implode("\n", $this->externalJs[self::POS_BEGIN]);
        }
        
        if (!empty($this->jsFiles[self::POS_BEGIN])) {
            $lines[] = implode("\n", $this->jsFiles[self::POS_BEGIN]);
        }
        if (!empty($this->js[self::POS_BEGIN])) {
            $lines[] = Html::script(implode("\n", $this->js[self::POS_BEGIN]));
        }

        return empty($lines) ? '' : implode("\n", $lines);
    }
    
    
    protected function renderBodyEndHtml($ajaxMode)
    {
        $lines = [];
        
        
        if (!empty($this->jsFiles[self::POS_END])) {
            $lines[] = implode("\n", $this->jsFiles[self::POS_END]);
        }
        if (!empty($this->externalJs[self::POS_END])) {
            $lines[] = implode("\n", $this->externalJs[self::POS_END]);
        }

        if ($ajaxMode) {
            $scripts = [];
            if (!empty($this->js[self::POS_END])) {
                $scripts[] = implode("\n", $this->js[self::POS_END]);
            }
            if (!empty($this->js[self::POS_READY])) {
                $scripts[] = implode("\n", $this->js[self::POS_READY]);
            }
            if (!empty($this->js[self::POS_LOAD])) {
                $scripts[] = implode("\n", $this->js[self::POS_LOAD]);
            }
            if (!empty($scripts)) {
                $lines[] = Html::script(implode("\n", $scripts));
            }
        } else {
            if (!empty($this->js[self::POS_END])) {
                $lines[] = Html::script(implode("\n", $this->js[self::POS_END]));
            }
            if (!empty($this->js[self::POS_READY])) {
                $lines[] = Html::script(implode("\n", $this->js[self::POS_READY]));
                
            }
            if (!empty($this->js[self::POS_LOAD])) {
                $lines[] = Html::script(implode("\n", $this->js[self::POS_LOAD]));
                
            }
        }
        
        if (!empty($this->jsFiles['POS_READY'])) {
            $lines[] = implode("\n", $this->jsFiles['POS_READY']);
        }
        
        return empty($lines) ? '' : implode("\n", $lines);
    }
    
    public function registerJs($js, $position = self::POS_READY, $key = null)
    {
        $key = $key ?: md5($js);
        $this->js[$position][$key] = $js;
        //if ($position === self::POS_READY || $position === self::POS_LOAD) {
        //    JqueryAsset::register($this);
        //}
    }
}
```

到这里，流程逻辑分析就完成了，view类通过renderXxxx将这些js发布到相应的位置。


逻辑流程明白了，您就可以通过自己的需求，二次开发GA插件了，添加自己的event。



































