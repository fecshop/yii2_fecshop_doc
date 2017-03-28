Fecshop 配置结构
================

> fecshop 配置结构是层级覆盖的方式，通过yii2的 `yii\helpers\ArrayHelper::merge()`函数
> 将所有的配置进行合并，最终成为一个大数组。配置结构通过层级覆盖的方式可以很方便的对fecshop的功能进行重写
> 

配置文件以及优先级
-----------------

#### 1.fecshop合并的配置文件：

fecshop配置是根据优先级，优先级高的配置可以覆盖优先级低的配置，
优先级由低到高的排列如下（其实就是index.php中的代码）：

```
$config = yii\helpers\ArrayHelper::merge(
    require(__DIR__ . '/../../common/config/main.php'),
    require(__DIR__ . '/../../common/config/main-local.php'),
    require(__DIR__ . '/../config/main.php'),
    require(__DIR__ . '/../config/main-local.php'),
	# fecshop services config
	require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/config/fecshop.php'),
	# fecshop module config
	require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/app/appfront/config/appfront.php'),
	
	# thrid part confing
	
	# common modules and services.
	require(__DIR__ . '/../../common/config/fecshop_local.php'),
	 
	# appadmin local modules and services.
	require(__DIR__ . '/../config/fecshop_local.php')
    
);
```
1到4，是Yii2框架的配置文件结构：

1.`@common/config/main.php`			# Yii2 公用配置，一般是Yii2的一些组件的公用配置。

2.`@common/config/main-local.php`		# Yii2 本地公用配置，一般是Yii2的一些数据库组件的配置

3.`@app/config/main.php	`			# Yii2 本app内的配置

4.`@app/config/main-local.php`		# Yii2 本app内的本地配置

5和6部分，是fecshop的配置文件结构：

5.`@vendor/fancyecommerce/fecshop/config/fecshop.php` 				# Fecshop的公用配置，一般是组件和服务的配置。

6.`@vendor/fancyecommerce/fecshop/app/appfront/config/appfront.php`	# Fecshop appfront这个入口的独有配置，里面包含模块和一些组件的配置。

第7部分为第三方开发的扩展的配置引入部分，您使用的第三方插件的配置，可以在这里引入进来。

7.第三方配置文件地址。

8和9部分，是二次开发者的配置文件部分：

8.`@common/config/fecshop_local.php`	# 二次开发者的各个入口的公用配置

9.`@app/config/fecshop_local.php`		# 二次开发者的当前入口的独有配置

上面8个配置文件的内容，通过`yii\helpers\ArrayHelper::merge()`函数合并，最后
形成一个数组，在合并的过程中，1的优先级最低，8个优先级最高，优先级高的配置
项可以覆盖优先级低的配置项。

覆盖顺序：

```
1.fecshop（5-6）可以覆盖前面Yii2的配置项(1-4)
2.第三方扩展（7），可以覆盖fecshop的配置项(1-6)
3.二次开发者（8-9）可以覆盖上面所有的配置(1-7)
```

#### 2.对于运费的配置，是通过csv的方式存储公式，路径为
`@common/config/shipping/fast_shipping.csv`

#### 3.yii class map重写机制

```
$yiiClassMap = require(__DIR__ . '/../config/YiiClassMap.php');
if(is_array($yiiClassMap) && !empty($yiiClassMap)){
	foreach($yiiClassMap as $namespace => $filePath){
		Yii::$classMap[$namespace] = $filePath;
	}
}
```
通过classMap的配置，可以重写任意一个class文件，譬如

```
<?php
return [
	'fecshop\app\appfront\helper\test\My' => '@appfront/helper/My.php',   
];
```

具体使用方法参看文章：[通过配置的方式重写某个Yii2 文件 或第三方扩展文件](http://www.fancyecommerce.com/2016/10/13/%e9%80%9a%e8%bf%87%e9%85%8d%e7%bd%ae%e7%9a%84%e6%96%b9%e5%bc%8f%e9%87%8d%e5%86%99%e6%9f%90%e4%b8%aayii2-%e6%96%87%e4%bb%b6-%e6%88%96%e7%ac%ac%e4%b8%89%e6%96%b9%e6%89%a9%e5%b1%95%e6%96%87%e4%bb%b6/)


优先级部分配置细化 - yii\helpers\ArrayHelper::merge()部分
--------

> 上面的9个配置文件，有的配置文件还包含其他的配置文件，下面逐一列举

### 1.`@vendor/fancyecommerce/fecshop/config/fecshop.php`

该配置文件包含:

1.1`@vendor/fancyecommerce/fecshop/config/services/*.php` 
,这个文件夹下面所有的php配置文件，这里面是各个Fecshop Services（服务）的配置

1.2`@vendor/fancyecommerce/fecshop/config/components/*.php `
，这个文件夹下面的所有的php文件，这里面是各个Fecshop Component（组件）的配置

### 2.`@vendor/fancyecommerce/fecshop/app/appfront/config/appfront.php`

该配置文件包含：

2.1`@vendor/fancyecommerce/fecshop/app/appfront/config/params.php`
这里面是一些参数的默认配置。

2.2`@vendor/fancyecommerce/fecshop/app/appfront/config/modules/*.php`
这个文件夹下面所有的php配置文件，这里面是各个模块对应的配置

### 3.`@common/config/fecshop_local.php`

该配置文件包含：

3.1`@common/config/fecshop_local_modules/*.php`
这个文件夹下面所有的php配置文件，这里面是二次开发的公用部分，添加或重写的
模块方面的配置

3.2`@common/config/fecshop_local_services/*.php`
这个文件夹下面所有的php配置文件，这里面是二次开发的公用部分，添加或重写的
服务方面的配置

4.`@app/config/fecshop_local.php`

该配置文件包含：

4.1`@app/config/fecshop_local_modules/*.php`
这个文件夹下面所有的php配置文件，这里面是二次开发的公用部分，添加或重写的
模块方面的配置

4.2`@app/config/fecshop_local_services/*.php`
这个文件夹下面所有的php配置文件，这里面是二次开发的公用部分，添加或重写的
服务方面的配置

一开始说的9个配置文件，以及对应的这些细分的配置文件，共同组合起来合并，形成
fecshop的最终配置。

通过配置项的覆盖，我们就可以重写各个组件，服务等功能，二次开发自己的功能。

配置加速
--------

配置文件的合并是在index.php文件中，
为了加速，您可以把合并后的数组放到缓存中，然后直接读取出来，节省数据合并带来的开销。
如果您更新了配置，您需要刷新一下缓存让更新的配置生效。




