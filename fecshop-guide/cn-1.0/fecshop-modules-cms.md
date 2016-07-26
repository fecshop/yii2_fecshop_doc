Fecshop Cms 模块介绍
====================

> cms 模块：包括：article单页面，home页面，static block，widgets等功能
，**前台模块** @fecshop\app\appfront\modules\Cms，
**后台模块** @fecshop\app\appadmin\modules\Cms。

### 1.Article功能

后台模块主要完成对Article功能的增删改查。
前台模块完成page的内容的展示，数据需要
调用 [[page-article]]服务。


调取当前store对应的语言的article，勾画出整个页面，
article一般用来做一些文字条款的页面说明。

### 2.home页面

勾画出来home页面。
首页的Title ，MetaKeywords，MetaDescription
在这个模块中进行配置,cms模块的配置如下：

```
<?php
return [
	'cms' => [
		'class' => '\fecshop\app\appfront\modules\Cms\Module',
		'params'=> [
			'homeTitle' 			=> 'fecshop home page',
			'homeMetaKeywords'		=> 'fecshop , fancy ecommerce shop ',
			'homeMetaDescription'	=> 'fancy ecommerce shop , base Yii2 framework',
		],
	],
];

```
		

### 3.static block页面

这个是静态块部分，静态块是在后台配置的一些静态的html
，前台通过配置的方式可以使用函数方便的调用显示。
在静态块中，可以使用一些规定的变量，譬如首页地址等。

### 4.widgets 定义。

这里是各个区块，
定义：Footer.php,Head.php, Header.php , Menu.php ,等。
相应的view文件在 @fecshop\app\appfront\theme\base\front\widgets\下
，通过 <?= Yii::$service->page->widget->render('head',$this); ?>
将其显示出来。 在 @fecshop\appfront\config\fecshop_local_services\Page.php
中 对 page的子服务widget 进行了配置，里面有如下：

```
'widget' => [
	'widgetConfig' => [
		'head' => [
			'class' => 'fecshop\app\appfront\modules\Cms\block\widgets\Head',
			# 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
			'view'  => 'widgets/head.php',
			'cache' => [
				'enable'	=> false,
				'timeout' 	=> 4500,
			],
		],
		'header' => [
			'class' => 'fecshop\app\appfront\modules\Cms\block\widgets\Headers',
			# 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
			'view'  => 'widgets/header.php',
			'cache' => [
				'enable'	=> true,
				'timeout' 	=> 4500,
			],
		],
		'menu' => [
			'class' => 'fecshop\app\appfront\modules\Cms\block\widgets\Menu',
			# 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
			'view'  => 'widgets/menu.php',
			'cache' => [
				'enable'	=> false,
				//'timeout' 	=> 4500,
			],
		],
		'footer' => [
			'class' => 'fecshop\app\appfront\modules\Cms\block\widgets\Footer',
			# 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
			'view'  => 'widgets/footer.php',
			'cache' => [
				'enable'	=> false,
				//'timeout' 	=> 4500,
			],
		],
		'scroll' => [
			#'class' => 'fecshop\app\appfront\modules\Cms\block\widgets\Scroll',
			# 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
			'view'  => 'widgets/scroll.php',
		],
	]
	
],
```

可以通过开启cache，而进行缓存widgets，最后，将区块画出来。
















