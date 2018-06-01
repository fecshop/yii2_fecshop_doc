fecshop模板
===========

> 这里是对fecshop模板的介绍


### 1.原理

fecshop的模板机制，是基于Yii2框架进行的二次封装，分为layout部分和view文件部分


1.1、`layout`：这个是模板的主体部分，在这里面做大体的整体框架


譬如：https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/theme/base/front/layouts/home.php

您可以通过代码来设置当前的layout文件
`Yii::$service->page->theme->layoutFile = 'home.php';`

譬如：https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/modules/Cms/Module.php
就是在模块的入口文件 Module.php，来为该模块指定模板layout文件。

1.2、`css js`文件，这个在layout中指定，
譬如：https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/theme/base/front/layouts/home.php
中指定了css 和 js

```
?php
$jsOptions = [
	# js config 1
	[
		'options' => [
			'position' =>  'POS_END',
		//	'condition'=> 'lt IE 9',
		],
		'js'	=>[
			'js/jquery-3.0.0.min.js',
			'js/jquery.lazyload.min.js',
			'js/owl.carousel.min.js',
			'js/js.js',
		],
	],
];
# css config
$cssOptions = [
	# css config 1.
	[
		'css'	=>[
			'css/style.css',
			'css/owl.carousel.css',
		],
	],
];
\Yii::$service->page->asset->jsOptions 	= \yii\helpers\ArrayHelper::merge($jsOptions, \Yii::$service->page->asset->jsOptions);
\Yii::$service->page->asset->cssOptions = \yii\helpers\ArrayHelper::merge($cssOptions, \Yii::$service->page->asset->cssOptions);				
\Yii::$service->page->asset->register($this);
?>

```

css 和 js的相对路径是模板路径下面的 `asset`文件夹，
也就是：https://github.com/fecshop/yii2_fecshop/tree/master/app/appfront/theme/base/front/assets

当然js 和 css也可以在配置文件中添加，更新的信息参看：

[Fecshop theme js and css](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-js-css.html)

[重写fecshop的模板](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-rewrite-func.html#4-fecshopview-js-css)

1.3、`view`：这个是具体的部分，相当于零碎的部件嵌入到layout文件中，对于
view文件，还可以包含其他的view文件，也就是部件中嵌入部分，譬如：

https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/theme/base/front/catalog/category/index.php
，通过代码可以加载子view文件

```
<?php
    $parentThis = [
        'query_item' => $query_item,
        'product_page'=>$product_page,
    ];
    $config = [
        'view'  		=> 'catalog/category/index/toolbar.php',
    ];
    $toolbar = Yii::$service->page->widget->renderContent('category_toolbar',$config,$parentThis);
    echo $toolbar;
?>
```

在config中指定了加载view文件，也就是：https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/theme/base/front/catalog/category/index/toolbar.php




### 2.fecshop多模板

多模板的原理参看：http://www.fancyecommerce.com/2016/06/30/yii2-fecshop-%E5%A4%9A%E6%A8%A1%E6%9D%BF%E7%9A%84%E4%BB%8B%E7%BB%8D/

多模板的原理2参看 ：http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-rewrite-func.html#4-fecshopview-js-css


fecshop模板开发：http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-theme.html

### 3.如何新建layout

参看示例帖子：http://www.fecshop.com/topic/1062


### 4.模板的嵌套

参看[Fecshop 模板view文件嵌套引用原理](fecshop_theme_view.md)












