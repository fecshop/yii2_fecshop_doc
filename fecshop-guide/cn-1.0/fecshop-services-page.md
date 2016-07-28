Fecshop Page 服务
=================

> Page提供很多子服务功能，您可以通过`Yii::$service->page->childService->XFunc();`
来访问Page服务的子服务。

下面介绍page服务的子服务。

### 1.page子服务 - Asset服务

该服务是js和css注册功能，该功能读取多模板路径的js和css信息的数组，
通过高优先级的模板路径依次查找js和css文件，找到后返回，最终找到所有的css和js文件，
，然后将js和css发布到`web/assets`路径下，并把js和css注册到`$view`中

例子：

文件：`@fecshop\app\appfront\theme\base\front\layouts\home.php`
在文件的顶部可以看到代码：

```
<?php
$jsOptions = [
	# js config 1
	[
		'options' => [
			'position' =>  'POS_END',
		//	'condition'=> 'lt IE 9',
		],
		'js'	=>[
			'js/jquery-3.0.0.min.js',
			'js/js.js',
		],
	],
	# js config 2
	[
		'options' => [
			'condition'=> 'lt IE 9',
		],
		'js'	=>[
			'js/ie9js.js'
		],
	],
];

# css config
$cssOptions = [
	# css config 1.
	[
		'css'	=>[
			'css/style.css',
			'css/ie.css',
		],
	],
	
	# css config 2.
	[
		'options' => [
			'condition'=> 'lt IE 9',
		],
		'css'	=>[
			'css/ltie9.css',
		],
	],
];
\Yii::$service->page->asset->jsOptions 	= $jsOptions;
\Yii::$service->page->asset->cssOptions = $cssOptions;				
\Yii::$service->page->asset->register($this);
?>
```

也就是通过数组的方式读取上面的js文件，然后通过
多模板机制找到js和css文件，然后通过`\Yii::$service->page->asset->register($this);`函数
，将文件发布到`web/assset`下面，然后将js和css的发布后的
地址注册到`$view`中，总之，fecshop的`css`和`js` 以及`css`对应
的`image`都是依赖`asset`服务实现。

### 2.page子服务 - Breadcrumbs 服务

面包屑导航服务，还未做


### 3.page子服务 - Currency 服务

对货币操作的一些服务函数，
譬如： 初始化当前`store`货币，得到当前货币的价格，
设置货币，等等。



### 4.page子服务 - Menu 服务

得到menu数组的服务


### 5.page子服务 - Newsletter 服务

订阅邮件

### 6.page子服务 - Theme 服务

多模板的模板服务，该模块一般用来查找多模板下的文件，
也就是先根据优先级，初始化一个多模板数组，
然后当要查找`js`和`css`的时候，从高优先级的模板依次
查找文件，找到则返回，找不到，到下一个模板路径，
直到找到文件。



### 7.page子服务 - Translate 服务

文字翻译服务，可以通过`Yii::$service->page->translate->__('Hello, {username}!', ['username' => $username]);`
来翻译文字，appfront的翻译文字（fecshop的翻译文件）在
`@fecshop\app\appfront\languages`下面，
用户可以在`@appfront\config\languages` 下面的
相应的语言中添加翻译，就可以覆盖
`@fecshop\app\appfront\languages`里的翻译

当前store的language初始化，是store服务实现的，也就是`Yii::$service->store`

### 8.page子服务 - Widget 服务

独立块服务，这个是通过一个`block（数据提供者）`和一个`view（html数据显示者）`
文件来完成的

首先需要配置widget:

```
'page' => [
		'childService' => [
			
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

`class`是数据的提供者，也就是block文件，`view`文件是
html显示者，上面配置的view
文件，同样遵循多模板机制，

您可以通过`Yii::$service->page->widget->render('header')`,
来调用，调用后就会显示这个区块。

譬如：在layout文件中的调用

```
<?= Yii::$service->page->widget->render('footer',$this); ?>
```

`$this`也就是当前调用者
，如果`$this`参数如果传入，那么，view文件中，
`$parentThis`变量就是传入的`$this`，

譬如：通过下面的方法调用：

layout 文件  home.php 调用独立块`footer`

```
<?= Yii::$service->page->widget->render('footer',$this); ?>
```

`widgets/footer.php`（view文件）中有代码

```
<?php $parentThis->head() ?>
```

这个`$parentThis` 就是上面的render中传入的`$this`,
也就是说，在layout文件中可以使用的函数，
在`widgets/footer.php`都可以使用`$parentThis`
来调用。








