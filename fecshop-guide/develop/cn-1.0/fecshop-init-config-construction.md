Fecshop 配置结构
================

> Yii2是多文件配置结构，将多个配置文件分散到各个路径下，
> 在初始化的时候最终合成一个配置数组，这种方式比较灵活，后面的数组和覆盖前面的数组
> 配置，这种方式非常适合重写某些组件，服务等


1. 入口文件加载的配置文件列表：
---------------------------

```
$config = yii\helpers\ArrayHelper::merge(
    require(__DIR__ . '/../../../common/config/main.php'),
    require(__DIR__ . '/../../../common/config/main-local.php'),
    require(__DIR__ . '/../../config/main.php'),
    require(__DIR__ . '/../../config/main-local.php'),
	# fecshop services config
	require(__DIR__ . '/../../../vendor/fancyecommerce/fecshop/config/fecshop.php'),
	# fecshop module config
	require(__DIR__ . '/../../../vendor/fancyecommerce/fecshop/app/appfront/config/appfront.php'),
	
	# thrid part confing
	
	# common modules and services.
	require(__DIR__ . '/../../../common/config/fecshop_local.php'),
	 
	# appadmin local modules and services.
	require(__DIR__ . '/../../config/fecshop_local.php')
    
);
```

对于
`yii\helpers\ArrayHelper::merge()`函数，可以点击这里查看具体的介绍：
[yii2 关于helper类 `ArrayHelper::merge()` 方法的介绍](http://www.fancyecommerce.com/2016/07/02/yii2-%E5%85%B3%E4%BA%8Ehelper%E7%B1%BB-arrayhelpermerge%EF%BC%88%EF%BC%89%E6%96%B9%E6%B3%95%E7%9A%84%E4%BB%8B%E7%BB%8D/)

merge函数里面的所有参数文件，最终合并成一个文件，如果配置文件中含有相同的配置项，
最后面的配置文件中的配置项，将覆盖前面的配置文件中的配置项。

2. 各个配置文件的详细阐述
---------------------------

2.1
`require(__DIR__ . '/../../../common/config/main.php'),`

这个是Yii2的配置文件，也是各个入口的公用配置，这个文件一般是加入到svn版本库中的

2.2
`require(__DIR__ . '/../../../common/config/main-local.php')`

这个是Yii2的配置文件，也是各个入口的公用配置，
里面一般是一些独有的配置，譬如mysql，mongodb，redis等，因为线上和线下的数据库配置不一样，
因此，这个文件一般是不加入到svn版本库中的，

2.3
`require(__DIR__ . '/../../config/main.php')`

该入口的Yii2的配置文件，一般添加到svn版本库

2.4
`require(__DIR__ . '/../../config/main-local.php')`

该入口的Yii2的配置文件，一般不添加到svn版本库

2.5
`require(__DIR__ . '/../../../vendor/fancyecommerce/fecshop/config/fecshop.php')`

fecshop的公用配置部分，里面是fecshop的service和component配置。
这个配置文件内容如下：

```
$services = [];
foreach (glob(__DIR__ . '/services/*.php') as $filename){
	$services = array_merge($services,require($filename));
}

# 组件
$components = [];
foreach (glob(__DIR__ . '/components/*.php') as $filename){
	$components = array_merge($components,require($filename));
}
 
return [
    'components' 	=> $components,
	'services' 		=> $services,
	'params'		=> [	
	
	],
];
```

他们加载其他文件夹下面的所有php文件进行合并,最终成为一个数组。

2.6
`require(__DIR__ . '/../../../vendor/fancyecommerce/fecshop/app/appfront/config/appfront.php')`

fecshop的appfront入口的配置部分

2.7 

添加第三方插件库的配置地址

2.8
`require(__DIR__ . '/../../../common/config/fecshop_local.php')`

本地用户用于二开的公用配置文件

2.9
`require(__DIR__ . '/../../config/fecshop_local.php')`
本地用户用于二开的appfront的配置文件


综上，2.8 和 2.9 是用于二开的配置，可以覆盖上面的其他配置，
因此，您如果想重写某个组件，某个service，甚至某个module
，可以通过添加配置的方式，重定向到您的路径中去。

配置文件是fecshop进行二开的重要部分，通过配置文件可以在不修改fecshop核心
源代码的前提下，修改fecshop和yii2的任意功能。
























