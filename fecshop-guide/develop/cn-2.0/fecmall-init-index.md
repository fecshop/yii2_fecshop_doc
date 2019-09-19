Fecmall index.php初始化
=======================

对于入口文件index.php, Fecmall进行了更改，下面是对更改的详细说明。

入口文件代码为：

```
<?php
error_reporting(E_ALL & ~E_NOTICE & ~E_COMPILE_WARNING ); //除去 E_NOTICE E_COMPILE_WARNING 之外的所有错误信息
#ini_set('session.cookie_domain', '.fancyecommerce.com'); //初始化域名，
$http = ($_SERVER['SERVER_PORT'] == 443) ? 'https' : 'http';
$homeUrl = $http.'://'.$_SERVER['HTTP_HOST'].rtrim(dirname($_SERVER['SCRIPT_NAME']), '\\/');
/**
 * fecshop 使用合并配置（config）数组进行加速，true 代表打开。
 * 打开配置加速开关前，您需要执行 http://domain/index-merge-config.php 进行生成单文件配置数组。
 * 注意：打开后，当您修改了配置，都需要访问一次上面的链接，重新生成单文件配置数组，否则修改的配置不会生效
 * 建议：本地开发环境关闭，开发环境如果访问量不大，关闭也行，如果访问量大，建议打开
 * 
 */
$use_merge_config_file = false; 
 
defined('YII_DEBUG') or define('YII_DEBUG', true);
defined('YII_ENV') or define('YII_ENV', 'dev');
defined('FEC_APP') or define('FEC_APP', 'appfront');

require(__DIR__ . '/../../vendor/autoload.php');
require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/yii/Yii.php');

$fecmall_common_main_local_config = require(__DIR__ . '/../../common/config/main-local.php');

require(__DIR__ . '/../../common/config/bootstrap.php');

require(__DIR__ . '/../config/bootstrap.php');

if($use_merge_config_file){
	$config = require('../merge_config.php');
}else{
	$config = yii\helpers\ArrayHelper::merge(
		require(__DIR__ . '/../../common/config/main.php'),
		$fecmall_common_main_local_config,
		require(__DIR__ . '/../config/main.php'),
		require(__DIR__ . '/../config/main-local.php'),
        
		# fecshop 公用配置
		require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/config/fecshop.php'),
		# fecshop 入口配置
		require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/app/appfront/config/appfront.php'),
		
		# thrid part confing
        # 第三方 公用配置
        require(__DIR__ . '/../../common/config/fecshop_third.php'),
        # 第三方 入口配置
        require(__DIR__ . '/../config/fecshop_third.php'),
        
		# 本地 公用配置
		require(__DIR__ . '/../../common/config/fecshop_local.php'),
		# 本地 入口配置
		require(__DIR__ . '/../config/fecshop_local.php')
		
	);
}

$config['homeUrl'] = $homeUrl;

/**
 * 添加fecshop的服务 ，Yii::$service  ,  将services的配置添加到这个对象。
 * 使用方法：Yii::$service->cms->article;
 * 上面的例子就是获取cms服务的子服务article。
 */
new fecshop\services\Application($config);

$application = new yii\web\Application($config);
$application->run();


```

详细分析如下：

index.php初始化

1.error_reporting(E_ALL & ~E_NOTICE & ~E_COMPILE_WARNING );

作用：除去 E_NOTICE E_COMPILE_WARNING 之外的所有错误信息


2.`ini_set('session.cookie_domain', '.fancyecommerce.com');` 

如果您的多语言store是以子域名的方式进行区分，譬如`fr.xxx.com`,  `it.xxx.com`,
您想在子域名之间共享购物车session，那么您这里填写 `.xxx.com`
当然，您也可以在php.ini里面设置该值，不过在这里设置更加灵活,
如果您的多语言是后缀的方式，譬如www.xxx.com/fr  , www.xxx.com/it , 则不需要设置，
注释掉即可（默认为注释掉的）

3.`$homeUrl = 'http://'.$_SERVER['HTTP_HOST'].rtrim(dirname($_SERVER['SCRIPT_NAME']), '\\/');`

