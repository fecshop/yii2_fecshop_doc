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


结合导入的数据和`test_group`属性组的配置，我们来看

1. 下面这些属性虽然没有在接口参数列表中存在，但是在`test_group`属性组的配置
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


2.总之，多了解fecshop的结构和说明，是可以满足您在产品属性上面的需求，
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
