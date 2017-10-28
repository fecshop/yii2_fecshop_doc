Fecshop 初始配置
================

> 当您手动安装好Linux 和FecShop的代码后，就可以进行配置了。


1、配置 [fecshop](http://www.fecshop.com) app advanced

```
在common/config/main-local.php中配置mysql，mongodb，redis

```


```
<?php
return [
    'components' => [
        'db' => [
            'class' => 'yii\db\Connection',
            'dsn' => 'mysql:host=localhost;dbname=fecshop',  # Fecshop是mysql的数据库名字，您需要到mysql中建立一个数据库
            'username' => 'root',  # mysql的账户
            'password' => '123456', # mysql的密码
            'charset' => 'utf8',
        ],
        'mongodb' => [
            'class' => 'yii\mongodb\Connection',
            # 有账户的配置，username是用户名，password是密码，fecshop是数据库
            //'dsn' => 'mongodb://username:password@localhost:27017/fecshop',
            # 无账户的配置，fecshop是数据库
            'dsn' => 'mongodb://127.0.0.1:27017/fecshop',
            # 复制集 如果您的mongodb是复制集（大站），可以使用下面的复制集的配置方式。
            //'dsn' => 'mongodb://10.10.10.252:10001/fecshop,mongodb://10.10.10.252:10002/fecshop,mongodb://10.10.10.252:10004/fecshop?replicaSet=terry&readPreference=primaryPreferred',
        ],


```

mongodb默认是没有密码的，您可以将mongodb的端口在iptables添加信任和端口封闭即可
保证安全，当然，您也可以配置mongodb的用户名和密码。


4、配置环境

4.1 添加host（这个相当于做一个域名本地指向配置）

打开C:\Windows\System32\drivers\etc\hosts，添加如下代码（如果是其他IP，将
127.0.0.1 替换成其他IP即可。）：

```
127.0.0.1       rock.fecshoptest.com     # rockmongo的域名指向，rockmongo是mongodb的可视化界面，类似于mysql的phpmyadmin
127.0.0.1       my.fecshoptest.com       # mysql的phpmyadmin的域名指向
127.0.0.1       appadmin.fecshoptest.com # 后台域名指向
127.0.0.1       appfront.fecshoptest.com # 前台pc端域名指向
127.0.0.1       appfront.fecshoptest.es  # 前台pc端 es 语言的域名指向
127.0.0.1       apphtml5.fecshoptest.com # 前台html端的域名指向
127.0.0.1       appapi.fecshoptest.com   # api端的域名指向
127.0.0.1       appserver.fecshoptest.com # server端的域名指向
127.0.0.1       img.fecshoptest.com		#appimage/common   图片的域名指向
127.0.0.1       img2.fecshoptest.com	#appimage/appadmin 图片的域名指向
127.0.0.1       img3.fecshoptest.com	#appimage/appfront 图片的域名指向
127.0.0.1       img4.fecshoptest.com	#appimage/apphtml5 图片的域名指向
127.0.0.1       img5.fecshoptest.com	#appimage/appserver图片的域名指向
```


4.2、配置nginx，注意下面的  `**fecshop**` 代表[fecshop](http://www.fecshop.com)的相对根目录的文件路径，
请根据自己安装的文件路径填写。

```
appfront.fecshoptest.com appfront.fecshoptest.es 指向 **fecshop**/appfront/web 
 
appadmin.fecshoptest.com 指向 **fecshop**/appadmin/web

apphtml5.fecshoptest.com 指向 **fecshop**/apphtml5/web

appapi.fecshoptest.com 	 指向 **fecshop**/appapi/web

appserver.fecshoptest.com 指向 **fecshop**/appserver/web

img.fecshoptest.com 	指向 **fecshop**/appimage/common

img2.fecshoptest.com 	指向 **fecshop**/appimage/appadmin

img3.fecshoptest.com 	指向 **fecshop**/appimage/appfront

img4.fecshoptest.com 	指向 **fecshop**/appimage/apphtml5

img5.fecshoptest.com 	指向 **fecshop**/appimage/appserver

```

5、配置语言（可以先使用默认）：


在配置文件（：`@common\config\fecshop_local_services\FecshopLang.php`



6、配置货币（可以先使用默认）：


在文件：`@common\config\fecshop_local_services\Page.php`


**注意：**

`@`是Yii2框架的一个语法，是一个`namespaces`的名字，
在后面的文档中会多次出现。

`@app` : 指的是入口代称，这个也是Yii2中使用的代称，指的是执行入口，譬如：
pc端入口为 @appfront，也就是根目录的appfront文件夹，
wap端入口为 @apphtml5， 也就是根目录的apphtml5文件夹。


`@fecshop` 指的是  vendor/fancyecommerce/fecshop 文件夹路径

`@fec` 指的是 vendor/fancyecommerce/fec 文件夹路径

`@fecadmin` 指的是 vendor/fancyecommerce/fec_admin 文件夹路径

`appadmin`,`appfront`,`appapi`,`apphtml5`,`appimage`,`appserver`,
`common`,`console`, 指的都是根目录下面的文件夹。


7、配置store的域名，您可以和我下面的示例代码一致，

**注意** 这个是针对前台访问入口的，也就是`appfront(pc)` `apphtml5(wap)` `appserver(app)`
几个入口的，对于`console`  `appadmin` 是不需要配置`Store.php` 的，因为后台是没有多store的概念的

store在配置文件：`@app\config\fecshop_local_services\Store.php`

对于初次配置，您可以只配置 @appfront 对于其他app入口，可以先不配置。

譬如我的代码(您可以和我的保持一致，相应域名已经在上面添加host)：

```
<?php
   return [
   'store' => [
		'class' => 'fecshop\services\Store',
		'stores' => [
			# 数据的key就是域名
			'appfront.fecshoptest.com' => [
				'language' 		=> 'en_US',   # 语言必须在上面第五步的fecshoplang中定义，否则将无法得到语言属性。
				'languageName' 	=> 'English', # 在添加store的时候，必须查看 添加的语言在 fecshoplang中是否定义。
				# 定义本地模板路径，用来重写fecshop的模板，或者开发新的模板文件。
				//'localThemeDir'	=> '@appfront/theme/terry/theme01',
				# 定义第三方模板路径，用来重写fecshop的模板，或者开发新的模板文件。
				'thirdThemeDir'	=> [],
				# 当前语言的默认货币，货币必须在上面第六步的配置中存在
				'currency' 		=> 'USD',
				'mobile'		=> [ # 当设备满足什么条件的时候，进行跳转。
					'enable'		=> true,
					'condition'		=> ['phone','tablet'], # phone 代表手机，tablet代表平板
					'redirectUrl' 	=> 'apphtml5.fecshoptest.com',	# 如果是移动设备访问进行域名跳转
				],
				# 第三方账号登录配置
				'thirdLogin' => [
					'facebook' =>[                       #fb api配置 ，fb可以一个app设置pc和手机两个域名 
						'facebook_app_id'     => '184963',
						'facebook_app_secret' => '2e097dd7139',
					],
					"google" => [                       #谷歌api visit https://code.google.com/apis/console to generate your google api
						'CLIENT_ID'  	 => '38037grhccontent.com',
						'CLIENT_SECRET'  => 'ei8RaoCHYm0rrwO',
					],
				]

				//'image'	=> [
				//	'domain' => 'img.appfront.fancyecommerce.com',
				//	'baseDir'=> '@appimage/appfront',
				//]
			],
			'appfront.fecshoptest.com/fr' => [
				'language' 		=> 'fr_FR',
				'languageName' 	=> 'Fran?ais',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'RMB',
				'mobile'		=> [
					'enable'			=> true,
					'condition'			=> ['phone'], # phone 代表手机，tablet代表平板。
					'redirectDomain' 	=> 'apphtml5.fecshoptest.com/fr', # 跳转后的url。
				],
			],
			'appfront.fecshoptest.es' => [
				'language' 		=> 'es_ES',
				'languageName' 	=> 'Espa?ol',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'USD',
				'mobile'		=> [
					'enable'		=> true,
					'condition'		=> ['tablet'],
					'redirectDomain' 	=> 'fecshop.apphtml5.es.fancyecommerce.com',	
				],
			],
			'appfront.fecshoptest.com/cn' => [
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

各个代码的具体含义，在注释中已经说明。

第三方登录：facebook和google登录，（** 初始配置，可以先不管这个，后面在说**）如何获取
CLIENT_ID，CLIENT_SECRET可以参看我的博文：
[ facebook login 申请 app_id 和 app_secret](http://blog.csdn.net/terry_water/article/details/55095721) ，
[ google login api 申请 CLIENT_SECRET 和 CLIENT_SECRET](http://blog.csdn.net/terry_water/article/details/55095209)

如果您的各个语言使用了子域名（譬如cn.fecshop.com , fr.fecshop.com 等），由于子域名之间session默认是不能共享的，为了更好的共享session，让语言切换后，
购物车和登录信息存在，您需要在入口文件index.php里面设置`session.cookie_domain`
，大约在`@app/web/index.php`第3行找到代码

```
#ini_set('session.cookie_domain', '.fancyecommerce.com'); //初始化域名，
```

将前面的注释去掉，将`.fancyecommerce.com`替换成您的域名,
如果您使用的是 `www.fecshop.com/cn` , `www.fecshop.com/fr`,
这种方式，则不需要设置 `session.cookie_domain`,
如果您想使用后缀模式区分多语言，譬如添加it语言，您需要到@app/web中添加一个文件夹it，
然后在文件夹里面新建@app/web/it/index.php文件，并新建文件夹@app/web/it/assets，并设置可写,
目前[fecshop](http://www.fecshop.com)只添加了cn和fr两个例子，你可以参考这两个。

8、图片域名配置文件：`@common\config\fecshop_local_services\Image.php`
,譬如我的代码(您可以和我的保持一致，相应域名已经在上面添加host)：

```
<?php
/**
 * FecShop file.
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
return [
	'image' => [
		'appbase'	=> [
			'appfront' => [
				'basedir' => '@appimage/appfront',
				'basedomain' => 'http://img3.fecshoptest.com',
			],
			'apphtml5' => [
				'basedir' => '@appimage/apphtml5',
				'basedomain' => 'http://img2.fecshoptest.com',
			],
			'appadmin' => [
				'basedir' => '@appimage/appadmin',
				'basedomain' => 'http://img2.fecshoptest.com',
			],
			'common' => [
				'basedir' => '@appimage/common',
				'basedomain' => 'http://img.fecshoptest.com',
			],
		],
	],
];
```

您可能会问，为什么要给图片配置域名，图片和网站使用一个域名不就可以吗？
原因：浏览器加载页面的时候，每一个域名加载的链接的并发个数是有限制的，把
图片使用不同的域名，可以让图片独立加载，加快页面的加载。
更多的信息参看[网站的图片，css，js 为什么要和网站的域名不一样](http://www.fancyecommerce.com/2017/04/17/%E7%BD%91%E7%AB%99%E7%9A%84%E5%9B%BE%E7%89%87%EF%BC%8Ccss%EF%BC%8Cjs-%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E5%92%8C%E7%BD%91%E7%AB%99%E7%9A%84%E5%9F%9F%E5%90%8D%E4%B8%8D%E4%B8%80%E6%A0%B7/)


9、配置是否强制复制assets到web目录，如果是开发环境，按照下面进行配置（可选配置，可以先不管这个）。

`@app/config/main.php`里面可以看到下面的配置


这个是yii2的知识范畴

```
'assetManager' => [
	'forceCopy' => true,
],
```

如果是线上， 将forceCopy设置成false `['forceCopy' => false]`

原因：本地开发经常修改css，因此，每次就需要yii的asset将css发布到web路径下面（这里的发布，就是yii2在初始化的时候就会强制把需要的css复制到
web/assets路径下面，譬如yii2封装的bootstrap前端框架），
如果是线上环境，这样非常耗费资源，因此，线上关闭即可，如果您发布了新的css文件，
那么您需要手动清空@app/web/assets下面的文件夹（如果线上访问量不大，开启也无所谓，呵呵。）。

10、导入数据库表(migrate)，在fecshop根目录执行下面的命令行

10.1、Yii2 migratge方式导入表。

mysql(导入mysql的表，数据，索引):

```
./yii migrate --interactive=0 --migrationPath=@fecshop/migrations/mysqldb
```

mongodb(导入mongodb的表，数据，索引):

```
./yii mongodb-migrate  --interactive=0 --migrationPath=@fecshop/migrations/mongodb
```

如果Mongodb migrate报错：`PHP Compile Error 'yii\base\ErrorException' with message 'require_once(): Failed opening required 'Array/m170228_072455_fecshop_tables.php' (include_path='.:')'`
可以参看这里解决：http://www.fecshop.com/topic/45

10.2、测试数据安装：

测试数据下载地址为：[测试mongodb数据库js数据](https://pan.baidu.com/s/1kVwRD2Z) ， 
进入后下载文件夹：[fecshop](http://www.fecshop.com)数据测试包 ，这个文件夹里面所有的文件。

10.2.1、导入mongodb测试数据

上面下载的文件夹中的文件`mongo-fecshop_test-20170419-065157.js`上传到您的系统中，譬如，我放到了该路径下:/www/restore/mongo-fecshop_test-20170419-065157.js

```
mongo 127.0.0.1:27017/fecshop --quiet /www/restore/mongo-fecshop_test-20170419-065157.js
```

`127.0.0.1:27017/fecshop`  27017为mongodb的默认端口，fecshop为数据库.

执行上面的命令，会把数据导入到mongodb的[fecshop](http://www.fecshop.com)数据库中。

> 对于导出，可以直接用rockmongo的库导出功能直接导出js文件。

10.2.2、导入mysql测试数据（产品库存在mysql中）

把`mysql_fecshop.sql` 导入到mysql中，导入mysql，这个大家都知道，这个就不说了。可以用phpmyadmin导入。

10.2.3、产品图片

对于产品的示例数据 对应的图片文件比较大，没有放到版本库里面，你可以到百度云盘下载`appimage.zip`，下载地址为：`https://pan.baidu.com/s/1kVwRD2Z`
将appimage覆盖到根目录即可，覆盖后，
设置一下文件可写可读：

```
chmod 777 -R  appimage
```

如果发现产品图片没有出来，那么您需要清空 `appimage/common/media/catalog/product/cache/*`下面所有文件和文件夹，

```
cd appimage/common/media/catalog/product/cache/
pwd
rm -rf ./*
```

上面使用了**rm -rf命令，一定要谨慎**，pwd看看是否进入了相关文件夹，看好文件路径是否正确，在执行删除，以免造成删除
了其他文件。

清空浏览器图片缓存，重新刷新页面即可。


10.3产品搜索

对于产品搜索，中文搜索需要安装xunSearch，英文用的是mongodb 的 full text search，
[xunSearch安装教程](http://www.fancyecommerce.com/2016/09/24/xunsearch-安装，使用/)
,安装完成后，需要跑脚本同步到搜索工具中，命令行如下：

```
cd vendor/fancyecommerce/fecshop/shell/search
sh fullSearchSync.sh
```

[Fecshop搜索详细文档](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_search.html#)
 

11、开启nginx  mysql  mongodb  php，你就可以访问本地配置的fecshop了。


12、后台的账户密码为： admin  admin123（如果不对，就是123456）

13、如果是线上，需要开启一些脚本。

详细参看：[Fecshop 脚本介绍](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_cron_script.html)
这个里面有一个测试环境也要跑的脚本：`@fecshop/shell/fullSearchSync.sh` ,
这个脚本是将产品数据复制到搜索工具中，否则将无法进行搜索工作。


二：其他

1.开启单文件配置（非必要）

[fecshop](http://www.fecshop.com)的配置最终是由N个配置php文件合并而成，在每次初始化
前执行，为了加速，可以先把配置文件合并成单文件，然后在加载
就会比较节省资源。

入口文件@app/web/index.php 代码： `$use_merge_config_file = false;` 处设置。
[fecshop](http://www.fecshop.com)使用合并配置（config）数组进行加速，true 代表打开。
打开配置加速开关前，您需要执行 http://www.domain.com/index-merge-config.php 进行生成单文件配置数组。
注意：打开后，当您修改了配置，都需要重新生成单文件配置数组，否则修改的配置不会生效,
建议：本地开发环境关闭，开发环境如果访问量不大，关闭也行，如果访问量大，建议打开

参考资料：[yii2 配置加速 – N个配置文件生成一个配置文件](http://www.fancyecommerce.com/2017/04/10/yii2-%E9%85%8D%E7%BD%AE%E5%8A%A0%E9%80%9F-n%E4%B8%AA%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E7%94%9F%E6%88%90%E4%B8%80%E4%B8%AA%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6/)


2.上线注意的问题

对于上线，您需要做一些线上的配置，这些可以参看[上线前的配置](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_online_config.html)