该代码是为了取到当前的home url，也就是网站的根URL，对于fecmall的多语言，你可以使用www.fecshop.com  es.fecshop.com  fr.fecshop.com这种子域名
作为不同语言的home url， 您也可以使用单域名不同后缀的方式，譬如www.fecshop.com  ， www.fecshop.com/es  , www.fecshop.com/fr
这种方式作为homeUrl,如果使用单域名后缀方式，需要到@app/web下面新建一个es  fr文件夹，@appfront/web/fr 下面有例子。


4.`defined('YII_DEBUG') or define('YII_DEBUG', true);` 

这个是Yii2的代码，是用来确定是否开启debug

5.`defined('YII_ENV') or define('YII_ENV', 'dev');`

这个是Yii2的代码，用来确定环境是dev（开发环境）还是prod（生产环境）

6.`require(__DIR__ . '/../../vendor/autoload.php');`

这个是Yii2的代码

7.`require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/yii/Yii.php');`

这个是fecshop重写的Yii.php，主要的修改就是添加一个类静态变量 `public static $service;`,
该变量作为fecshop service的入口，譬如调用order service的代码为：
`Yii::$service->order`

8.`require(__DIR__ . '/../../common/config/bootstrap.php');`


主要是添加一些Alias，以及加载数据库中的应用插件。

9.`require(__DIR__ . '/../config/bootstrap.php');`

在appfront/config/bootstrap.php 可以添加当前入口独有的东西

10.

```
$config = yii\helpers\ArrayHelper::merge(
		require(__DIR__ . '/../../common/config/main.php'),
		$fecmall_common_main_local_config,
		require(__DIR__ . '/../config/main.php'),
		require(__DIR__ . '/../config/main-local.php'),
        
		# fecshop 公用配置
		require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/config/fecshop.php'),
		# fecshop 入口配置
		require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/app/appfront/config/appfront.php'),
		
		# thrid part confing
        # 第三方 公用配置
        require(__DIR__ . '/../../common/config/fecshop_third.php'),
        # 第三方 入口配置
        require(__DIR__ . '/../config/fecshop_third.php'),
        
		# 本地 公用配置
		require(__DIR__ . '/../../common/config/fecshop_local.php'),
		# 本地 入口配置
		require(__DIR__ . '/../config/fecshop_local.php')
		
	);
```

上面的代码是将所有的配置文件进行合并，后面的数组配置将覆盖前面的数组配置，譬如：
`require(__DIR__ . '/../config/fecshop_local.php')` 将覆盖`require(__DIR__ . '/../../common/config/fecshop_local.php'),`
里面的数组配置。

另外需要注意的是，上面的有一些配置文件又会包含其他的配置文件，譬如代码：
`require(__DIR__ . '/../config/fecshop_local.php')`

```
<?php
# 本文件在app/web/index.php 处引入。

# fecshop的核心模块
$modules = [];
foreach (glob(__DIR__ . '/fecshop_local_modules/*.php') as $filename){
	$modules = array_merge($modules,require($filename));
}
# 服务器组件
$services = [];
foreach (glob(__DIR__ . '/fecshop_local_services/*.php') as $filename){
	$services = array_merge($services,require($filename));
}

    
return [
	'modules'=>$modules,
    'services' => $services,
];
```

将 ./fecshop_local_modules/*.php 下面所有的配置文件都包含进来

配置文件的合并，还是耗费一定时间的，为了性能高效，您可以将config数组缓存起来，
直接从缓存文件或者内存数据库redis中直接读取，加快初始化。

11.`$config['homeUrl'] = $homeUrl;`

设置配置的htmlUrl




13.

```
/**
 * 添加fecshop的服务 ，Yii::$service  ,  将services的配置添加到这个对象。
 * 使用方法：Yii::$service->cms->article;
 * 上面的例子就是获取cms服务的子服务article。
 */
new fecshop\services\Application($config);
```

14.

```
$application = new yii\web\Application($config);
$application->run();
```

这里是Yii2的初始化，这里不做详细叙述。
