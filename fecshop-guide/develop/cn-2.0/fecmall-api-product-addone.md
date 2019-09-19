Fecshop Api 产品 AddOne
=========================

> Api描述：根据传递的json数据，新增一行product数据



URL: `http://fecshop.appapi.fancyecommerce.com/v1/product/addone`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称          | 是否必须    |  类型       |  描述     |
| ------------------| -----:      | :----:      |:----:     |
| name              | 必须        |   Array     | 【多语言属性】产品的名字|
| spu               | 必须        |   String    | 产品的spu|
| sku               | 必须        |   String    | 产品的sku|
| weight            | 必须        |   Float     | 产品的重量kg|
| status            | 可选        |   Int       | 产品的状态，1代表激活，2代表关闭，如果不填写默认为激活|
| qty               | 可选        |   Int       | 产品的库存，如果不填写，则代表为0|
| is_in_stock       | 可选        |   Int       | 产品的上架状态，1代表上架，2代表下架，如果不填写，则默认为上架状态|
| category          | 可选        |   Array     | 产品的分类id，该属性是数组属性|
| price             | 必须        |   Float     | 产品的价格|
| special_price     | 可选        |   Float     | 产品的特价|
| special_from      | 可选        |   Date      | 产品的特价开始时间|
| special_to        | 可选        |   Date      | 产品的特价结束时间|
| cost_price        | 可选        |   Float     | 产品的成本价|
| tier_price        | 可选        |   Array     | 产品的批发价，根据加入购物车的产品的数量，设置不同的价格|
| new_product_from  | 可选        |   Date      | 作为新产品的开始时间|
| new_product_to    | 可选        |   Date      | 作为新产品的结束时间|
| short_description | 可选        |   Array     | 【多语言属性】产品的简短描述|
| attr_group        | 必须        |   String    | 产品的属性组|
| remark            | 可选        |   String    | 产品的备注，一般作为后台的一些备注，不用于前台显示的内容|
| custom_option     | 可选        |   Array     | 产品的自定义属性部分，|
| relation_sku      | 可选        |   Array     | 产品的相关产品，该属性是数组属性，数组的每一个item为sku|
| buy_also_buy_sku  | 可选        |   Array     | 买了这个产品的人还买了那些产品，该属性是数组属性，数组的每一个item为sku|
| see_also_see_sku  | 可选        |   Array     | 看了这个产品的人还看了那些产品，该属性是数组属性，数组的每一个item为sku|
| url_key           | 可选        |   String    | 产品对应的url key，如果自定义的url_key存在，系统会添加一块字符串来保证唯一|
| title             | 可选        |   Array     | 【多语言属性】产品 的标题         |
| meta_keywords     | 可选        |   Array     | 【多语言属性】产品 的meta keywords|
| meta_description  | 可选        |   Array     | 【多语言属性】产品 的meta keywords|
| description       | 可选        |   Array     | 【多语言属性】产品的描述|
| image             | 可选        |   Array     | 产品图片，数组属性，您需要把首先，把图片通过ftp上传到 `@appimage/common/media/catalog/product/` 下面，图片里面填写的是在该路径下的相对路径 |



对于多语言属性的`数据结构`和`必填`的详细说明参看： [AppApi多语言属性说明](fecshop-api-mutil-lang.md)

产品属性是一个比较复杂的部分，您在使用api导入产品之前，请必须先了解产品属性的构成
: 

[Fecshop 产品属性](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_product.html)

