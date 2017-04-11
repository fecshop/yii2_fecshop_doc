Fecshop 安装
=======================


github: https://github.com/fancyecommerce/yii2_fecshop_app_advanced

[![Latest Stable Version](https://poser.pugx.org/fancyecommerce/fecshop-app-advanced/v/stable)](https://packagist.org/packages/fancyecommerce/fecshop-app-advanced) [![Total Downloads](https://poser.pugx.org/fancyecommerce/fecshop-app-advanced/downloads)](https://packagist.org/packages/fancyecommerce/fecshop-app-advanced) [![Latest Unstable Version](https://poser.pugx.org/fancyecommerce/fecshop-app-advanced/v/unstable)](https://packagist.org/packages/fancyecommerce/fecshop-app-advanced)


> 项目已经开始, 正在开发中，框架整理阶段。
> Terry

#### 1.安装 fecshop app advanced

安装这个扩展的首选方式是通过 [composer](http://getcomposer.org/download/).

安装composer

```
curl -sS https://getcomposer.org/installer | php  
mv composer.phar /usr/local/bin/composer 
composer self-update
```

安装fecshop app advanced

```
composer global require "fxp/composer-asset-plugin:~1.1.1"
git clone git@github.com:fancyecommerce/yii2_fecshop_app_advanced.git  fecshop
cd fecsop
composer update
./init

```

init过程中，根据提示选择选项安装文件，如果是开发，就选择develop。

执行完上面，就安装完成了。

#### 2.配置 fecshop app advanced（初始配置）


在`@common/main-local.php`中配置mysql，mongodb，redis


```
'db' => [ 
	'class' => 'yii\db\Connection',
	'dsn' => 'mysql:host=localhost;dbname=fecshop',
	'username' => 'root',
	'password' => '',
	'charset' => 'utf8',
],
'mongodb' => [
	'class' => 'yii\mongodb\Connection',
	# 有账户的配置
	//'dsn' => 'mongodb://username:password@localhost:27017/datebase',
	# 无账户的配置
	'dsn' => 'mongodb://127.0.0.1:27017/fecshop',
	# 复制集
	//'dsn' => 'mongodb://10.10.10.252:10001/erp,mongodb://10.10.10.252:10002/erp,mongodb://10.10.10.252:10004/erp?replicaSet=terry&readPreference=primaryPreferred',
],
'mailer' => [
	'class' => 'yii\swiftmailer\Mailer',
	'viewPath' => '@common/mail',
	// send all mails to a file by default. You have to set
	// 'useFileTransport' to false and configure a transport
	// for the mailer to send real emails.
	'useFileTransport' => true,
],

'redis' => [
	'class' => 'yii\redis\Connection',
	'hostname' => 'localhost',
	'port' => 6379,
	//'password'  => 'dfr12EDFqa',
	
],
```

redis是用来做缓存，注意redis一定要设置密码，
密码一定要长，或者无密码模式，屏蔽掉6379端口，网络上爆出来
redis无密码窃取root权限： [redis root 漏洞](https://help.aliyun.com/knowledge_detail/37447.html)
redis 使用的是yii2_Redis扩展，[Yii2 Redis扩展文档](https://github.com/yiisoft/yii2-redis/blob/master/docs/guide/README.md)


mongodb 也是这样，要么密码方式，要么无密码模式屏蔽端口，
mongodb使用的yii2_Mongdb,[Yii2 Mongodb扩展文档](https://github.com/yiisoft/yii2-mongodb/blob/master/docs/guide/README.md)

mysql这个就不用说了，地球人基本都知道，不知道的去搜索。

对于redis缓存，如果您不想安装，可以使用mongodb来替代。

代码如下：

```
'session' => [
	/**
	 * use mongodb for session.
	 */
	/*
	'class' => 'yii\mongodb\Session',
	'db' => 'mongodb',
	'sessionCollection' => 'session',
	*/
	'class' => 'yii\redis\Session',
	'timeout' => 6000,
],

'cache' => [
	/**
	 * use mongodb for cache.
	 */
	//'class' => 'yii\mongodb\Cache',
	'class' => 'yii\redis\Cache',
	'keyPrefix' => 'console',
],
```




#### 3.通过migrate安装数据库mysql和mongodb 

#### 4.配置store.

下面我们先只配置pc端的appfront
在配置文件`@appfront\config\fecshop_local_services\Store.php`
可以看到如下的代码：

```
<?php
   return [
   'store' => [
		'class' => 'fecshop\services\Store',
		'stores' => [
			# store_code ,define by domain and fold.
			# 语言必须在fecshoplang中定义，否则将无法得到语言属性。
			# 在添加store的时候，必须查看 添加的语言在 fecshoplang中是否定义。
			'fecshop.appfront.fancyecommerce.com' => [
				'language' 		=> 'en_US',  # 语言
				'languageName' 	=> 'English', # 语言名称
				
				//'localThemeDir'	=> '@appfront/theme/terry/theme01', #本地模板路径
				'thirdThemeDir'	=> [],  #第三方模板
				'currency' 		=> 'USD', # 默认货币
				'mobile'		=> [ # 当设备满足什么条件的时候，进行跳转。
					'enable'		=> true,
					'condition'		=> ['phone','tablet'],
					'redirectUrl' 	=> 'fecshop.apphtml5.fancyecommerce.com',	
				],
			],
			'fecshop.appfront.fancyecommerce.com/fr' => [
				'language' 		=> 'fr_FR',
				'languageName' 	=> 'Français',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'RMB',
				'mobile'		=> [
					'enable'			=> true,
					'condition'			=> ['phone'], # phone 代表手机，tablet代表平板。
					'redirectDomain' 	=> 'fecshop.apphtml5.fancyecommerce.com/fr', # 跳转后的url。
				],
			],
			'fecshop.appfront.es.fancyecommerce.com' => [
				'language' 		=> 'es_ES',
				'languageName' 	=> 'Español',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'USD',
				'mobile'		=> [
					'enable'		=> true,
					'condition'		=> ['tablet'],
					'redirectDomain' 	=> 'fecshop.apphtml5.es.fancyecommerce.com',	
				],
			],
			'fecshop.appfront.fancyecommerce.com/cn' => [
				'language' 		=> 'zh_CN',
				'languageName' 	=> '中文',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'RMB',
				'mobile'		=> [
					'enable'		=> false,
					'condition'		=> ['phone','tablet'],
					'redirectDomain' 	=> 'fecshop.apphtml5.fancyecommerce.com/cn',	
				],
			],
		],
		
	],
			
];

```

Fecshop 多store的介绍，请参看文旦：
[Fecshop 多store](fecshop-feature-mutil-stores.md)



`fecshop.appfront.fancyecommerce.com`替换成您的域名

`language`为您的语言，

`languageName`为在相应语言下的写法全称，譬如西班牙语下为`Español`,

`thirdThemeDir` 为第三方模板路径，可以是多个，这个是模板路径数组，

`currency` 为当前的默认货币，

`mobile` 为当设备为什么时候进行跳转，这个只有PC端  appfront 有这个。


#### 5. 设置语言对应：

配置文件为：`@common/config/fecshop_local_services/FecshopLang.php`

```
return [
	'fecshoplang' => [
		
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

`allLangCode`为所有语言的对应二位简码，如果您添加
的store中这里存在没有的语言，那么您需要在这里添加
上去

`defaultLangCode`为默认的语言二位简码。

### 6. 设置图片的路径和url

打开：common\config\fecshop_local_services\Image.php
为各个入口设置图片的base dir 和base domain。

```
'image' => [
	'appbase'	=> [
		'appfront' => [
			'basedir' => '@appimage/appfront',
			'basedomain' => 'http://img.appfront.fancyecommerce.com',
		],
		'apphtml5' => [
			'basedir' => '@appimage/apphtml5',
			'basedomain' => 'http://img.apphtml5.fancyecommerce.com',
		],
		//'appadmin' => [
		//	'basedir' => '@appimage/appadmin',
		//	'basedomain' => 'http://img.appadmin.fancyecommerce.com',
		//],
		'common' => [
			'basedir' => '@appimage/common',
			'basedomain' => 'http://img.fancyecommerce.com',
		],
	],
],
```


#### 7. 配置nginx

```
nginx root 分别指向 

appfront/web(PC端) 
appadmin/web(后台端),
apphtml5/web(手机web端),
appapi/web(API端),
appserver/web(手机app端),
当然，如果您不使用某个入口，可以不设置。

另外，您需要配置一下图片的域名和相应的根路径、
```

#### 8. 访问appfront 和appadmin对应的域名即可。










