Fecmall 功能初始化
==================

> 这里讲述的是在 Fecmall 初始化的过程中，通过配置的方式嵌入到Yii2的初始化进程中
> 的部分功能。

1.Fecmall 入口文件
-----------------

在入口文件index.php执行,也就是 @app/web/index.php (@app 统称各个入口，譬如 @appfront, @apphtml5)
,打开这个文件，你会发现加载了很多的配置
，对于入口文件index.php的初始化，您可以参看：
[Fecmall index.php初始化](fecshop-init-index.md)


2.Fecmall - Yii2框架初始化
------------

当在index.php最后执行下面的代码的时候，就开始了Yii2 初始化过程

```
$application = new yii\web\Application($config);
$application->run();
```

2.1 Fecmall - Yii2 BootStrap（Yii2框架初始化）

这个部分，主要是store的初始化，详细参看：
[Fecmall Store初始化](fecmall-init-store.md)

3.Fecmall - Request Url初始化
------------------

对于该部分，详细参看：

[Fecmall Request Url初始化](Fecmall-init-request-url.md)

4.Module - 模块
------------

4.1模块的配置

完成了上面的初始化，就要执行模块部分了，
对于各个入口的模块部分配置，可以在
@fecshop/app/appXxx/config/modules/*.php中看到，

每个配置文件都是一个模块的配置，里面的class指向的文件就是
模块的入口文件，
譬如：@fecshop/app/appfront/config/modules/Catalog.php

```
'catalog' => [
        'class' => '\fecshop\app\appfront\modules\Catalog\Module',

    ],
```

找到模块入口class文件：`@fecshop\app\appfront\modules\Catalog\Module.php`


4.2模块结构

打开文件夹：`@fecshop\app\appfront\modules\Catalog\` 可以看到

`Module.php`:模块的入口文件

`controllers`：模块的controller文件存放路径

`block`：controller里面调用`$this->getBlock()->getLastData();`
的文件就是按照路径存放到block文件夹下面

`helpers`：模块的一些帮助函数

5.模板Theme部分：
------------

fecshop采用的是多模板机制，关于这个，可以参看
：[Fecmall-theme](fecmall-theme.md)


6.Fecshop二次开发：
------------

对于二次开发，你可以参看：
[Fecmall 重写功能](fecmall-rewrite-func.md)


7.fecmall 数据库
------------

参看：[fecmall 数据库](fecmall-database.md)








