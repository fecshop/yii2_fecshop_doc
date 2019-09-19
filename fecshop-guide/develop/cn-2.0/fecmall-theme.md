Fecmall 模板（theme）
==============

> fecmall theme也就是多模板机制，详细参看
[fecmall 模板](http://www.fecshop.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-rewrite-func.html#4-fecshopview-js-css)
这里不做详细的叙述。


### 多模板机制

多模板机制的方式查找view文件，也就是多个模板路径，通过优先级
依次查找，知道找到位置，这个类似于magento的多模板机制


`fecmall的模板路径`: fecmall的模板路径，view文件最全，但是优先级最低

`fecmall第三方模板路径`：第三方开发的应用模板路径，优先级次之

`本地开发模板路径`：本地的模板路径，优先级最高

store设置`第三方模板路径` 和 `本地开发模板路径`

![](images/p51.png)

您可以为不同的store设置不同的`第三方模板路径` 和 `本地开发模板路径`，
`第三方模板路径`可以设置多个，逗号隔开，
`本地开发模板路径`指的是您本地开发的模板路径，您可以改成其他的模板路径。


### UrlKey设置具体的view文件（绝对路径）

如果您在配置中指定了某urlKey对应的view文件路径（并以@开头），那么会直接加载该
view文件，不会走多模板机制，譬如：

@fecshop/app/appfront/config/appfront.php

```
'services' => [
        'page' => [
            'childService' => [
                'theme' => [
                    'viewFileConfig' => [
                        // 'catalog/category/index' => '@fecshop/app/appfront/theme/base/front/catalog/category/index.php',
                    ],
                ],
                
                ...
```

如果去掉注释，那么访问分类页面，将直接加载对应的view文件，不在走多模板机制

这种方式比较适合某些插件重写view，如果本地想要二开，可以通过配置覆盖这个配置，
更改成其他的view文件即可。


### widget部分

> widget是在view文件引用的小部件，可以做成多个独立小部件，在各个view中直接调用。

对于widget，譬如:https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/theme/base/front/layouts/main.php#L64

```
<?= Yii::$service->page->widget->render('base/head',$this); ?>
```
就是调用一个widget，fecmall系统配置的widget是在配置文件：https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/config/appfront.php#L108

你可以通过多模板的方式（上面的1部分）重写widget，也可以通过指定绝对路径
的方式（上面的2部分），指定绝对路径，譬如：

```
'header' => [
    'class' => 'fecshop\app\appfront\widgets\Headers',
    'view'  => '@fecfurlica/views/header.php',   // @开头，指定绝对路径。
    'cache' => [
        'timeout'    => 4500,
    ],
],
```   



对于分类页面：'catalog/category/index'，对应的view文件直接是后面配置对应的view文件，
view文件以@开头，可以直接找到绝对路径，这种方式绕开了多模板机制，可以直接指定view文件

> 这种方式非常适合一些应用插件，应用插件只会改很少页面的view，可以直接
指定页面对应的view文件，方便做应用插件。





### 模板文件的结构

这里说一下模板的构造，其实就是yii2的模板知识。

打开`@fecshop/appfront/theme/base/default`就进入了模板路径，可以看下面的文件夹：

`assets` :是 css js img存放的文件路径

`layouts` :是 页面主体部分，也就是从<html>标签开始，进入打开main.php
就可以看到，里面设置了如何添加css js等等。

`widgets` :是fecmall的小部件存放的view部分

`其他文件夹`：是fecmall的view部分，view部分作为content的一部分，
在上面的`layouts/main.php`种你可以看到如下的代码：

```
<?= $content; ?>
```

这个就是`view`文件部分内容，最终放到`layout`的html内容的位置。


对于yii2er，对这些并不会太陌生，只要了解了fecshop的模板重写机制就可以了。


多模板机制，详细参看
[重写fecmall的模板（view js css等）](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-rewrite-func.html#4-fecshopview-js-css)
这里不做详细的叙述。







### 开发fecmall的多模板机制（view js css等，再次详细讲解）

`fecmall模板原理`：对于用户来说想要二开appfront的模板，需要修改才能满足自己的需求，
但是对fecmall就比较难办，因为fecmall升级，难免也要修改view css js也要改动
等文件，这些文件不同于php类文件的重写机制，无法通过继承重写函数
的方式进行二开模板文件，
因此就带来了矛盾冲突，fecmall参考了magento的多模板机制，
设置二开的高优先级模板路径,譬如，fecshop想要找view文件
`/category/product/index.php`,首先会在二开模板路径里面找，如果
找到，就不会使用fecshop的模板路径下面的`/category/product/index.php`
因此通过这种方式实现的模板重写。

fecmall的模板部分，以入口进行区分（appfront apphtml5等）的同时，
每一个store又是可以单独选择模板的。

模板的重写原理是通过模板路径优先级来，也就是有好几个
模板路径，分别为fecshop的模板路径【低优先级】，第三方的模板路径【中优先级】，
用户二开（二次开发）的模板路径【高优先级】，fecshop的模板路径的文件最为
全面（优先级最低），然后用户想要重写某个文件，只需要把这个文件路径复制到
二开模板路径下（包括相对文件夹路径），即可完成重写，因为
用户二开模板路径优先级最高。


下面以appfront（pc端）进行举例
说明：

appfront入口的模板路径的配置是在：

`@fecshop/app/appfront/config/params.php`

```
'appfrontBaseTheme' 	=> '@fecshop/app/appfront/theme/base/front',
```

也就是默认所有的store都是使用这里的模板，

用户二开的模板路径，和第三方模板的路径，可以在后台设置

![](images/p51.png)

重写模板详细举例：
fecshop模板路径为：`@fecshop/app/appfront/theme/base/default`，
我想要重写这个view文件:
@fecshop/app/appfront/theme/base/default/catalog/category/index.php


我本地store设置的模板路径为:
`appfront/theme/terry/theme01`

因此，我创建文件

`appfront/theme/terry/theme01/catalog/category/index.php`

然后把`@fecshop/app/appfront/theme/base/default/catalog/category/index.php`
文件的内容复制到`@appfront/theme/terry/theme01/catalog/category/index.php`
中，然后修改这个文件，就完成了该文件的重写。

是不是很easy呢？

原理还是有一点小复杂，有兴趣可以参看资料：

[yii2 多模板路径优先级加载view方式下- js和css 的解决](http://www.fancyecommerce.com/2016/07/06/yii2-%e5%a4%9a%e6%a8%a1%e6%9d%bf%e8%b7%af%e5%be%84%e4%bc%98%e5%85%88%e7%ba%a7%e5%8a%a0%e8%bd%bdview%e6%96%b9%e5%bc%8f%e4%b8%8b-js%e5%92%8ccss-%e7%9a%84%e8%a7%a3%e5%86%b3/)

[yii2 fecmall 多模板的介绍](http://www.fancyecommerce.com/2016/06/30/yii2-fecshop-%e5%a4%9a%e6%a8%a1%e6%9d%bf%e7%9a%84%e4%bb%8b%e7%bb%8d/)



### 实战模板

上面说了很多，还是先撸起来在说，您可以参考下这个模板：
http://addons.fecmall.com/83829447


您可以参考这个，开发fecmall的模板，您可以将您的模板发布到应用市场，
赚取RMB


如果您有迷惑，可以去论坛发帖求助。














