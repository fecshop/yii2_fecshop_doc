Fecshop 小部件
==============

> fecshop小部件，不同于fecshop的小部件，fecshop的小部件是集数据库数据与view文件
> 生成的一个区块，譬如网站侧栏的热销产品，做成一个小部件，可以很方便的
> 在其他页面进行引入。当然，fecshop的head header（头部），footer（尾部）都是小部件实现的。

### 小部件结构：

小部件由两部分组成，动态数据提供部分 和 提供html代码的view部分，共同组合
，显示出来小部件。

### 小部件配置：
`@fecshop/config/services/Page.php`里面进行小部件的配置，示例代码：

```
'widget' => [
	'class' 		=> 'fecshop\services\page\Widget',
	'widgetConfig' => [
		'head' => [
			# 动态数据提供部分
			'class' => 'fecshop\app\appfront\widgets\Head',
			# 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
			'view'  => 'widgets/head.php',
			# 缓存
			'cache' => [
				'enable'	=> false, # 是否开启
				'timeout' 	=> 4500,  # 缓存过期时间
			],
		],
		'header' => [
			'class' => 'fecshop\app\appfront\widgets\Headers',
			# 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
			'view'  => 'widgets/header.php',
			'cache' => [
				'enable'	=> false,
				'timeout' 	=> 4500,
			],
		],
		'topsearch' => [
			'view'  => 'widgets/topsearch.php',
		],
```

譬如header小部件，数据提供部分为:`@fecshop\app\appfront\widgets\Headers.php`,
view部分为：`@fecshop\app\appfront\theme\base\default\widgets\header.php`。


其中，head header都是一个小部件，里面的class是动态数据提供部分，
view是显示部分，cache是缓存，您可以通过该配置将缓存打开，以及设置缓存的超时时间。

小部件的view部分遵循fecshop的多模板机制，可以在二开theme路径下添加
相应文件实现view部分的重写，可以通过classMap机制进行动态数据提供class文件
的重写。

### 小部件的使用：

```
<?= Yii::$service->page->widget->render('header',$this); ?>
```

上面传的的`$this`，在view文件中对应的变量为：`$parentThis`，举例子可以参看head小部件

```
<?= Yii::$service->page->widget->render('head',$this); ?>
```

```
<?php $parentThis->head() ?>
```

`$parentThis`就是`render()`函数调用传入的`$this`变量。














