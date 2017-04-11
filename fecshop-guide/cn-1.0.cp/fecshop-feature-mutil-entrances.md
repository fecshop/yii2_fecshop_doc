Fecshop 多入口
==============

> Fecshop 多入口，指的是可以通过多个入口来访问fecshop，
也就是说，通过多个域名解析到fecshop的多个入口的文件夹，
譬如@appfront/web/index.php，
@appadmin/web/index.php，
@apphtml5/web/index.php，
@appserver/web/index.php，
@appapi/web/index.php，
当然，多个域名可以解析到同一个入口。

### Fecshop多个入口的介绍：

### 1.@appfront/web/index.php

这个入口，作为PC端入口，也就是我们通过电脑访问，
解析到这个入口，如果移动设备（不包括平板），访问，
则跳转到手机web入口 @apphtml5/web/index.php，
对于多语言，一般用多子域名的方式解析到该入口，来实现
前端PC端的多store，进而实现多语言，
该入口对应到fecshop核心代码：@fecshop/app/appfront.

文件夹介绍：

**@appfront\config\**：该文件夹下面的都是配置文件

- 文件:**params-local.php** ，该文件是参数配置，该文件一般是本地配置，
不上传到版本库中，也就是本地开发环境的一些配置，和线上环境不一样的一些配置。

- 文件:**params.php** ，该文件是参数配置，该文件和[[params-local.php]]的不同
在于params.php , 会上传到svn版本库中，和线上保持一致。

- 文件**main-local.php**,该文件是对Yii2的一些系统配置，包括组件和一些参数，
该文件是本地的一些配置，不上传到svn版本库中的，譬如配置redis,本地和线上的密码，库都不一样
需要线上和开发环境单独配置，这些就写入到[[main-local.php]]中

- 文件**main.php**， 和 [[main-local.php]]的不同在于，该
文件会被保存到版本库中。

- 文件**fecshop_local.php**，这是对fecshop进行配置的文件
包括fecshop的服务services，模块modules，以及bootstrap等一些fecshop
系统的配置。本文件，会加载下面的两个文件夹里面的所有配置文件
。

- 文件夹**fecshop_local_modules**，该文件夹下面的所有的文件
都是覆盖或者添加对于fecshop系统模块的配置，进而重写或者添加
一些模块功能

- 文件夹**fecshop_local_services**，该文件夹下面的
所有文件，都是覆盖或者添加对于fecshop系统服务组件的配置。
如果您想要自定义配置一个fecshop的服务组件，可以在这个文件夹
下面添加一个文件，然后填写配置，即可完成覆盖fecshop
的服务配置。
譬如:@appfront/config/fecshop_local_services/Store.php


```php

<?php
   return [
   'store' => [
		'class' => 'fecshop\services\Store',
		'stores' => [
			# store_code ,define by domain and fold.
			# 语言必须在fecshoplang中定义，否则将无法得到语言属性。
			# 在添加store的时候，必须查看 添加的语言在 fecshoplang中是否定义。
			'fecshop.appfront.fancyecommerce.com' => [
				'language' 		=> 'en_US',
				'languageName' 	=> 'English',
				
				//'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'USD',
			],
			'fecshop.appfront.fancyecommerce.com/fr' => [
				'language' 		=> 'fr_FR',
				'languageName' 	=> 'Français',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'RMB',
			],
			'fecshop.appfront.fancyecommerce.com/es' => [
				'language' 		=> 'es_ES',
				'languageName' 	=> 'Español',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'USD',
			],
			'fecshop.appfront.fancyecommerce.com/cn' => [
				'language' 		=> 'zh_CN',
				'languageName' 	=> '中文',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'RMB',
			],
		],
		
	],
			
];

```

通过配置stores，将配置文件当做内容注入到fecshop的服务中。


**@appfront\local_modules\**：本地开发，或者重写的模块，写到这里

**@appfront\languages\**：各个翻译语言文件，里面包括各个语言，
譬如：de_DE, en_US, es_ES , fr_FR, it_IT , nl_NL,
pt_PT, ru_RU,zh_CN。等

**@appfront\theme\**：模板路径。譬如：@appfront\theme\terry\theme01\,
\assets 为js css img文件 ，\layouts为view 布局文件， 其他的为模块view文件。

**@appfront\web\**：index.php为入口文件，assets为js,css,img的
发布文件夹，

### 2.@appadmin/web/index.php 

这个是后台入口文件，一般后台解析到这个文件夹。
该入口对应到fecshop核心代码：@fecshop/app/appadmin.
里面的组织结果和@appfront类似，不过appadmin目前不支持多语言
，仅仅支持中文。appadmin是基于fec_admin扩展而来，
又进行了一些修改，

### 3.@apphtml5/web/index.php

这个是手机web的入口文件，一般用于移动设备浏览器访问的入口（不包括
平板，平板的屏幕比较宽，可以直接访问pc端入口），
该入口对应到fecshop核心代码：@fecshop/app/apphtml5.

### 4.@appserver/web/index.php

这个是手机app端的入口文件，也就是app的api调用，都是从这个入口进入。
该入口对应到fecshop核心代码：@fecshop/app/appserver.

### 5.@appapi/web/index.php，

这个是api的总api，一般是为了和外部系统对接，譬如ERP,营销系统等。
该入口对应到fecshop核心代码：@fecshop/app/appapi.

### Fecshop入口的共同点：

对于Fecsop的各个入口，下面的文件夹：










