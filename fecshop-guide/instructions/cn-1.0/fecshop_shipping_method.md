Fecshop 货运方式
===============

> fecshop

货运方式的配置文件在 

@fecshop/common/config/fecshop_local_services/Shipping.php

内容如下：

```
return [
	'shipping' => [
		# Shipping的运费，是表格的形式录入，shippingCsvDir是存放运费表格的文件路径。
		'shippingCsvDir' => '@common/config/shipping', 
		'shippingConfig'=>[
			'free_shipping'=>[  # 免运费
				'label'=>'Free shipping( 7-20 work days)',
				'name' => 'HKBRAM',
				'cost' => 0,
			],
			'fast_shipping'=>[
				'label'=>'Fast Shipping( 5-10 work days)',
				'name' => 'HKDHL',
				'cost' => 'csv' # 请将文件名字的命名写入 fast_shipping.csv
				
			],
		],
		# 该值必须在上面的配置 $shippingConfig中存在，如果不存在，则返回为空。
		'defaultShippingMethod' => [
			'enable'	=> true, # 如果值为true，那么用户在cart生成的时候，就会填写上默认的货运方式。
			'shipping' => 'fast_shipping',
		],
	]
];
```

![aaa](images/a44.jpg)

1. 配置运费

这里的显示和上面的配置相关，其中cost如果等于0，代表是免运费，
如果不免运费，请填写csv，填写csv后，运费的计算就依赖于csv表格的配置，
`shippingCsvDir`配置了表格csv文件存放的路径`@common/config/shipping`。对于运费方式`fast_shipping`
cost填写的是`csv`，那么他的文件路径为`@common/config/shipping/fast_shipping.csv`,
也就是`fast_shipping`与`.csv`拼成文件名字.

2.设置默认运费

设置默认运费后，在下单页面，默认选择相应的运费方式，需要配置
`defaultShippingMethod`。

3.关于csv运费配置文件的说明：

`shippingCsvDir`: Shipping的运费，是表格的形式录入，`shippingCsvDir`是存放运费表格的文件路径。
对于运费方式fast_shipping，打开表格`@common/config/shipping/fast_shipping.csv`，你会发现下面的数据

```
Country,Region/State,"Zip/Postal Code","Weight (and above)","Shipping Price"
*,*,*,0.0000,29.9000
*,*,*,0.5100,31.9000
*,*,*,1.0100,33.9000
*,*,*,1.5100,35.9000
AU,*,*,0.0000,19.9000
AU,*,*,0.5100,22.9000
AU,*,*,1.0100,25.9000
AU,*,*,1.5100,28.9000
AU,*,*,2.0100,31.9000
DE,*,*,0.0000,119.9000
DE,*,*,0.5100,122.9000
DE,*,*,1.0100,125.9000
DE,*,*,1.5100,128.9000
DE,*,*,2.0100,131.9000
```

`*`：代表所有的意思，

譬如国家（country）下面是*，代表所有的国家，第二个*代表国家
下面所有的省市，第三个*代表所有的zip编号，通过* ，可以先做一个通用的配置，
然后对某些国家做独有的运费设置，如果不这样，世界上几百个国家设置运费列表，麻烦死了，
只设置某些订单量比较大的国家即可。

第四列为重量，第五列为运费。

譬如第1行的意思为`0.0 - 0.51kg`之间的重量，发送到任意
国家的运费为`29.9`（基础货币值）。

第2行的意思为`0.5100 - 1.0100kg`之间的重量，发送到任意
国家的运费为`31.9000`（基础货币值）。


通过`*`将所有的国家进行了配置，然后，下面就是对某些国家的配置
，譬如第五行，是对AU国家进行的单独配置。

后面就是对DE（德国）国家进行的配置。

通过上面您应该就明白了运费的配置。


























