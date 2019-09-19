Fecmall 小部件
==============

> Fecmall 的小部件是集数据库数据与view文件
> 生成的一个区块，譬如网站侧栏的热销产品，做成一个小部件，可以很方便的
> 在其他页面进行引入。当然，Fecmall的head header（头部），footer（尾部）都是小部件实现的。

### 小部件结构：

小部件由两部分组成，动态数据提供部分 和 提供html代码的view部分，共同组合
，显示出来小部件。

### 小部件配置：
`@fecshop/app/appfront/config/appfront.php`里面进行小部件的配置，示例代码：

```
'services' => [
        'page' => [
            'childService' => [
                'theme' => [
                    'viewFileConfig' => [
                        // 'catalog/category/index' => '@fecshop/app/appfront/theme/base/front/catalog/category/index.php',
                    ],
                ],
                'widget' => [
                    'widgetConfig' => [
                        'base' => [
                            'head' => [
                                // 动态数据提供部分
                                'class' => 'fecshop\app\appfront\widgets\Head',
                                // 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
                                'view'  => 'widgets/head.php',
                                // 缓存
                                'cache' => [
                                    'timeout'    => 4500,  // 缓存过期时间
                                ],
                            ],
                            'header' => [
                                'class' => 'fecshop\app\appfront\widgets\Headers',
                                // 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
                                'view'  => 'widgets/header.php',
                                'cache' => [
                                    'timeout'    => 4500,
                                ],
                            ],
                            'topsearch' => [
                                'view'  => 'widgets/topsearch.php',
                            ],
                            'menu' => [
                                'class' => 'fecshop\app\appfront\widgets\Menu',
                                // 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
                                'view'  => 'widgets/menu.php',
                                'cache' => [
                                    //'timeout' 	=> 4500,
                                ],
                            ],
                            'footer' => [
                                'class' => 'fecshop\app\appfront\widgets\Footer',
                                // 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
                                'view'  => 'widgets/footer.php',
                                'cache' => [
                                    //'timeout' 	=> 4500,
                                ],
                            ],
                            'scroll' => [
                                // 'class' => 'fecshop\app\appfront\modules\Cms\block\widgets\Scroll',
                                // 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
                                'view'  => 'widgets/scroll.php',
                            ],
                            'breadcrumbs' => [
                                'view'  => 'widgets/breadcrumbs.php',
                            ],
                            'flashmessage' => [
                                'view'  => 'widgets/flashmessage.php',
                            ],
                            'trace' => [
                                'view'  => 'widgets/trace.php',
                            ],
                            'beforeContent' => [
                                'view'  => 'widgets/beforeContent.php',
                            ],
                        ],
                        'home' => [
                            'product_price' => [
                                'class' 		=> 'fecshop\app\appfront\modules\Catalog\block\category\Price',
                                'view'  		=> 'cms/home/index/price.php',
                            ],
                        ],
                        'customer' => [
                            'left_menu' => [
                                'class' => 'fecshop\app\appfront\modules\Customer\block\LeftMenu',
                                'view'	=> 'customer/leftmenu.php'
                            ],
                        ],
                        'cms' => [
                            'productlist' => [
                                'view'  => 'cms/home/index/product.php',
                            ],
                        ],
                        'category' => [
                            'price' => [
                                'class' 		=> 'fecshop\app\appfront\modules\Catalog\block\category\Price',
                                'view'  		=> 'catalog/category/price.php',
                            ],
                            'toolbar' => [
                                'view'  		=> 'catalog/category/index/toolbar.php',
                            ],
                            'filter_refineby' => [
                                'view'  		=> 'catalog/category/index/filter/refineby.php',
                            ],
                            'filter_subcategory' => [
                               'view'  		=> 'catalog/category/index/filter/subcategory.php',
                            ],
                            'filter_attr' => [
                               'view'  		=> 'catalog/category/index/filter/attr.php',
                            ],
                            'filter_price' => [
                               'view'  		=> 'catalog/category/index/filter/price.php',
                            ],
                            
                        ],
                        'product' => [
                            'price' => [
                               'view'	=> 'catalog/product/index/price.php'
                            ],
                            'options' => [
                                'view'	=> 'catalog/product/index/options.php'
                            ],
                            'tier_price' => [
                                'view'	=> 'catalog/product/index/tier_price.php'
                            ],
                            'image' => [
                                'view'	=> 'catalog/product/index/image.php'
                            ],
                            'buy_also_buy' => [
                                'view'	=> 'catalog/product/index/buy_also_buy.php'
                            ],
                            'review' => [
                                'class'  => 'fecshop\app\appfront\modules\Catalog\block\product\Review',
                                'view'  => 'catalog/product/index/review.php',
                            ],
                            'payment' => [
                                'view'			=> 'catalog/product/index/payment.php',
                            ],
                        ],
                        'search' => [
                            'toolbar' => [
                                'view'  		=> 'catalogsearch/index/index/toolbar.php',
                            ],
                        ],
                        // 下单页面
                        'order' => [
                            'shipping' => [
                                'view'	=> 'checkout/onepage/index/shipping.php'
                            ],
                            'payment' => [
                                'view'	=> 'checkout/onepage/index/payment.php'
                            ],
                            'view' => [
                                'view'	=> 'checkout/onepage/index/review_order.php'
                            ],
                        ],
                        'payment' => [
                            'paypal_express_address' => [
                                'view'	=> 'payment/paypal/express/review/address.php',
                            ],
                            'paypal_express_shipping' => [
                                'view'	=> 'payment/paypal/express/review/shipping.php'
                            ],
                            'paypal_express_orderview' => [
                                'view'	=> 'payment/paypal/express/review/review_order.php'
                            ],
                        ],
                    ],
                ],
            ],
        ],
    
    ],
```

