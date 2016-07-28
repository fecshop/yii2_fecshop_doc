Fecshop 服务开发
================

> Fecshop服务开发，包括开发新的服务功能，和重写原来的服务

1.扩展新的服务：

对于服务，包括两部分，一个是配置。
也就是类似配置component一样，不过，服务对应的配置为services，
在配置中加入

```
[
	'services' => [
		....
	],
]
```

在里面添加服务即可，如果是本地二次开发，可以
直接在@app/config/fecshop_local_services里面直接
添加一个文件即可，譬如:
@appfront/config/fecshop_local_services/FecshopLang.php
,代码如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
return [
	'fecshoplang' => [
		//'class' => 'fecshop\services\FecshopLang',
		'allLangCode' => [
			'en_US' => 'en',
			'fr_FR' => 'fr',
			'de_DE' => 'de',
			'es_ES' => 'es',
			'ru_RU' => 'ru',
			'pt_PT' => 'pt',
			'zh_CN' => 'zh',
		],
		'defaultLangCode' => 'en',
	],
];
```

通过这面的方式就可以创建一个新的服务了，
如果在fecshop核心代码中存在这个service，那么您
可以通过指定一个同样的名字，譬如上面的[[fecshoplang]],
然后将class写成自己创建的类即可完成重写。

下面您需要创建服务，也就是services
在@app/local_services/下面创建上面配置中的class，
这个class必须继承 fecshop\services\Service,否则无法给
这个服务添加子服务，

**子服务介绍：**

@fecshop\services\Cms 是一个服务，我们可以通过
Yii::$service->cms->xxxx()访问cms服务的属性或者方法。
我们可以给cms服务定义子服务，
首先要配置，譬如cms的配置为：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
return [
	'cms' => [
		'class' => 'fecshop\services\Cms',
		
		# 子服务
		'childService' => [
			'article' => [
				'class' 			=> 'fecshop\services\cms\Article',
				'storage' => 'mysqldb', # mysqldb or mongodb.
			],
		],
	],
];
```

从上面的代码配置中，给cms配置了article子服务。
下面需要创建这个子服务的class：
fecshop\services\cms\Article。

我们使用cms服务的子服务article，可以通过

Yii::$service->cms->article->XXXX() 来调用，
在默认yii2，Yii是没有$service这个变量的，
我们来关心一下Yii::$service这个变量是怎么来的？


**Yii::$service的变量的由来：**



fecshop定义了一个Yii2文件，文件在：vendor/fancyecommerce/fecshop/yii/Yii.php

```
class Yii extends \yii\BaseYii
{
	public static $service;
	
}

```

定义了一个变量，然后在index入口文件中加载的是这个Yii，
index.php的代码如下：

```
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

通过代码：
[[new fecshop\services\Application($config['services']);]]和
[[unset($config['services']);]]， 
将service的配置，加入到fecshop\services\Application，
然后将 new fecshop\services\Application 赋值于Yii::$service 。





















