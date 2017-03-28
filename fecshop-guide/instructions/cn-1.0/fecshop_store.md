Fecshop Store
=============

> fecshop是支持多store的，store一般是用来构建多语言站点，
> 可以为每一个store指定不同的语言和url结构，设置不同的语言，默认货币,模板等。

### 1.Store的配置：

您可以在`@appfront/config/fecshop_local_services/Store.php`中配置Store

示例代码：

```
'stores' => [	
	# store key：域名去掉http部分，作为key，这个必须这样定义。
	'fecshop.appfront.fancyecommerce.com' => [
		'language' 		=> 'en_US',		# 语言简码需要在@common/config/fecshop_local_services/FecshopLang.php 中定义。
		'languageName' 	=> 'English',	# 语言简码对应的文字名称，将会出现在语言切换列表中显示。
		'localThemeDir'	=> '@appfront/theme/terry/theme01', # 设置当前store对应的模板路径。关于多模板的方面的知识，您可以参看fecshop多模板的知识。
		'thirdThemeDir'	=> [],  # 第三方模板路径，数组，可以多个路径
		'currency' 		=> 'USD', # 当前store的默认货币,这个货币简码，必须在货币配置中配置
		'mobile'		=> [ # 当设备满足什么条件的时候，进行跳转。
			'enable'		=> true,
			'condition'		=> ['phone','tablet'], # phone 代表手机，tablet代表平板
			'redirectUrl' 	=> 'fecshop.apphtml5.fancyecommerce.com',	# 如果是移动设备访问进行域名跳转，这里填写的值为store key
		],
		# 第三方账号登录配置
		'thirdLogin' => [
			# facebook账号登录
			'facebook' =>[       #fb api配置 ，fb可以一个app设置pc和手机web两个域名 
				'facebook_app_id'     => '1849609081926823',
				'facebook_app_secret' => '2e097a6d5a424531770fc05760dd7139',
			],
			# google账号登录
			"google" => [       #谷歌api visit https://code.google.com/apis/console to generate your google api
				'CLIENT_ID'  	 => '380372364773-qdj1seag9bh2n0pgrhcv2r5uoc58ltp3.apps.googleusercontent.com',
				'CLIENT_SECRET'  => 'ei8RaoCDoAlIeh1nHYm0rrwO',
			],
		]
	],
```

需要注意的是您的store key，如果您的首页是
`http://fecshop.appfront.fancyecommerce.com`，那么您的key为
`fecshop.appfront.fancyecommerce.com`
，如果您的首页为
`http://fecshop.appfront.fancyecommerce.com/fr`，那么您的key为
`fecshop.appfront.fancyecommerce.com/fr`

您可以为您的每一个store指定特定的域名，用不同的子域名或用不同的语言路径的
方式，来构建您的多语言的网站。

### 2.多语言站点的构建方式：


#### 1.子域名的方式构建多语言站点，譬如：

`www.fecshop.com`（英文）,`fr.fecshop.com`（法文）  `de.fecshop.com`（德文）

这种方式可以在index.php中设置 `ini_set('session.cookie_domain', '.fancyecommerce.com');`
来进行子域名之间session的共享。

#### 2.url路径的方式构建多语言站点，譬如：

`www.fecshop.com`（英文）,`www.fecshop.com/fr/`（法文）,`www.fecshop.com/de/`（德文）

#### 3.独立多域名方式:

`www.fecshop.com`（英文）,`www.fecshop.fr`（法文）,`www.fancyecommerce.de`（德文）

这种方式，session不能共享，因此购物车和登录信息在切换站点的时候，需要重新
进行登录。

### 3.store 组件 的初始化

在Yii2 bootstrap初始化的时候，都会执行store service的bootstrap方法，进行
Fecshop Store 的初始化，Fecshop Store Services的文件路径为:
`@fecshop/services/Store.php`
, 在这个函数中进行当前store的语言，货币，模板等等各个参数的初始化，
具体详细可以参看这个文件里面的代码。