[关于Fecshop 产品属性的实战讲解](http://www.fecshop.com/topic/379)

[fecshop为什么要用mongodb组件](http://www.fecshop.com/topic/97)

看完上面的资料，您对产品结构的构成就有了一定的了解，下面是产品导入接口的数据示例：



**Request JSON Data(Body Example)：**

```
{
    "name": {
        "name_en": "test computer",
        "name_fr": "",
        "name_de": "",
        "name_es": "",
        "name_ru": "",
        "name_pt": "",
        "name_zh": "测试计算机"
    },
    "spu": "computer001",
    "sku": "computer001-xinghao1-cpu42",
    "weight": 0.3,
    "status": 1,
    "qty": 334,
    "is_in_stock": 1,
    "url_key": "/test-computer-98383376",
    "category": [
        "57beb586f656f275313bf57a"
    ],
    "price": 33,
    "special_price": 32,
    "special_from": "2017-09-09",
    "special_to": "2018-09-09",
    "cost_price": 10,
    "tier_price": [
        {
            "qty": 2,
            "price": 30
        },
        {
            "qty": 4,
            "price": 28
        }
    ],
    "new_product_from": "2017-11-05",
    "new_product_to": "2017-12-05",
    "meta_title": {
        "meta_title_en": "sex sex",
        "meta_title_fr": "",
        "meta_title_de": "",
        "meta_title_es": "",
        "meta_title_ru": "",
        "meta_title_pt": "",
        "meta_title_zh": ""
    },
    "meta_keywords": {
        "meta_keywords_en": "sex xx meta keywords",
        "meta_keywords_fr": "",
        "meta_keywords_de": "",
        "meta_keywords_es": "",
        "meta_keywords_ru": "",
        "meta_keywords_pt": "",
        "meta_keywords_zh": ""
    },
    "meta_description": {
        "meta_description_en": "sex xx meta keywords sex xx meta keywords sex xx meta keywords",
        "meta_description_fr": "",
        "meta_description_de": "",
        "meta_description_es": "",
        "meta_description_ru": "",
        "meta_description_pt": "",
        "meta_description_zh": ""
    },
    "image": {
        "main": {
            "image": "/1/11/111147807271192428.jpg",
            "label": "",
            "sort_order": "",
            "is_thumbnails": "1",
            "is_detail": "1"
        },
        "gallery": [
            {
                "image": "/2/01/20161024170457_13851.jpg",
                "label": "",
                "is_thumbnails": "1",
                "is_detail": "1",
                "sort_order": ""
            },
            {
                "image": "/2/01/20161024170457_21098.jpg",
                "label": "",
                "is_thumbnails": "1",
                "is_detail": "1",
                "sort_order": ""
            },
            {
                "image": "/2/01/20161101155240_26690.jpg",
                "label": "",
                "is_thumbnails": "1",
                "is_detail": "1",
                "sort_order": ""
            },
            {
                "image": "/2/01/20161101155240_56328.jpg",
                "label": "",
                "is_thumbnails": "1",
                "is_detail": "1",
                "sort_order": ""
            },
            {
                "image": "/2/01/20161101155240_94256.jpg",
                "label": "",
                "is_thumbnails": "1",
                "is_detail": "1",
                "sort_order": ""
            }
        ]
    },
    "description": {
        "description_en": "3333",
        "description_fr": "",
        "description_de": "",
        "description_es": "",
        "description_ru": "",
        "description_pt": "",
        "description_zh": ""
    },
    "short_description": {
        "short_description_en": "334343",
        "short_description_fr": "",
        "short_description_de": "",
        "short_description_es": "",
        "short_description_ru": "",
        "short_description_pt": "",
        "short_description_zh": ""
    },
    "remark": "4444",
    "attr_group": "test_group",
    "custom_option": {
        "red-s-s2-s3": {
            "my_color": "red",
            "my_size": "S",
            "my_size2": "S2",
            "my_size3": "S3",
            "sku": "red-s-s2-s3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161024170457_10036.jpg"
        },
        "red-m-s2-s3": {
            "my_color": "red",
            "my_size": "M",
            "my_size2": "S2",
            "my_size3": "S3",
            "sku": "red-m-s2-s3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161024170457_10036.jpg"
        },
        "red-m-m2-s3": {
            "my_color": "red",
            "my_size": "M",
            "my_size2": "M2",
            "my_size3": "S3",
            "sku": "red-m-m2-s3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161024170457_10036.jpg"
        },
        "red-m-m2-m3": {
            "my_color": "red",
            "my_size": "M",
            "my_size2": "M2",
            "my_size3": "M3",
            "sku": "red-m-m2-m3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161024170457_10036.jpg"
        },
        "red-m-m2-l3": {
            "my_color": "red",
            "my_size": "M",
            "my_size2": "M2",
            "my_size3": "L3",
            "sku": "red-m-m2-l3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161024170457_10036.jpg"
        },
        "red-m-l2-l3": {
            "my_color": "red",
            "my_size": "M",
            "my_size2": "L2",
            "my_size3": "L3",
            "sku": "red-m-l2-l3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161024170457_10036.jpg"
        },
        "red-m-l2-s3": {
            "my_color": "red",
            "my_size": "M",
            "my_size2": "L2",
            "my_size3": "S3",
            "sku": "red-m-l2-s3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161024170457_10036.jpg"
        },
        "red-m-l2-m3": {
            "my_color": "red",
            "my_size": "M",
            "my_size2": "L2",
            "my_size3": "M3",
            "sku": "red-m-l2-m3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161024170457_10036.jpg"
        },
        "red-l-l2-m3": {
            "my_color": "red",
            "my_size": "L",
            "my_size2": "L2",
            "my_size3": "M3",
            "sku": "red-l-l2-m3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161024170457_10036.jpg"
        },
        "red-l-m2-m3": {
            "my_color": "red",
            "my_size": "L",
            "my_size2": "M2",
            "my_size3": "M3",
            "sku": "red-l-m2-m3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161024170457_10036.jpg"
        },
        "red-l-m2-l3": {
            "my_color": "red",
            "my_size": "L",
            "my_size2": "M2",
            "my_size3": "L3",
            "sku": "red-l-m2-l3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161024170457_10036.jpg"
        },
        "black-s-s2-s3": {
            "my_color": "black",
            "my_size": "S",
            "my_size2": "S2",
            "my_size3": "S3",
            "sku": "black-s-s2-s3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161101155240_56328.jpg"
        },
        "black-s-l2-s3": {
            "my_color": "black",
            "my_size": "S",
            "my_size2": "L2",
            "my_size3": "S3",
            "sku": "black-s-l2-s3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161101155240_56328.jpg"
        },
        "black-s-xl2-s3": {
            "my_color": "black",
            "my_size": "S",
            "my_size2": "XL2",
            "my_size3": "S3",
            "sku": "black-s-xl2-s3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161101155240_56328.jpg"
        },
        "black-s-s2-l3": {
            "my_color": "black",
            "my_size": "S",
            "my_size2": "S2",
            "my_size3": "L3",
            "sku": "black-s-s2-l3",
            "qty": 9999,
            "price": 0,
            "image": "/2/01/20161101155240_56328.jpg"
        },
        "blue-s-s2-s3": {
            "my_color": "blue",
            "my_size": "S",
            "my_size2": "S2",
            "my_size3": "S3",
            "sku": "blue-s-s2-s3",
            "qty": 9999,
            "price": 5,
            "image": "/2/01/20161101155240_94256.jpg"
        }
    },
    "memory_capacity": {
        "memory_capacity_en": "",
        "memory_capacity_fr": "",
        "memory_capacity_de": "",
        "memory_capacity_es": "",
        "memory_capacity_ru": "",
        "memory_capacity_pt": "",
        "memory_capacity_zh": ""
    },
    "my_remark": "111",
    "my_email": "1111@22.com",
    "my_date": "2016-11-03",
    "style": "Cute",
    "dresses-length": "Mini",
    "pattern-type": "Animal",
    "sleeve-length": "Sleeveless",
    "collar": "Round Neck",
    "relation_sku": "",
    "buy_also_buy_sku": "",
    "see_also_see_sku": ""
}
```

导入示例数据分析：

1.在导入的数据example中，属性组的配置为：`"attr_group": "test_group"` ，
代表产品的属性组是`test_group`,我们到配置文件中可以查看到这个
属性组的配置：

```
'test_group' => [
    'custom_options' => [
        'my_color'      => [
            'dbtype'    => 'String',
            'label'     => 'My Color',
            'name'      => 'color',
            'showAsImg' => true, // 通过图片的方式展示属性。
            'require'   => 1,  // 1代表是必填选项，0代表选填
            'display'   => [
                'type' => 'select',
                'data' => [
                    'red'              => 'red',
                    'white'            => 'white',
                    'black'            => 'black',
                    'blue'             => 'blue',
                    'green'            => 'green',
                    'yellow'           => 'yellow',
                    'gray'             => 'gray',
                    'khaki'            => 'khaki',

                    'ivory'             => 'ivory',
                    'beige'             => 'beige',
                    'orange'            => 'orange',
                    'cyan'              => 'cyan',
                    'leopard'           => 'leopard',
                    'camouflage'        => 'camouflage',

                    'silver'           => 'silver',
                    'pink'             => 'pink',
                    'purple'           => 'purple',
                    'brown'            => 'brown',
                    'golden'           => 'golden',
                    'leopard'          => 'leopard',
                    'multicolor'       => 'multicolor',
                    'white & blue'     => 'White & Blue',
                    'white & black'    => 'White & Black',
                ],
            ],

        ],

        'my_size'      => [
            'dbtype'     => 'String',
            'label'      => 'My Size',
            'name'       => 'size',
            'require'    => 1,
            'showAsImg'  => false,
            'display'    => [
                'type'    => 'select',
                'data'    => [
                    'S'       => 'S',
                    'M'       => 'M',
                    'L'       => 'L',
                    'XL'      => 'XL',
                    'XXL'     => 'XXL',
                    'XXXL'    => 'XXXL',
                ],
            ],

        ],

        'my_size2'      => [
            'dbtype'     => 'String',
            'label'      => 'My Size',
            'name'       => 'size',
            'require'    => 1,
            'showAsImg'  => false,
            'display'    => [
                'type'    => 'select',
                'data'    => [
                    'S2'       => 'S2',
                    'M2'       => 'M2',
                    'L2'       => 'L2',
                    'XL2'      => 'XL2',
                    'XXL2'     => 'XXL2',
                    'XXXL2'    => 'XXXL2',
                ],
            ],

        ],

        'my_size3'      => [
            'dbtype'     => 'String',
            'label'      => 'My Size',
            'name'       => 'size',
            'require'    => 1,
            'showAsImg'  => false,
            'display'    => [
                'type'    => 'select',
                'data'    => [
                    'S3'    => 'S3',
                    'M3'    => 'M3',
                    'L3'    => 'L3',

                ],
            ],

        ],

    ],
    'general_attr' => [
        // 这是input type='text' 的类型
        'my_remark' => [
            'dbtype' => 'String',
            'label'  => '我的备注',
            'name'   => 'my_remark',
            'display'=> [
                'type' => 'inputString',   // 字符串格式的属性
            ],
            'require' => 0,
        ],
        // 这是input type='email' 的类型
        'my_email' => [
            'dbtype'  => 'String',
            'label'   => '我的邮箱',
            'name'    => 'my_email',
            'require' => 0,
            'display' => [
                'type' => 'inputEmail',        // 字符串格式的属性（email格式验证）
            ],
        ],
        // 这是input type='date' 的类型
        'my_date'  => [
            'label'  => '我的日期',
            'name'   => 'my_date',
            'display'=> [
                'type' => 'inputDate',        // 字符串格式的属性（Date格式验证）
            ],
        ],
        // 这是<select> 的类型
        'style'   => [
            'dbtype'     => 'String',
            'label'      => '类型',
            'name'       => 'style',
            'display'    => [
                'type'    => 'select',        // 下拉条选择格式的属性
                'data'    => [
                    'Casual'      => 'Casual',
                    'Cute'        => 'Cute',
                    'Sexy & Club' => 'Sexy & Club',
                    'Bohemian'    => 'Bohemian',
                    'Vintage '    => 'Vintage ',
                    'Brief'       => 'Brief',
                    'Work'        => 'Work',
                    'Novelty'     => 'Novelty',
                ],
            ],
        ],

        'dresses-length'    => [
            'dbtype'     => 'String',
            'label'      => '裙长',
            'name'       => 'dresses-length',
            'display'    => [
                'type'    => 'select',    // 下拉条选择格式的属性
                'data'    => [
                    'Mini'               => 'Mini',
                    'Knee-Length'        => 'Knee-Length',
                    'Mid-Calf'           => 'Mid-Calf',
                    'Ankle-Length'       => 'Ankle-Length',
                    'Floor-Length '      => 'Floor-Length ',

                ],
            ],
        ],

        'pattern-type'    => [
            'dbtype'     => 'String',
            'label'      => '款式',
            'name'       => 'pattern-type',    // 属性名字
            'display'    => [
                'type'    => 'select',    // 下拉条选择格式的属性
                'data'    => [
                    'Animal'           => 'Animal',
                    'Character'        => 'Character',
                    'Floral'           => 'Floral',
                    'Geometric '       => 'Geometric ',
                    'Leopard '         => 'Leopard ',
                    'Letter'           => 'Letter',
                    'Paisley'          => 'Paisley',
                    'Patchwork'        => 'Patchwork',
                    'Polka Dot'        => 'Polka Dot',
                    'Print'            => 'Print',
                    'Striped'          => 'Striped',

                ],
            ],
        ],

        'sleeve-length'    => [
            'dbtype'     => 'String',
            'label'      => '袖长',
            'name'       => 'sleeve-length',
            'display'    => [
                'type'    => 'select',
                'data'    => [
                    'Sleeveless'             => 'Sleeveless',
                    'Short-Sleeves'          => 'Short Sleeves',
                    'Half-Sleeves'           => 'Half Sleeves',
                    '3-4-Length-Sleeves '    => '3/4 Length Sleeves ',
                    'Long-Sleeves '          => 'Long Sleeves ',

                ],
            ],
        ],

        'collar' => [
            'dbtype'     => 'String',
            'label'      => '领口',        // 后台显示的中文名（目前后台只有中文）
            'name'       => 'collar',
            'display'    => [
                'type'    => 'select',
                'data'    => [
                    'Round Neck'          => 'Round Neck',    // 下拉条里面对应的各个可以选择的值。
                    'V-Neck'              => 'V-Neck',
                    'Hooded'              => 'Hooded',
                    'Turn-down-Collar'    => 'Turn-down Collar',

                ],
            ],
            //'require' => 0,
            //'default' => 2,
        ],
    ],
],
```

2.结合导入的数据和`test_group`属性组的配置，我们来看

2.1 下面这些属性虽然没有在接口参数列表中存在，但是在`test_group`属性组的配置
中存在，我们可以在传递数据api中把这些数据导入进去，而且
对于 `['display']['type'] = 'select'`, 这种列举类型的属性，值必须在
属性定义的['display']['data']中存在，否则将会报错

```
"my_remark": "111",
"my_email": "1111@22.com",
"my_date": "2016-11-03",
"style": "Cute",
"dresses-length": "Mini",
"pattern-type": "Animal",
"sleeve-length": "Sleeveless",
"collar": "Round Neck",
```

2.2 对于custom option属性，是淘宝模式的部分，里面设置的每一行是一个sku，
这个需要一定的篇幅来说明，详细参看上面说的文档，这里不做详细的阐述。

3.总之，多了解fecshop的结构和说明，是可以满足您在产品属性上面的需求，
产品数据是一个复杂的部分，细细了解fecshop的产品数据结构的构成，将会对您有很大的帮助。

另外，您可以在mongodb查看后台手动编辑的产品的json数据结构，
将对您了解fecshop的表结构有很大的帮助。

**Response Header 参数:**


| 参数名称                    | 是否必须    |  类型       |  描述     |
| ----------------------------| -----:      | :----:      |:----:     |
| X-Rate-Limit-Limit          | 可选        |   String    | 在开启速度限制后才会存在，同一个时间段所允许的请求的最大数目|
| X-Rate-Limit-Remaining      | 可选        |   String    | 在开启速度限制后才会存在，在当前时间段内剩余的请求的数量|
| X-Rate-Limit-Reset          | 可选        |   String    | 在开启速度限制后才会存在，为了得到最大请求数所等待的秒数|



**Response JSON Data(Body)：**

格式：`json`

| 参数名称        | 是否必须    |  类型       |  描述        |
| ----------------| -----:      | :----:      |:----:        | 
| code            | 必须        |   Number    | 200 代表成功 |
| message         | 必须        |   String    | 执行结果的文字描述信息  |
| data            | 必须        |   Object    | api获取的数据保存到data中  |

**Response JSON Data(Body Example)**：将会返回保存到数据库中的数据最终值

```

{
    "code": 200,
    "message": "add product success",
    "data": {
        "addData": {
            "name": {
                "name_en": "test computer",
                "name_fr": "",
                "name_de": "",
                "name_es": "",
                "name_ru": "",
                "name_pt": "",
                "name_zh": "测试计算机"
            },
            "spu": "computer001",
            "sku": "computer001-xinghao1-cpu42",
            "weight": 0.3,
            "score": 0,
            "status": 1,
            "qty": 334,
            "min_sales_qty": 0,
            "is_in_stock": 1,
            "visibility": null,
            "url_key": "/test-computer-47678459",
            "category": [
                "57beb586f656f275313bf57a"
            ],
            "price": 33,
            "cost_price": 10,
            "special_price": 32,
            "special_from": 1504886400,
            "special_to": 1536508799,
            "tier_price": [
                {
                    "qty": 2,
                    "price": 30
                },
                {
                    "qty": 4,
                    "price": 28
                }
            ],
            "final_price": 32,
            "new_product_from": 1509811200,
            "new_product_to": 1512489599,
            "freeshipping": null,
            "featured": null,
            "upc": null,
            "meta_title": null,
            "meta_keywords": {
                "meta_keywords_en": "sex xx meta keywords",
                "meta_keywords_fr": "",
                "meta_keywords_de": "",
                "meta_keywords_es": "",
                "meta_keywords_ru": "",
                "meta_keywords_pt": "",
                "meta_keywords_zh": ""
            },
            "meta_description": {
                "meta_description_en": "sex xx meta keywords sex xx meta keywords sex xx meta keywords",
                "meta_description_fr": "",
                "meta_description_de": "",
                "meta_description_es": "",
                "meta_description_ru": "",
                "meta_description_pt": "",
                "meta_description_zh": ""
            },
            "image": {
                "main": {
                    "image": "/1/11/111147807271192428.jpg",
                    "label": "",
                    "sort_order": "",
                    "is_thumbnails": 1,
                    "is_detail": 1
                },
                "gallery": [
                    {
                        "image": "/2/01/20161024170457_13851.jpg",
                        "label": "",
                        "is_thumbnails": "1",
                        "is_detail": "1",
                        "sort_order": ""
                    },
                    {
                        "image": "/2/01/20161024170457_21098.jpg",
                        "label": "",
                        "is_thumbnails": "1",
                        "is_detail": "1",
                        "sort_order": ""
                    },
                    {
                        "image": "/2/01/20161101155240_26690.jpg",
                        "label": "",
                        "is_thumbnails": "1",
                        "is_detail": "1",
                        "sort_order": ""
                    },
                    {
                        "image": "/2/01/20161101155240_56328.jpg",
                        "label": "",
                        "is_thumbnails": "1",
                        "is_detail": "1",
                        "sort_order": ""
                    },
                    {
                        "image": "/2/01/20161101155240_94256.jpg",
                        "label": "",
                        "is_thumbnails": "1",
                        "is_detail": "1",
                        "sort_order": ""
                    }
                ]
            },
            "sell_7_count": null,
            "sell_30_count": null,
            "sell_90_count": null,
            "description": {
                "description_en": "3333",
                "description_fr": "",
                "description_de": "",
                "description_es": "",
                "description_ru": "",
                "description_pt": "",
                "description_zh": ""
            },
            "short_description": {
                "short_description_en": "334343",
                "short_description_fr": "",
                "short_description_de": "",
                "short_description_es": "",
                "short_description_ru": "",
                "short_description_pt": "",
                "short_description_zh": ""
            },
            "custom_option": {
                "red-s-s2-s3": {
                    "my_color": "red",
                    "my_size": "S",
                    "my_size2": "S2",
                    "my_size3": "S3",
                    "sku": "red-s-s2-s3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161024170457_10036.jpg"
                },
                "red-m-s2-s3": {
                    "my_color": "red",
                    "my_size": "M",
                    "my_size2": "S2",
                    "my_size3": "S3",
                    "sku": "red-m-s2-s3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161024170457_10036.jpg"
                },
                "red-m-m2-s3": {
                    "my_color": "red",
                    "my_size": "M",
                    "my_size2": "M2",
                    "my_size3": "S3",
                    "sku": "red-m-m2-s3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161024170457_10036.jpg"
                },
                "red-m-m2-m3": {
                    "my_color": "red",
                    "my_size": "M",
                    "my_size2": "M2",
                    "my_size3": "M3",
                    "sku": "red-m-m2-m3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161024170457_10036.jpg"
                },
                "red-m-m2-l3": {
                    "my_color": "red",
                    "my_size": "M",
                    "my_size2": "M2",
                    "my_size3": "L3",
                    "sku": "red-m-m2-l3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161024170457_10036.jpg"
                },
                "red-m-l2-l3": {
                    "my_color": "red",
                    "my_size": "M",
                    "my_size2": "L2",
                    "my_size3": "L3",
                    "sku": "red-m-l2-l3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161024170457_10036.jpg"
                },
                "red-m-l2-s3": {
                    "my_color": "red",
                    "my_size": "M",
                    "my_size2": "L2",
                    "my_size3": "S3",
                    "sku": "red-m-l2-s3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161024170457_10036.jpg"
                },
                "red-m-l2-m3": {
                    "my_color": "red",
                    "my_size": "M",
                    "my_size2": "L2",
                    "my_size3": "M3",
                    "sku": "red-m-l2-m3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161024170457_10036.jpg"
                },
                "red-l-l2-m3": {
                    "my_color": "red",
                    "my_size": "L",
                    "my_size2": "L2",
                    "my_size3": "M3",
                    "sku": "red-l-l2-m3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161024170457_10036.jpg"
                },
                "red-l-m2-m3": {
                    "my_color": "red",
                    "my_size": "L",
                    "my_size2": "M2",
                    "my_size3": "M3",
                    "sku": "red-l-m2-m3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161024170457_10036.jpg"
                },
                "red-l-m2-l3": {
                    "my_color": "red",
                    "my_size": "L",
                    "my_size2": "M2",
                    "my_size3": "L3",
                    "sku": "red-l-m2-l3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161024170457_10036.jpg"
                },
                "black-s-s2-s3": {
                    "my_color": "black",
                    "my_size": "S",
                    "my_size2": "S2",
                    "my_size3": "S3",
                    "sku": "black-s-s2-s3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161101155240_56328.jpg"
                },
                "black-s-l2-s3": {
                    "my_color": "black",
                    "my_size": "S",
                    "my_size2": "L2",
                    "my_size3": "S3",
                    "sku": "black-s-l2-s3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161101155240_56328.jpg"
                },
                "black-s-xl2-s3": {
                    "my_color": "black",
                    "my_size": "S",
                    "my_size2": "XL2",
                    "my_size3": "S3",
                    "sku": "black-s-xl2-s3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161101155240_56328.jpg"
                },
                "black-s-s2-l3": {
                    "my_color": "black",
                    "my_size": "S",
                    "my_size2": "S2",
                    "my_size3": "L3",
                    "sku": "black-s-s2-l3",
                    "qty": 9999,
                    "price": 0,
                    "image": "/2/01/20161101155240_56328.jpg"
                },
                "blue-s-s2-s3": {
                    "my_color": "blue",
                    "my_size": "S",
                    "my_size2": "S2",
                    "my_size3": "S3",
                    "sku": "blue-s-s2-s3",
                    "qty": 9999,
                    "price": 5,
                    "image": "/2/01/20161101155240_94256.jpg"
                }
            },
            "remark": null,
            "created_at": 1511796132,
            "updated_at": 1511796132,
            "created_user_id": 1,
            "attr_group": "test_group",
            "reviw_rate_star_average": null,
            "review_count": null,
            "reviw_rate_star_average_lang": null,
            "review_count_lang": null,
            "favorite_count": null,
            "relation_sku": "",
            "buy_also_buy_sku": "",
            "see_also_see_sku": "",
            "my_remark": "111",
            "my_email": "1111@22.com",
            "my_date": "2016-11-03",
            "style": "Cute",
            "dresses-length": "Mini",
            "pattern-type": "Animal",
            "sleeve-length": "Sleeveless",
            "collar": "Round Neck",
            "id": "5a1c2da4bfb7ae0b615fee53"
        }
    }
}

```
