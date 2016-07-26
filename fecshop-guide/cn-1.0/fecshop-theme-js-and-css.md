Fecshop theme js and css重写
============================

js 和 css 的重写和view ，layout类似，也是通过
模板路径的优先级，来完成重写。

### 1. fecshop如何添加js和css

在layout.php文件的顶部可以看到代码，譬如：
譬如：@fecshop/app/appfront/theme/base/front/layouts/home.php

```

<?php
$jsOptions =[ # js的配置部分
	[
		# js options ，来定义位置，条件等
		'options' => [
			'position' =>  'POS_END',
			'condition'=> 'lt IE 9',
		],
		# 在当前options下的js文件
		'js'	=>[
			'js/jquery-3.0.0.min.js',
			'js/js.js',
		],
	],
	# 另外一个js配置
	[
		# 定义另外一个options下的js文件
		'options' => [
			'condition'=> 'lt IE 9',
		],
		'js'	=>[
			'js/ie9js.js'
		],
	],
];

$cssOptions = [
	# css配置
	[
		'css'	=>[
			'css/style.css',
			'css/ie.css',
		],
	],
	
	# 另外一个css配置
	[
		# 这个css配置，有一定的条件
		'options' => [
			'condition'=> 'lt IE 9',
		],
		# css文件
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

每一个layout文件，都可以自定义当前的js和css文件。

js和css的文件是放到模板路径下的assets文件夹下面，如果要重写css或者js，
只需要在高优先级的模板路径下创建js或者css文件即可。

譬如：我想要重写 js文件：@fecshop/app/appfront/theme/base/front/assets/js/js.js

如果本地模板路径为：@appfront/theme/terry/theme01，
那么，新建文件 @appfront/theme/terry/theme01/assets/js/js.js 即可，
在加载js的文件，就会加载 @appfront/theme/terry/theme01/assets/js/js.js，
这样就完成了js文件的重写。






