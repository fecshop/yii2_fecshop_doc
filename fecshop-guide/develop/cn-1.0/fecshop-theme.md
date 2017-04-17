Fecshop 模板（theme）
==============

> fecshop theme也就是多模板机制，详细参看
[fecshop 模板](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-rewrite-func.html#4-fecshopview-js-css)
这里不做详细的叙述。

### 模板文件的结构

这里说一下模板的构造，其实就是yii2的模板知识。

打开`@fecshop/appfront/theme/base/default`就进入了模板路径，可以看下面的文件夹：

`assets` :是 css js img存放的文件路径

`layouts` :是 页面主体部分，也就是从<html>标签开始，进入打开main.php
就可以看到，里面设置了如何添加css js等等。

`widgets` :是fecshop的小部件存放的view部分

`其他文件夹`：是fecshop的view部分，view部分作为content的一部分，
在上面的`layouts/main.php`种你可以看到如下的代码：

```
<?= $content; ?>
```

这个就是`view`文件部分内容，最终放到`layout`的html内容的位置。


对于yii2er，对这些并不会太陌生，只要了解了fecshop的模板重写机制就可以了。


多模板机制，详细参看
[fecshop 模板](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-rewrite-func.html#4-fecshopview-js-css)
这里不做详细的叙述。


### 开发fecshop的模板（view js css等）

对于用户来说想要二开appfront的模板，需要修改才能满足自己的需求，
但是对fecshop就比较难办，因为fecshop升级，难免也要修改view css js也要改动
等文件，这些文件不同于php类文件的重写机制，无法通过继承重写函数
的方式进行二开模板文件，
因此就带来了矛盾冲突，fecshop参考了magento的多模板机制，
设置二开的高优先级模板路径,譬如，fecshop想要找view文件
`/category/product/index.php`,首先会在二开模板路径里面找，如果
找到，就不会使用fecshop的模板路径下面的`/category/product/index.php`
因此通过这种方式实现的模板重写。

fecshop的模板部分，以入口进行区分（appfront apphtml5等）的同时，
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

用户二开的模板路径的定义在文件：
`appfront/config/fecshop_local_services/Store.php`

在每一个store中，您可以看到如下的内容：

```
	'localThemeDir'	=> '@appfront/theme/terry/theme01', # 设置当前store对应的模板路径。关于多模板的方面的知识，您可以参看fecshop多模板的知识。
	'thirdThemeDir'	=> [],  # 第三方模板路径，数组，可以多个路径				
```

`@appfront/theme/terry/theme01` ： 为本地二开路径，优先级最高

`thirdThemeDir`	: 第三方插件的模板路径，如果您安装了多个第三方
的插件，那么您需要按照顺序填写多个，这里是数组的方式填写。


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

[yii2 fecshop 多模板的介绍](http://www.fancyecommerce.com/2016/06/30/yii2-fecshop-%e5%a4%9a%e6%a8%a1%e6%9d%bf%e7%9a%84%e4%bb%8b%e7%bb%8d/)





















