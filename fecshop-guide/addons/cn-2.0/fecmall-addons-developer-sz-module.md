Fecmall-module模块部分
===========

> Fecmall module模块，本质就是yii2框架的module

### Fecmall-module模块

您可以在应用扩展插件的config.php文件，各个入口的config部分，加入modules的配置

譬如Appfront入口：

```
'appfront' => [
    'enable' => true,
    'config' => [
        'modules' => [
            // 1. coupon module 配置
            'coupon' => [
                'class' => '\fecyo\app\appfront\modules\Coupon\Module',
            ],
            // 2.checkout modules，重写（或者新建）fecmall checkout模块的某个controller
            'checkout' => [
                'controllerMap' => [
                    'cartinfo' => 'fecyo\app\appfront\modules\Checkout\controllers\CartInfoController',          
                ],
            ],
        ],
    ],
],
```

### 新建module


1.在 `modules config` 里面加入相关配置，譬如：


```
'coupon' => [
    'class' => '\fecyo\app\appfront\modules\Coupon\Module',
],
```

2.新建模块class文件`@fecyo\app\appfront\modules\Coupon\Module.php`

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace fecyo\app\appfront\modules\Coupon;

use fecshop\app\appfront\modules\AppfrontModule;
use Yii;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 * Catalog Module 模块
 */
class Module extends AppfrontModule
{
    public $blockNamespace;

    public function init()
    {
        parent::init();
        // 以下代码必须指定
        $nameSpace = __NAMESPACE__;
        // 如果 Yii::$app 对象是由类\yii\web\Application 实例化出来的。
        if (Yii::$app instanceof \yii\web\Application) {
            // 设置模块 controller namespace的文件路径
            $this->controllerNamespace = $nameSpace . '\\controllers';
            // 设置模块block namespace的文件路径
            $this->blockNamespace = $nameSpace . '\\block';
        
        }
        
        /// 设置该模块的view(theme)的默认layout文件。
        Yii::$service->page->theme->layoutFile = 'main.php';
        
    }
}


```

对于各个入口的module，有一些细微的差别，您可以去fecmall里面找一个配置文件，复制过来即可，
譬如，对于appfront里面的，可以在appfront里面复制一个模块的class文件，然后改改路径即可


对于此例子,init函数的内容，您不需要进行改动，如果想设置view layout文件，可以将main.php改成您自己的文件即可


3.新建controllers和block文件夹


```
fecyo\app\appfront\modules\Coupon\controllers\
fecyo\app\appfront\modules\Coupon\block\
```

然后在里面新建相应的controller和block即可，具体您可以参看一下fecmall里面的实现



4.在模板路径里面新建相应的theme view文件即可



### 在已有的module中添加新的controller，或者覆盖已有的controller

当fecmall已经有了`Checkout`,您想在该模块里面添加新的controller文件，或者重写已有的，
可以通过`controllerMap`机制来实现

```
'checkout' => [
    'controllerMap' => [
        'cartinfo' => 'fecyo\app\appfront\modules\Checkout\controllers\CartInfoController',          
    ],
],
```

1.如果fecmall源码中的Checkout模块，已经存在CartInfoController，则会进行重写操作

2.如果fecmall源码中的Checkout模块，不存在CartInfoController，则相当于添加新的controller文件


### controller和block

1.关于controller和block的关系，您可以参看文档：[Fecmall 架构](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-construct-framework.html)

2.关于函数`$this->getBlock()`

controller一般通过代码 `$data = $this->getBlock()->getLastData();` ， 来获取block的数据
，`$this->getBlock()`默认对应的文件，就是block文件夹里面的文件。

譬如：

```
// 用户购物车页面进入下单页面，如果用户没有货运地址，那么进入该页面进行货运地址的add
public function actionAddressadd()
{
    Yii::$service->page->theme->layoutFile = 'one_step_checkout.php';
    $data = $this->getBlock()->getLastData();
    return $this->render($this->action->id, $data);
}
```

`./controllers/CartinfoController`里面的 `actionAddressadd` 方法里面执行 `$this->getBlock()`，对应的block文件
就是 `./block/cartinfo/Addressadd.php`
,可以看出命名和文件的对应关系,然后在 `./block/cartinfo/Addressadd.php`里面实现`getLastData()`函数就可以了。

关于 `$this->getBlock()`函数的具体代码，可以参看: https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/modules/AppfrontController.php#L64


3.重写block文件

重写block文件有2种：

3.1通过重写controller文件的方式重写block文件，这种方式适合您需要吧controller里面的所有方法都重写

在controller类里面，加入`类变量`,如下：

```
public $blockNamespace = 'fecyo\app\appfront\modules\Checkout\block';
```

当controller里面的函数执行`$this->getBlock()`，对应的将是新的block文件路径，具体原理您可以参看`$this->getBlock()`的代码。

这样，您在应用扩展文件夹里面，新建新的block文件即可。


3.2通过`fecRewriteMap`

这种方式适合只对模块里面的某个block文件进行重写

```
// 1.appfront层
'appfront' => [
    // appfront入口的开关，如果false，则会失效
    'enable' => true,
    'config' => [
        // 重写model和block
        'fecRewriteMap' => [
            '\fecshop\app\appfront\modules\Cms\block\home\Index'  => '\fectfurnilife\app\appfront\modules\Cms\block\home\Index',
            '\fecshop\app\appfront\modules\Customer\block\address\Edit'  => '\fectfurnilife\app\appfront\modules\Customer\block\address\Edit',
        ],
    ],
],
```

左边的fecmall的block文件路径，右边是重写后的block文件路径，您按照这个格式对应好即可，
重写的block文件类继承于fecmall block 类, 然后重写里面相应的函数即可。


参考资料：[通过rewriteMap进行重写Block Model 层](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-rewrite-func.html#8rewritemapblock-model)


至此，fecmall的模块部分基本完成

参考学习资料：


[Fecmall 在现有的modules上面开发新controller](http://www.fecmall.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_new_controller_in_current_modules.html)

[Fecmall 本地新建modules，开发新功能](http://www.fecmall.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_hand_local_module.html)

[Fecmall appadmin 本地增加一个modules例子](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-appadmin-developer.html#)



[Yii2框架模块知识点](https://www.yiichina.com/doc/guide/2.0/structure-modules)