譬如header小部件

```
'header' => [
    'class' => 'fecshop\app\appfront\widgets\Headers',
    // 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
    'view'  => 'widgets/header.php',
    'cache' => [
        'timeout'    => 4500,
    ],
],
```

数据提供部分为:`@fecshop\app\appfront\widgets\Headers.php`,
view部分为：`@fecshop\app\appfront\theme\base\default\widgets\header.php`。


其中，head header都是一个小部件，里面的class是动态数据提供部分，
view是显示部分，cache是缓存，您可以通过该配置将缓存打开，以及设置缓存的超时时间。

小部件的view部分遵循fecshop的多模板机制，可以在二开theme路径下添加
相应文件实现view部分的重写.

### 小部件的使用：

1.

```
Yii::$service->page->widget->render('base/header',$this);
```

上面传的的`$this`，在view文件中对应的变量为：`$parentThis`，举例子可以参看head小部件


```
<?php $parentThis->head() ?>
```

`$parentThis`就是`render()`函数调用传入的`$this`变量。


2.

```
Yii::$service->page->widget->DiRender($configKey, $diConfig = [])
```

$configKey配置中必须含有class部分，也就是动态数据提供部分
$diConfig数组将会被注入到该class，譬如：
https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/theme/base/front/catalog/product/index.php#L134

```
<?php # review部分。
    $reviewParam = [
        'product_id' 	=> $_id,
        'spu'			=> $spu,
    ];
    
    $reviewParam['reviw_rate_star_info'] = $reviw_rate_star_info;
    $reviewParam['review_count'] = $review_count;
    $reviewParam['reviw_rate_star_average'] = $reviw_rate_star_average;
    // var_dump($reviewParam);exit;
?>
<?= Yii::$service->page->widget->DiRender('product/review', $reviewParam); ?>

```

3.

https://github.com/fecshop/yii2_fecshop/blob/6057826ab07517ed7f39874a85ca24a06eff99ef/app/apphtml5/theme/base/html5/catalog/product/index/buy_also_buy.php#L24

```
<?php
    //$parentThis['products'] = $parentThis['products'];
    $parentThis['name'] = 'featured';
    $config = [
        'view'  		=> 'cms/home/index/product.php',
    ];
    echo Yii::$service->page->widget->renderContent('category_product_price',$config,$parentThis);
?>
```

这种情况，可以自定义，不需要再配置文件中提前定义。
















