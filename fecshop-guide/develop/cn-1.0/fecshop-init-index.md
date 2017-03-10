Fecshop index.php初始化
=======================

对于入口文件index.php, Fecshop进行了更改，下面是对更改的详细说明。

入口文件代码为：

```
<?php
ini_set('session.cookie_domain', '.fancyecommerce.com');
$homeUrl = 'http://'.$_SERVER['HTTP_HOST'].rtrim(dirname($_SERVER['SCRIPT_NAME']), '\\/');

defined('YII_DEBUG') or define('YII_DEBUG', true);
defined('YII_ENV') or define('YII_ENV', 'dev');

require(__DIR__ . '/../../../vendor/autoload.php');
require(__DIR__ . '/../../../vendor/fancyecommerce/fecshop/yii/Yii.php');

require(__DIR__ . '/../../../common/config/bootstrap.php');

require(__DIR__ . '/../../config/bootstrap.php');

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

$config['homeUrl'] = $homeUrl;

/**
 * 添加fecshop的服务 ，Yii::$service  ,  将services的配置添加到这个对象。
 * 使用方法：Yii::$service->cms->article;
 * 上面的例子就是获取cms服务的子服务article。
 */
new fecshop\services\Application($config['services']);
unset($config['services']);

$application = new yii\web\Application($config);
$application->run();

```

详细分析如下：

index.php初始化

1.`error_reporting(E_ALL || ~E_NOTICE); `

作用：除去 E_NOTICE 之外的所有错误信息


2.`ini_set('session.cookie_domain', '.fancyecommerce.com');` 

这里需要填写您的域名，fecshop是支持多语言store的，各个语言可以用不同的子域名，为了在多个域名之间共享session（购物车，登录信息都是基于session），
在语言进行切换的时候，购物车和登录信息不被丢失，需要做session共享，当然，您也可以在php.ini里面设置该值，不过在这里设置更加灵活

3.`$homeUrl = 'http://'.$_SERVER['HTTP_HOST'].rtrim(dirname($_SERVER['SCRIPT_NAME']), '\\/');`

该代码是为了取到当前的home url，也就是网站的根URL，对于fecshop的多语言，你可以使用www.fecshop.com  es.fecshop.com  fr.fecshop.com这种子域名
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

这个文件的内容如下：

```
<?php
Yii::setAlias('@common', dirname(__DIR__));
Yii::setAlias('@console', dirname(dirname(__DIR__)) . '/console');
Yii::setAlias('@appadmin', dirname(dirname(__DIR__)) . '/appadmin');
Yii::setAlias('@appfront', dirname(dirname(__DIR__)) . '/appfront');
Yii::setAlias('@apphtml5', dirname(dirname(__DIR__)) . '/apphtml5');
Yii::setAlias('@appserver', dirname(dirname(__DIR__)) . '/appserver');
Yii::setAlias('@appapi', dirname(dirname(__DIR__)) . '/appapi');
Yii::setAlias('@appimage', dirname(dirname(__DIR__)) . '/appimage');

Yii::setAlias('@Facebook', dirname(dirname(__DIR__)) . '/vendor/fancyecommerce/fecshop/lib/Facebook');
Yii::setAlias('@google', dirname(dirname(__DIR__)) . '/vendor/fancyecommerce/fecshop/lib/google');

```

主要是添加一些Alias

9.`require(__DIR__ . '/../config/bootstrap.php');`

在appfront/config/bootstrap.php 可以添加当前入口独有的东西

10.

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

上面的代码是将所有的配置文件进行合并，后面的数组配置将覆盖前面的数组配置，譬如：
`require(__DIR__ . '/../config/fecshop_local.php')` 将覆盖`require(__DIR__ . '/../../common/config/fecshop_local.php'),`
里面的数组配置。

另外需要注意的是，上面的有一些配置文件又会包含其他的配置文件，譬如代码：

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

12.

```
$yiiClassMap = require(__DIR__ . '/../config/YiiClassMap.php');
if(is_array($yiiClassMap) && !empty($yiiClassMap)){
	foreach($yiiClassMap as $namespace => $filePath){
		Yii::$classMap[$namespace] = $filePath;
	}
}
```

上面是设置classMap，通过classMap您可以重写任何一个文件，关于classMap的详细，你可以参看文档
http://www.yiichina.com/doc/guide/2.0/concept-autoloading#class-map，
通过classMap可以将namespace进行重定向，譬如

```
<?php
namespace fecshop\services;
use Yii;
use yii\base\InvalidValueException;
use yii\base\InvalidConfigException;
use fec\helpers\CSession;
class Coupon extends Service
{
	
	
	
}
?>
```

我通过
`Yii::$classMap['fecshop\services\Coupon'] = '@appfront/services/Coupon.php';`
当我引入
`use fecshop\services\Coupon`,系统就会执行重定向的这个文件`@appfront/services/Coupon.php`,
而不是`@fecshop/services/Coupon.php`,这就是classMap的作用，当然，也起到加速的作用，不需要php去
查找文件，对于Yii2的几个核心文件，都是添加到了classMap中了。详细参看文件`vendor\yiisoft\yii2\classes.php`,
下面是列出这个文件的部分代码：

```
<?php
return [
  'yii\base\Action' => YII2_PATH . '/base/Action.php',
  'yii\base\ActionEvent' => YII2_PATH . '/base/ActionEvent.php',
  'yii\base\ActionFilter' => YII2_PATH . '/base/ActionFilter.php',
  'yii\base\Application' => YII2_PATH . '/base/Application.php',
  'yii\base\ArrayAccessTrait' => YII2_PATH . '/base/ArrayAccessTrait.php',
  'yii\base\Arrayable' => YII2_PATH . '/base/Arrayable.php',
```




13.

```
new fecshop\services\Application($config['services']);
unset($config['services']);
```

这里是给Yii类添加服务配置，将Yii::$service指向 fecshop\services\Application;
原理类似Yii2的组件（component），譬如使用cms 服务的代码为`Yii::$service->cms`
，使用cms服务的article子服务的get()方法的代码为`Yii::$service->cms->article->get()`

14.

```
$application = new yii\web\Application($config);
$application->run();
```

这里是Yii2的初始化，这里不做详细叙述。

> 本文由 [fecommerce](http://www.getyii.com/member/fecommerce) 创作，采用 [知识共享署名 3.0 中国大陆许可协议](http://creativecommons.org/licenses/by/3.0/cn) 进行许可。
可自由转载、引用，但需署名作者且注明文章出处。