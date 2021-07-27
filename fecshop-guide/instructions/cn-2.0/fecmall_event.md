Fecmall Event
==============

> Fecmall 事件的介绍，fecmall的事件，没有使用yii2的事件机制，而是自己做了一个比较简单实用的事件机制。

### 事件使用

目前fecmall的事件：

```
return [
    'event' => [
        'class' => 'fecshop\services\Event',
        # 事件配置表，这是Fecshop默认存在的事件。您可以在配置中添加您的事件函数。
        'eventList' => [
            # Fecmall初始化执行的event（发生在yii2框架初始化之前）
            'event_service_application_init' => [],
            # 加入购物车before
            'event_add_to_cart_before' 		=> [],
            # 加入购物车after
            'event_add_to_cart_after' 		=> [],
            # 生成订单before
            'event_generate_order_before' 	=> [],
            # 生成订单after
            'event_generate_order_after' 	=> [],
            # 后台配置，appfront，apphtml5等入口配置，保存支付配置事件，主要用于支付扩展插件，解决冲突问题
            'event_before_save_payment_config' => [],
            # 用于给head加meta信息
            'event_after_head_meta_config' => [],
            # 用于给head加link信息
            'event_after_head_link_config' => [],
            
            #下面是page trace service中触发的event
            
            // page trace service执行的event，在首页中执行
            'event_after_trace_home_js_code' => [],
            // page trace service执行的event，在category分类页面中执行
            'event_after_trace_category_js_code' => [],
            // page trace service执行的event，在search搜索页面中执行
            'event_after_trace_search_js_code' => [],
            // page trace service执行的event，在product产品详情页页面中执行
            'event_after_trace_product_js_code' => [],
            // page trace service执行的event，在checkout下单页面中执行
            'event_after_trace_checkout_js_code' => [],
            // page trace service执行的event，在订单支付成功页面中执行
            'event_after_trace_purchase_js_code' => [],
            
            // 订单生成订单编号之前执行的event，可以通过该event，自己更改订单编号格式的生成
            'event_generate_order_increment_id_before' => [],
        ]
    ],
];
```




### Fecmall事件event的使用


对于日常撸业务代码，事件event很少用到，一般在产品的扩展插件开发用到的会多一些，目的是为了解决多个插件的冲突问题，
以及插件的即插即用。

下面以例子讲解如何使用event，譬如：我们开发了一个扩展插件A，然后想在appfront 入口，每个页面的head里面加上一个meta信息，
譬如：

```
<meta name="p:domain_verify" content="ab1a1e2693892ce62a6a3812445b77d5"/>
```

我们开发插件，是不能直接修改fecmall代码的，因此，我们需要用重写的方式

如果我们采用多模板路径的方式，那么如果有一个`扩展插件B`也要在head里面加入一个meta信息，那么`势必冲突`,
因此，我们采用event来更好的解决这个问题。

我们可以使用`event_after_head_meta_config`事件来解决


1.我们先去看看事件所在的代码文件位置，@fecshop/services/page/Asset.php 大约153行左右

```
$metaAfterEventName = 'event_after_head_meta_config';
Yii::$service->event->trigger($metaAfterEventName, $view);
```

可以看到，将对象`$view`作为参数传递到事件参数中


2.我们建立`插件A`，如何创建fecmall插件，请参看[Fecmall-开发者中心-创建发布升级应用](https://www.fecmall.com/doc/fecshop-guide/addons/cn-2.0/guide-fecmall-addons-developer-center.html)

当然，您也可以在本地添加配置。下面的例子是fecfeed插件作为例子：

```
'services' => [
    'event' => [
        'eventList' => [
            'event_after_head_meta_config' => [
                ['fecfeed\event\Fecfeed','addHeadMetaConfig'],
            ],
            // 'event_after_head_link_config' => [
            //    ['fecfeed\event\Fecfeed','addHeadLinkConfig'],
            // ],
            
        ],
    ],
],
```

通过上面的配置可以看到，当代码执行`Yii::$service->event->trigger($metaAfterEventName, $view);`触发
event，就会执行@fecfeed\event\Fecfeed类的addHeadMetaConfig($view)方法，并把`$view`，传递过来
,代码如下：

```
<?php
namespace fecfeed\event;

use fecshop\services\Service;
use Yii;

class Fecfeed extends Service
{
    
    public static function addHeadMetaConfig( $view)
    {
        $view->registerMetaTag([
            'name' => 'p:domain_verify',
            'content' => 'ab1a1e2693892ce62a6a3812445b77d5'
        ]);
    }
}

```

保存后，可以到pc入口访问，查看html源代码，可以看到meta信息出来了。


3.如果我们想要开发插件B，加入meta信息，可以用同样的方法添加event事件，来完成我们的意愿。

到这里event机制就完成了，如果您想深入了解，可以下载一些使用了event的插件，研究一下代码


3.1插件`fecfeed`用到了`event_after_head_meta_config` : http://addons.fecmall.com/66888936

3.2插件`fecpaygate` 用到了`event_before_save_payment_config`  ： http://addons.fecmall.com/98739358


总之，event机制是为了更好的解决插件开发，以及多个插件的冲突问题。
