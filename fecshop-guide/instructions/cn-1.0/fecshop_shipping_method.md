Fecshop 货运方式
===============

> fecshop shipping method 的配置以及详细的说明


### 重量计算 

> `1.3.2版本`以后添加的`体积重`

1.产品的重量分为`实际重量`和`体积重量`两种。

2.计算运费的`重量` = max(`实际重量`, `体积重量`)，取两种的最大的哪一个作为产品最终重量
，详细参看：http://www.fecshop.com/topic/659

3.`体积重` = `(长(c㎡) * 宽(c㎡) * 高(c㎡) )` / `换算系数`

3.1fecshop默认的换算系数:采用
目前的国际标准值`5000`，如果您想要自己定义，在
`@common/config/fecshop_local_services/Shipping.php` 中更改配置
`volumeWeightCoefficient`的值

3.2后台产品编辑功能，加入了长, 宽, 高, 体积重 4个属性，当您填写`长, 宽, 高`这三个属性后，
产品的体积重，将由上面的公式计算得到，填写到产品表中。

3.3购物车页面，显示产品的体积信息，重量信息，如果您不想显示，可以在模板中手动去除。


### Shipping Method 配置

货运方式的配置文件在 
`@fecshop/common/config/fecshop_local_services/Shipping.php`

内容如下：

```
return [
    'shipping' => [
        // Shipping的运费，是表格的形式录入，shippingCsvDir是存放运费表格的文件路径。
        'shippingCsvDir' => '@common/config/shipping',
        'shippingConfig' => [
            'free_shipping'=> [  // 免运费
                'label'=> 'Free shipping( 7-20 work days)',
                'name' => 'HKBRAM',
                'formula' => '0',  // 这里填写公式，该值代表免邮。
                // 国家限制，当国家限制不满足，则该物流不可用 （如果没有国家限制可以去掉）
                'country' => [  // 这里填写(允许|不允许)使用的国家简码，如果您没有这方面的约束，请去掉，去掉后代表没有任何约束
                    'type' => 'allow',  // allow代表只允许下面的国家使用该shipping，not_allow代表不允许下面国家使用该shipping
                    'code' => [
                        'CN',
                        'US',
                    ]
                ],
                // 重量限制，当重量超出这个范围，该物流将不可用 （如果没有重量限制可以去掉）
                'weight' => [
                    'min' => 0,
                    'max' => 100,
                ],
            ],
            'middle_shipping'=> [  // xxx shipping
                'label'=> 'middle shipping( 6-15 work days)',
                'name' => 'HKBRAM',
                'formula' => '[weight] * 0.5',  // 这里填写公式
                // 对于国家和重量限制，如果没有，则不用填写，如果有，参考上面的样式填写
            ],
            'fast_shipping'=> [
                'label'=> 'Fast Shipping( 5-10 work days)',
                'name' => 'HKDHL',
                'formula' => 'csv', // 请将文件名字的命名写入，譬如： fast_shipping.csv
                'csv_content' => '', // 这个由shipping动态从文件中获取内容
                // 对于国家和重量限制，如果没有，则不用填写，如果有，参考上面的样式填写
            ],
        ],
    ],
];
```

前端显示：

![aaa](images/a44.jpg)

### 1.配置运费

> 在上面配置中，formula 代表运费计算数学公式。

1.1 `formula == 'csv'`

如果是该方式，
代表以`csv`文件的方式配置物流运费，运费的计算就依赖于csv表格的配置，
`shippingCsvDir`配置了表格csv文件存放的路径`@common/config/shipping`。对于运费方式`fast_shipping`
cost填写的是`csv`，那么他的文件路径为`@common/config/shipping/fast_shipping.csv`,
也就是`fast_shipping`与`.csv`拼成文件名字，对于csv方式的详细，参看下面第4部分

1.2 formula 值为其他的时候，则代表数学公式

根据字符串数学公式，计算出来运费




### 2.对国家的限制

2.1通用限制，譬如：

```
'country' => [  // 这里填写(允许|不允许)使用的国家简码，如果您没有这方面的约束，请去掉，去掉后代表没有任何约束
    'type' => 'allow',  // allow代表只允许下面的国家使用该shipping，not_allow代表不允许下面国家使用该shipping
    'code' => [
        'CN',
        'US',
    ]
],
```

`type` ： 类型，可以填写 `allow` 和 `not_allow` ，只能填写其中的一个值
，详细参看上面的注释

2.2csv类型独有限制

对于csv类型的shipping，对于表格里面没有配置的国家和省市，
该shipping method不可用，
在csv表格中 `*`,代表所有，详细查看第四部分，
因此，对于csv类型，除了上面的限制外，还可以在csv表格内部做限制，
也就是在csv表格中，把 `*` `*`部分的去掉，只填写可用的国家和省市，
那么只有填写的这些国家省市有效，其他的国家将会导致该货运方式不可用


### 3.重量限制

```
'weight' => [
    'min' => 0,
    'max' => 100,
],
```

3.1满足上面的重量范围时，则该货运方式有效。

3.2如果不加入这部分配置，则没有重量限制。



### 4.关于csv运费配置文件的说明：

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

譬如国家（country）下面是*，代表所有的国家，第二个*代表该国家
对应所有的省市，第三个*代表所有的zip编号，通过* ，可以先做一个通用的配置，
然后对某些国家做独有的运费设置，如果不这样，世界上几百个国家设置运费列表，麻烦死了，
只设置某些订单量比较大的国家即可。

如果不设置 `*`,那么，只有相应的国家和省市有效，其他国家该shipping method不可用。

第四列为重量，第五列为运费。

譬如第1行的意思为`0.0 - 0.51kg`之间的重量，发送到任意
国家的运费为`29.9`（基础货币值）。

第2行的意思为`0.5100 - 1.0100kg`之间的重量，发送到任意
国家的运费为`31.9000`（基础货币值）。


通过`*`将所有的国家进行了配置，然后，下面就是对某些国家的配置
，譬如第五行，是对AU国家进行的单独配置。

后面就是对DE（德国）国家进行的配置。

通过上面您应该就明白了运费的配置。


























