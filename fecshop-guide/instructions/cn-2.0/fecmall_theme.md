fecmall模板
===========

> 这里是对fecmall模板的介绍


### 1.原理

fecmall的模板机制，是基于Yii2框架进行的二次封装，分为layout部分和view文件部分


1.1、`layout`：这个是模板的主体部分，在这里面做大体的整体框架


譬如：https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/theme/base/front/layouts/home.php

您可以通过代码来设置当前的layout文件(在模块的入口文件，或者controller文件中设置)
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

[Fecmall theme js and css](http://www.fecshop.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-js-css.html)

[重写fecmall的模板](http://www.fecshop.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-rewrite-func.html#4-fecshopview-js-css)

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




### 2.fecmall多模板

多模板的原理参看：http://www.fancyecommerce.com/2016/06/30/yii2-fecshop-%E5%A4%9A%E6%A8%A1%E6%9D%BF%E7%9A%84%E4%BB%8B%E7%BB%8D/

多模板的原理2参看 ：http://www.fecshop.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-rewrite-func.html#4-fecshopview-js-css

fecmall模板开发：http://www.fecshop.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-theme.html

### 3.fecmall使用绝对模板路径

您可以指定模板绝对路径，绕过fecmall多模板

@fecshop/app/appfront/config/appfront.php 可以看到如下的配置：

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

上面的注释就是一个例子，可以将分类页面的url，指定到具体的view文件，

`'catalog/category/index'`:  模块/controller/action 

这种方式，比较适合应用插件开发，当插件想要替换controller的某个view file，可以直接
指定，绕靠多模板机制（不需要添加多模板路径）。


### 4.theme widget

对于view，里面有一些独立块widget，以独立的形式，方便在各个view中调用，譬如：

https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/theme/base/front/layouts/main.php#L70

```
<?= Yii::$service->page->widget->render('base/header',$this); ?>
```
调用的就是一个独立块widget，对于appfront，widget匹配的路径为：
https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/config/appfront.php#L119



### 3.如何新建layout

参看示例帖子：http://www.fecshop.com/topic/1062


### 4.模板的嵌套

参看[Fecshop 模板view文件嵌套引用原理](fecshop_theme_view.md)












