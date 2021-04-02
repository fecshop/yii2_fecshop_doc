Fecmall-component组件部分
=============

> fecmall component组件, 本质就是yii2框架的组件。

### Fecmall-component组件

1.Yii2基础组件

fecmall基于yii2开发，使用了yii2的很多基础组件，譬如：db，request，user，log，urlManager
，mongodb，cache, session 等

2.fecmall新开发的组件：

除了使用yii2的基础组件，fecmall还开发了一些组件：https://github.com/fecshop/yii2_fecshop/tree/master/config/components




### 组件配置

在应用扩展种配置组件compontent

```
'common' => [
    'enable' => true,
    // 公用层的具体配置下载下面
    'config' => [
        'components' => [
            'serviceLog' => [
                'class' => 'fecshop\components\ServiceLog',
            ]
        ]
    ],
]

```


对于`组件compontent`，`services`等，一般各个入口都会使用，而且是`懒加载机制`，
只有在调用的时候才会实例化，因此一般在`common公用`部分配置，配置后各个入口都可以调用。

譬如上面配置的serviceLog组件, 放到 `common`里面，appfront和apphtml5都可以


### 组件使用

1.添加配置，参看上面的配置例子


2.创建文件

```
<?php
namespace fecshop\components;

use Yii;
use yii\base\BootstrapInterface;
use yii\base\Component;

class ServiceLog extends Component
{
    public function logInfo()
    {
    }
}  
```

3.组件调用


```
Yii::$app->serviceLog->logInfo();
```



### Yii2组件资料


[Yii2应用组件](https://www.yiichina.com/doc/guide/2.0/structure-application-components)



[yii2组件（Component）](https://www.yiichina.com/doc/guide/2.0/concept-components)










