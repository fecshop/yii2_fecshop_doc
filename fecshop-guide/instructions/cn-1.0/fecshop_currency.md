Fecshop 货币  
=============

> fecsop 支持多货币


货币配置
----------

您可以在@common/config/fecshop_local_services/Page.php中进行配置货币。

```
'currency' => [
	'baseCurrecy' => 'USD',  	# 基础货币，后台产品的价格都使用基础货币填写价格值。
	'defaultCurrency' => 'USD', # 默认货币，如果store不设置货币，就使用这个store默认货币
	'currencys' => [
		'USD' => [  			# 货币简码，USD代表美元，这个是国际标准
			'rate' 		=> 1, 	# 汇率  当前货币/基础货币的比值，譬如，人民币/美元 = 7
			'symbol' 	=> '$', #货币符号
		],
		'EUR' => [  			# 欧元
			'rate' 		=> 0.93,# 汇率
			'symbol' 	=> '€',
		],
		//'AUD' => [
		//	'rate' 		=> 1.33,
		//	'symbol' 	=> 'AU$',
		//],
		'GBP' => [  			# 英镑
			'rate' 		=> 0.8,
			'symbol' 	=> '£',
		],
		'CNY' => [  			# 人民币
			'rate' 		=> 6.87,
			'symbol' 	=> '￥',
		],
	],
],
```

设置货币后，在前端的顶部的语言切换选项中，就能看到您添加或者修改的货币配置。

另外在store中设置的货币，必须在此处存在，否则将会报错。
