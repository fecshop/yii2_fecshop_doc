Fecshop 初始化配置
=======================

在安装[Fecshop安装](fecshop-install.md)完成数据库后，需要配置一下。

#### 1.配置介绍：

1.1公共配置介绍：
配置文件在common\config路径下，文件详细为：
- bootstrap.php 这个是yii2初始化的配置文件，一般设置一些别名Alias。
- params-local.php 这个是参数配置文件，用户可以通过config取出数据使用，
这个文件里面的配置一般是本地配置，不会加入到svn版本控制里面。
- params.php  这个也是参数配置文件，功能和params-local.php一样，唯一的不同
在于这个文件会加入svn版本控制，测试和线上保持一致，这个文件
用来配置一些公用配置（各个app都会用到的配置）
- main-local.php ,这个文件是yii2系统的配置文件，一般是本地的配置部分，是不加入svn的。
在这里用来配置数据库。
- main.php，这个文件也是yii2系统的配置文件，是要加入svn版本控制，测试和线上保持一致的，关于
里面的具体配置语法，可以去参看yii2的教程，这里不做详细叙述。


1.2app入口配置介绍：

配置文件在app\config路径下，文件详细为：

- bootstrap.php 这个是yii2初始化的配置文件，一般设置一些别名Alias。
- params-local.php 这个是参数配置文件，用户可以通过config取出数据使用，
这个文件里面的配置一般是本地配置，不会加入到svn版本控制里面。
- params.php  这个也是参数配置文件，功能和params-local.php一样，唯一的不同
在于这个文件会加入svn版本控制，测试和线上保持一致。
- main-local.php ,这个文件是yii2系统的配置文件，一般是本地的配置部分，是不加入svn的。
- main.php，这个文件也是yii2系统的配置文件，是要加入svn版本控制，测试和线上保持一致的，关于
里面的具体配置语法，可以去参看yii2的教程，这里不做详细叙述。
- fecshop_local.php 这个文件是fecshop的本地配置文件入口，本文件的作用
是加载fecshop_local_modules文件夹 和fecshop_local_services文件夹
里面的配置文件。

- fecshop_local_modules 这个是本地二次开发的模块配置，可以在这个
文件夹下面重写fecshop的模块，也可以加入新的模块，如果您加入一个模块，需要
在这里加入一个php文件，然后加入相应的配置即可。

- fecshop_local_services 这个是本地二次开发的服务组件（services）部分，
您可以在这个文件夹下面加入本地开发的服务配置，或者通过配置重写fecshop的
组件。

------------------------------------------------------

#### 2.配置详细：

2.1 common配置详细：

打开common\config\main-local.php ，配置db，mongodb等组件

**mysql的配置如下：**

```
'db' => [ 
            'class' => 'yii\db\Connection',
            'dsn' => 'mysql:host=localhost;dbname=fecshop',
            'username' => 'root',
            'password' => 'pass123$d',
            'charset' => 'utf8',
        ],
```

对于db组件，对应的是mysql，您需要配置DSN,username，password
dsn中[[localhost]] 代表mysql的ip，如果本地，则为[[localhost]] 
dbname=fecshop代表连接的数据库的名字

[[username]] 为上面 [[dbname]] 对应的用户

[[password]]为 [[username]] 对应的密码

**Mongodb的配置如下:**

```
'mongodb' => [
            'class' => 'yii\mongodb\Connection',
			# 有账户的配置
            //'dsn' => 'mongodb://username:password@localhost:27017/datebase',
			# 无账户的配置
			'dsn' => 'mongodb://127.0.0.1:27017/fecshop',
			# 复制集的配置方式
			//'dsn' => 'mongodb://192.168.0.218:27017/erp,192.168.0.238:27017/erp?replicaSet=rs0&readPreference=primaryPreferred',
	   ],
```
mongodb一般是把端口禁止掉，然后添加内网信任的方式，这样就可以使用
无账号的配置。如果端口没有禁止，可以使用有账号的方式配置。
如果mongodb是复制集，可以使用复制集的配置方式进行配置。




2.2 appadmin配置详细：

**配置redis组件** ，打开appadmin\config\main-local.php,

```
'redis' => [
            'class' => 'yii\redis\Connection',
            'hostname' => 'localhost',
            'port' => 6379,
            'database' => '1',
			# connect redis with unix Stock 
			//'unixSocket' => '/var/run/redis/redis.sock',
			# redis password
			'password'  => 'dfa@#dsfaerfwev@#R$FRE23r12EDFqa',
			
        ],
```

[[hostname]] 为redis的ip

[[port]] 为端口
[[database]] 数据库名字，一般设置为数字，各个app 设置不同的数字
[[password]],如果redis没有配置[[password]]，则不需要填写，如果redis服务的端口被开放，则
需要填写代码，不然会被黑客攻击拿到root密码。
[[unixSocket]],为使用unix连接方式的配置方式，使用 unixSocket连接方式
速度会提高一倍左右，不过使用默认也可以，都是微秒级别的。





