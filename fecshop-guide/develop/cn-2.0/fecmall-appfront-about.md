Fecmall Appfront 关于和介绍
=========================

> Appfront 入口对应的pc端浏览器访问的入口


### Appfront入口文件

1.默认入口文件： `@appfront/web/index.php`

2.对于其他store的，根据配置，有的是`@appfront/web/index.php`，有的是在
该路径下的其他语言的文件夹里面，譬如：`@appfront/web/fr/index.php`
, `@appfront/web/cn/index.php`

3.打开index.php ， 你会发现加载了很多的配置文件，通过`yii\helpers\ArrayHelper::merge()`
函数进行覆盖合并，最终形成一个配置文件

4.因为初始化，有大量的配置文件需要合并，这本身就是一个开销，因此，可以先合并生成一个配置文件，
然后在加载这个合并后的配置文件，即可节省资源，详细参看:http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-about-config.html
,该地址页面的最下面即可查看。

### Appfront 配置


1.本地配置文件路径：`@appfront/config/` ，打开这个文件夹，可以看到很多配置文件

1.1 Yii2框架的配置文件

`bootstrap.php`：这个是Yii2框架初始化执行的部分，详细参看：
[启动引导（Bootstrapping）](http://www.yiichina.com/doc/guide/2.0/runtime-bootstrapping)

`main.php`: 这里是对入口定义 ，另外配置一些Yii2的组件，譬如component部分就是配置的Yii2
的组件，关于Yii2组件的更详细的介绍，可以参看：
[Yii2 应用组件](http://www.yiichina.com/doc/guide/2.0/structure-application-components)


`main-local.php`: Yii2框架的一些配置，这个文件是在init的时候生成了，
每次执行init，在该文件中生成的 `cookieValidationKey` 都不一样

`params.php` `params-local.php`：是Yii2 param的配置 

1.2 Fecmall系统本地配置文件

`@appfront/config/fecshop_local_modules/*`： 本地模块配置部分

`@appfront/config/fecshop_local_services/*`： 本地services配置部分

`fecshop-local.php` ：fecshop的入口加载部分,这个部分的作用是加上上面2个部分里面的所有
配置文件，打开查看代码即一目了然

```
<?php

// 本文件在app/web/index.php 处引入。

// fecshop的核心模块
$modules = [];
foreach (glob(__DIR__.'/fecshop_local_modules/*.php') as $filename) {
    $modules = array_merge($modules, require($filename));
}
// 服务器组件
$services = [];
foreach (glob(__DIR__.'/fecshop_local_services/*.php') as $filename) {
    $services = array_merge($services, require($filename));
}

return [
    'modules'  => $modules,
    'services' => $services,
];
```


`YiiClassMap.php` ：这个是Yii2的classMap机制，可以参看[类映射表（Class Map）](http://www.yiichina.com/doc/guide/2.0/concept-autoloading#class-map)
，关于Yii2 classMap在fecshop中的使用，参看：[重写yii2框架的class classMap的方式](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-rewrite-func.html#7yii2classclassmapfecshop)


`YiiRewriteMap.php`：这个是fecmall的机制，详细参看：[通过rewriteMap进行重写Block Model 层 ](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-rewrite-func.html#8rewritemapblock-model)

1.3 对于Fecmall系统appfront的配置文件，在
`vendor/fancyecommerce/fecshop/app/appfront/config` 下面

关于Fecmall更详细的配置结果，参看:[Fecmall 配置结构](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-init-config-construction.html)

2.多语言

多语言是在本地翻译文件路径 @appfront/languages/下面，
对于Fecshop的多语言的翻译文件是在： @fecshop/app/appfront/languages/下面，
您可以在本地翻译文件中，对fecshop的翻译进行重写，或者添加新的翻译内容。


### 本地开发。

1.组件重写或开发新组件： 建立写到@appfront/local/local_components 下面

2.模块重写或开发新模块：建立写到@appfront/local/local_modules 下面

models， services，等都写到 @appfront/local 下面

如果您想在本地开发一个全新的模块，可以参看：
[Fecmall，本地Appfront入口新建modules](http://www.fecmall.com/topic/451)

3.模板Theme：建议写到 @appfront/theme/terry/theme01 路径下, 在这里新建模板view
文件，layouts文件  ，以及相应的assets文件（里面是js和css img等文件。）

`terry` ：模板包名

`theme01`：模板名

