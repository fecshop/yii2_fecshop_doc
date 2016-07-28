Fecshop Store 服务
=================

> 这是很重要的一个服务，

`@fecshop/services/Store`

配置：

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
				'language' 		=> 'en_US',
				'languageName' 	=> 'English',
				
				//'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'USD',
				'mobile'		=> [ # 当设备满足什么条件的时候，进行跳转。
					'enable'		=> true,
					'condition'		=> ['phone','tablet'],
					'redirectUrl' 	=> 'fecshop.apphtml5.fancyecommerce.com',	
				],
			],
			'fecshop.appfront.fancyecommerce.com/fr' => [
				'language' 		=> 'fr_FR',
				'languageName' 	=> 'Fran?ais',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'RMB',
				'mobile'		=> [
					'enable'			=> true,
					'condition'			=> ['phone'], # phone 代表手机，tablet代表平板。
					'redirectDomain' 	=> 'fecshop.apphtml5.fancyecommerce.com/fr', # 跳转后的url。
				],
			],
			'fecshop.appfront.fancyecommerce.com/es' => [
				'language' 		=> 'es_ES',
				'languageName' 	=> 'Espa?ol',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'USD',
				'mobile'		=> [
					'enable'		=> true,
					'condition'		=> ['tablet'],
					'redirectDomain' 	=> 'fecshop.apphtml5.fancyecommerce.com/es',	
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

上面配置可各个store、的 首页域名key，语言，模板，货币
是否开启移动设备跳转，以及跳转的条件，跳转的域名。

在fecshop的初始化过程中，会调用bootstrap($app)方法

1.遍历上面的配置，查看当前的域名，满足条件的是配置中的·
那个store

2.找到当前域名对应的store后，检查是否满足移动设备跳转要求
如果满足，则跳转

3.如果不满足移动设备跳转，则开始初始化当前store的参数
当前的store，语言，货币，模板等。






