2.3 appfront配置详细：

**配置redis组件** ，打开appfront\config\main-local.php,
配置参考2.2步骤


**配置Store** ：打开文件appfront\config\fecshop_local_services\Store.php

```
<?php
   return [
   'store' => [
		'class' => 'fecshop\services\Store',
		'stores' => [
			# store_code ,define by domain and fold.
			'fecshop.appfront.fancyecommerce.com' => [
				'language' 		=> 'en_US',
				'languageName' 		=> 'English',
				'themePackage'	=> 'default',
				'theme'	=> 'default',
				'currency' => 'USD',
			],
			'fecshop.appfront.fancyecommerce.com/fr' => [
				'language' 		=> 'fr_FR',
				'languageName' 		=> 'Français',
				'themePackage'	=> 'default',
				'theme'	=> 'default',
				'currency' => 'RMB',
			],
			'fecshop.appfront.fancyecommerce.com/es' => [
				'language' 		=> 'es_ES',
				'languageName' 		=> 'Español',
				'themePackage'	=> 'default',
				'theme'	=> 'default',
				'currency' => 'USD',
			],
			
		],
		
	],
			
];
```

fecshop.appfront.fancyecommerce.com, fecshop.appfront.fancyecommerce.com/fr
, fecshop.appfront.fancyecommerce.com/es 三个为store，
store的key的规范为store的首页地址去掉http://部分。
譬如：首页地址为 http:://en.example.com ，那么这里的key填写
为en.example.com，如果首页地址为http:://www.example.com/en
那么store的key为www.example.com/en。

依次设置多个store，如果您只有一个store，则将2,3去掉即可。

[[language]]为store的默认语言
[[languageName]]为对应语言的全程
[[themePackage]]为模板包名
[[theme]]为模板名
[[currency]]为默认货币


现在appfront就配置好了。下面的page的配置可以后续修改。

**配置Page** 

**在初始配置中，此部分的配置不是必须，可以先使用默认配置，
后续按照需求更改。**

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
	'page' => [
		'childService' => [
			'theme' => [
				'localThemeDir' 	=> '@appfront/theme/terry/theme01',
				# init by third theme.
				'thirdThemeDir'		=> [],
				# init in @fecshop/app/appName/modules/AppfrontController.php
				# it will be set value in appfront  controller  init, it can not effect if you set value to it.
				#'fecshopThemeDir'	=> '',
			],
			'widget' => [
				'widgetConfig' => [
					
					'head' => [
						#'class' => 'fecshop\app\appfront\modules\Cms\block\widgets\Head',
						# 根据多模板的优先级，依次去模板找查找该文件，直到找到这个文件。
						'view'  => 'widgets/head.php',
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
			
			
			
			
			'currency' => [
				'currencys' => [
					'USD' => [
						'rate' 		=> 1,
						'symbol' 	=> '$',
					],
					'RMB' => [
						'rate' 		=> 6.3,
						'symbol' 	=> '￥',
					],
				],
			],
			
			'menu' => [
				'displayHome' => [
					'enable' => true,
					'display'=> 'Home',
				],
				/**
				 *	custom menu  in the front menu section.
				 */
				'frontCustomMenu' => [
					[
						'name' 		=> 'my custom menu',
						'urlPath'	=> '/my-custom-menu.html',
						'childMenu' => [
							[
								'name' 		=> 'my custom menu 2',
								'urlPath'	=> '/my-custom-menu-2.html',
							],
							[
								'name' 		=> 'my custom menu 2',
								'urlPath'	=> '/my-custom-menu-2.html',
								'childMenu' => [
									[
										'name' 		=> 'my custom menu 2',
										'urlPath'	=> '/my-custom-menu-2.html',
									],
									[
										'name' 		=> 'my custom menu 2',
										'urlPath'	=> '/my-custom-menu-2.html',
									],
								],	
							],
						],	
					],
					[
						'name' 		=> 'my custom menu 2',
						'urlPath'	=> '/my-custom-menu-2.html',
					],
				],
				/**
				 *	custom menu  behind the menu section.
				 */
				'behindCustomMenu' => [
					[
						'name' 		=> 'my behind custom menu',
						'urlPath'	=> '/my-behind-custom-menu.html',
					],
					[
						'name' 		=> 'my behindcustom menu 2',
						'urlPath'	=> '/my-behind-custom-menu-2.html',
					],
				],
			],
			
		],
	],
];
```



theme子服务，设置的是当前的模板地址，第三方模板地址，使用默认配置接口
asset子服务，设置的当前使用到的js和css，如果您不进行模板开发添加新文件，使用默认配置即可
currency子服务，设置可以使用到的货币和汇率。
menu子服务设置自定义菜单





















