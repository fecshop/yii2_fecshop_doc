Fecshop 第三方扩展开发
=====================

对于第三方开发模块，需要功能和模块2块。

对于模块，添加配置，然后在入口文件添加相应的配置即可。

```
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

在 # thrid part confing 处，将第三方的配置引入进来。
然后在store中，将theme路径配置进去。
或者在controller中动态设置，动态设置是最好
的方式。

在store中引入第三方模板的例子；

```

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
```




然后用户在所使用的store中，添加模板路径到
thirdThemeDir 的数组中即可。