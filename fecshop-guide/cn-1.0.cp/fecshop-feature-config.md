Fecshop 配置层
==============

> Fecshop 的配置，在入口文件index.php被引入，通过
yii2的yii\helpers\ArrayHelper::merge函数，将各个配置合并起来，
代码如下：

```php

<?php
//$secure = isset($_SERVER['HTTPS']) && (strcasecmp($_SERVER['HTTPS'], 'on') === 0 || $_SERVER['HTTPS'] == 1) || isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && strcasecmp($_SERVER['HTTP_X_FORWARDED_PROTO'], 'https') === 0;

$secure = 0;
$http = $secure ? 'https' : 'http';
$homeUrl = $http.'://'.$_SERVER['HTTP_HOST'].rtrim(dirname($_SERVER['SCRIPT_NAME']), '\\/');

defined('YII_DEBUG') or define('YII_DEBUG', true);
defined('YII_ENV') or define('YII_ENV', 'dev');

require(__DIR__ . '/../../vendor/autoload.php');
require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/yii/Yii.php');
require(__DIR__ . '/../../common/config/bootstrap.php');
require(__DIR__ . '/../config/bootstrap.php');

$config = yii\helpers\ArrayHelper::merge(
    require(__DIR__ . '/../../common/config/main.php'),
    require(__DIR__ . '/../../common/config/main-local.php'),
    require(__DIR__ . '/../config/main.php'),
    require(__DIR__ . '/../config/main-local.php'),
	# fecshop base
	require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/config/fecshop.php'),
	# fecshop module base
	require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/app/appfront/config/appfront.php'),
	
	# thrid part confing
	
	# user local config.
	require(__DIR__ . '/../config/fecshop_local.php')
    
);

$config['homeUrl'] = $homeUrl;
# 给予单独的配置文件，用于service配置
# 然后将services下面的$app都改成$service.
# echo Yii::$service->cmstest->article->storage;exit;
# 对于其他的地方都要进行这样的修改才行。

new fecshop\services\Application($config['services']);
unset($config['services']);
//var_dump($config);
$application = new yii\web\Application($config);
$application->run();

```


首先要了解一下 ， yii\helpers\ArrayHelper::merge(),下面通过例子讲解：

```php

$arr1 = [
  'name'   => 'terry',
  'age'  =>  15,
  'friend'=> [
	'zhangsan','lisi'
  ],
  'work' =>[
	'aa'  => 11,
	'bb'  => ['aa','bb'],
  ],
];
$arr2 = [
  'name'   => 'water',
  'age'  =>  22,
  'friend'=> [
	'zhangsan','wangwu'
  ],
  'work' =>[
	'cc'  => ['77','bb'],
	'aa'  => 22,
  ],
];
$arr3 = yii\helpers\ArrayHelper::merge($arr1,$arr2);

```

$arr3的值为：

```

[
	"name"		=> "water" ,
	"age" 		=> 22,
	"friend"	=> [
		"zhangsan","lisi","zhangsan","wangwu"
	],
	"work" 		=> [
		"aa"	=> 22,
		"bb"	=> [
			"aa","bb",
		]
		"cc"	=> [
			"77,"bb"
		],
	],
]

```

- 如果数组存在key，key不是数字，而且key对应的不是数组，那么，
后面的就会覆盖前面的，譬如上面的[[name]],

- 如果数组存在key，key是数字，value值是数组，那么就会合并起来，
需要注意的是，这里不会去掉重复，譬如[[friend]],
$arr1['friend'] = ['zhangsan','lisi'];
$arr2['friend'] = ['zhangsan','wangwu'];

合并后 $arr3['friend'] = ["zhangsan","lisi","zhangsan","wangwu"], 并没有去掉重复。


了解完了ArrayHelper::merge()函数，咋们回去看看入口文件的代码部分:

```php

$config = yii\helpers\ArrayHelper::merge(
    require(__DIR__ . '/../../common/config/main.php'),
    require(__DIR__ . '/../../common/config/main-local.php'),
    require(__DIR__ . '/../config/main.php'),
    require(__DIR__ . '/../config/main-local.php'),
	# fecshop base
	require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/config/fecshop.php'),
	# fecshop module base
	require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/app/appfront/config/appfront.php'),
	
	# thrid part confing
	
	# user local config.
	require(__DIR__ . '/../config/fecshop_local.php')
    
);

```

后面的配置文件，会覆盖前面的配置，但是，一种情况出来，就是
数组的key是数组的时候，也就是上面的 **$arr3['friend']**，
这种情况会合并起来，而不是覆盖，因此，对于一些key为数字的数组是不能覆盖的，

如果存在上面说的，数组的key为数字的情况，尽量放到最后的配置文件中，
或者将key设置成字符串。

对于上面的配置方法，配置是ArrayHelper::merge()是无法删除配置的
，不过可以在后面的文件中覆盖配置，将配置的值设置成空，
然后在后面的逻辑中将是空值的去除，即可 。


介绍完了原理，下面介绍一下详细。

我们知道，fecshop通过很多方式，来解决自身升级和二次开发用户，修改文件造成冲突的问题，
这里的解决就是通过配置文件，在上面的merge()函数中可以看到：

```
require(__DIR__ . '/../config/fecshop_local.php');

```

app/config下面的配置文件的优先级最高，二次开发用户可以在这个文件中重写
fecshop系统的配置, 优先级低于二次开发用户配置和第三方开发用户配置，
下面是fecshop的系统配置：

```
# fecshop base
require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/config/fecshop.php'),
# fecshop module base
require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/app/appfront/config/appfront.php'),

```

因此，第三方开发者可以通过配置的更改，重写fecshop的功能，
同样，二次开发用户可以通过配置的更改，
修改第三方和fecshop系统用户的功能，而不需要改动
第三方和fecshop的系统文件。

**fecshop 系统的服务配置：**

文件路径在@fecshop\app\config\ 下面，@fecshop\app\config\fecshop.php 是主配置，他会
把@fecshop\app\config\services下面的所有配置文件合并起来。
这里主要配置的是 服务组件。用户如果想要重写fecshop的系统服务
可以在@app\config\fecshop_local_services下面进行添加配置，
覆盖fecshop的系统配置

**fecshop 系统的模块配置：**

文件路径在@fecshop\app\appfront(appadmin,or other)\config\下面。
在这个路径下面的appfront.php是主体配置，modules下面的各个模块的详细配置，
二次开发用户可以在@appfront/cofnig/fecshop_local_modules下面
添加模块的配置文件，进行模块的某些功能的重写。


**yii2 系统的重写**

对于yii2，很多底层功能是可以重写的，譬如：@fecshop\yii下面
都是对yii2的一些功能进行的重写，二次开发用户当然可以重写yii2
框架的组件和模块等。

**fecshop 第三方重写**

作为第三方可以通过配置的方式重写fecshop和yii2的功能。









