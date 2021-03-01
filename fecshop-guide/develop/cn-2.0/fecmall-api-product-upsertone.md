Fecshop Api 产品 UpdateOne
=========================

> Api描述：根据传递的id，更新一行product数据


**注意**: 这里的产品更新，需要提交产品的所有内容进行覆盖，是一个save操作，相当于将该id的产品的原来的内容进行替换。

在使用前，多多测试，处理产品数据是一个复杂的事情，多根据自身的情况，多看一下fecmall的代码实现，不满足的自己进行二开。


URL: `http://fecshop.appapi.fancyecommerce.com/v1/product/upsertone`

格式：`json`

方式：`post`：

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称          | 是否必须    |  类型       |  描述     |
| ------------------| -----:      | :----:      |:----:     |
| spu               | 必须        |   String    | 产品的spu|
| sku               | 必须        |   String    | 产品的sku|
| name              | 必须          |   Array     | 【多语言属性】产品的名字|
| weight            | 必须          |   Float     | 产品的重量kg|
| status            | 必须          |   Int       | 产品的状态，1代表激活，2代表关闭，如果不填写默认为激活|
| qty               | 可选        |   Int       | 产品的库存，如果不填写，则代表为0 ，对于新产品，则会直接设置为默认库存，如果是更新产品，该字段无效  |
| is_in_stock       | 必须         |   Int       | 产品的上架状态，1代表上架，2代表下架，如果不填写，则默认为上架状态|
| category          | 可选        |   Array     | 产品的分类id，该属性是数组属性|
| price             | 必须         |   Float     | 产品的价格|
| special_price     | 可选        |   Float     | 产品的特价|
| special_from      | 可选        |   Date      | 产品的特价开始时间|
| special_to        | 可选        |   Date      | 产品的特价结束时间|
| cost_price        | 可选        |   Float     | 产品的成本价|
| tier_price        | 可选        |   Array     | 产品的批发价，根据加入购物车的产品的数量，设置不同的价格|
| new_product_from  | 可选        |   Date      | 作为新产品的开始时间|
| new_product_to    | 可选        |   Date      | 作为新产品的结束时间|
| short_description | 可选        |   Array     | 【多语言属性】产品的简短描述|
| remark            | 可选        |   String    | 产品的备注，一般作为后台的一些备注，不用于前台显示的内容|
| relation_sku      | 可选        |   Array     | 产品的相关产品，该属性是数组属性，数组的每一个item为sku|
| buy_also_buy_sku  | 可选        |   Array     | 买了这个产品的人还买了那些产品，该属性是数组属性，数组的每一个item为sku|
| see_also_see_sku  | 可选        |   Array     | 看了这个产品的人还看了那些产品，该属性是数组属性，数组的每一个item为sku|
| title             | 可选        |   Array     | 【多语言属性】产品 的标题         |
| meta_keywords     | 可选        |   Array     | 【多语言属性】产品 的meta keywords|
| meta_description  | 可选        |   Array     | 【多语言属性】产品 的meta keywords|
| description       | 必须        |   Array     | 【多语言属性】产品的描述|
| image             | 必须        |   Array     | 产品图片，数组属性 |
| url_key           | 可选        |   String    | 产品对应的url key，如果自定义的url_key存在，系统会添加一块字符串来保证唯一|
| attr_group        | 必须        |   String    | 产品的属性组|
| attr_group_info        | 必须        |   String    | 产品的属性组对应的详细|
| package_number        | 必须        |   String    | 打包数 |
| long        | 必须        |   String    | 长 |
| width        | 必须        |   String    | 宽 |
| high        | 必须        |   String    | 高 |






对于多语言属性的`数据结构`和`必填`的详细说明参看： [AppApi多语言属性说明](fecshop-api-mutil-lang.md)


**Request JSON Data(Body Example)：**

```
{
        "id": 165,
        "name": {
            "name_en": "test computerxxxxxx  444444",
            "name_zh": "测试计算999xxxxx99x999999999921机",
            "name_fr": "",
            "name_de": "",
            "name_es": "",
            "name_pt": "",
            "name_ru": "",
            "name_it": ""
        },
        "spu": "sk2001",
        "sku": "fecaaa222121",
        "score": 0,
        "status": 1,
        "qty": 21,
        "min_sales_qty": 0,
        "is_in_stock": 1,
        "url_key": "/test-computerxxxxx",
        "meta_title": {
            "meta_title_en": "",
            "meta_title_zh": "",
            "meta_title_fr": "",
            "meta_title_de": "",
            "meta_title_es": "",
            "meta_title_pt": "",
            "meta_title_ru": "",
            "meta_title_it": ""
        },
        "price": "21.00",
        "cost_price": "10.00",
        "special_price": "32.00",
        "special_from": 2017,
        "special_to": 2018,
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
        "final_price": "21.00",
        "new_product_from": 0,
        "new_product_to": 0,
        "meta_keywords": {
            "meta_keywords_en": "sex xx meta keywords",
            "meta_keywords_zh": "",
            "meta_keywords_fr": "",
            "meta_keywords_de": "",
            "meta_keywords_es": "",
            "meta_keywords_pt": "",
            "meta_keywords_ru": "",
            "meta_keywords_it": ""
        },
        "meta_description": {
            "meta_description_en": "sex xx meta keywords sex xx meta keywords sex xx meta keywords",
            "meta_description_zh": "",
            "meta_description_fr": "",
            "meta_description_de": "",
            "meta_description_es": "",
            "meta_description_pt": "",
            "meta_description_ru": "",
            "meta_description_it": ""
        },
        "image": {
            "gallery": [
                {
                    "image": "/2/01/20160722142719_96573.jpg",
                    "label": "",
                    "sort_order": "",
                    "is_thumbnails": "1",
                    "is_detail": "1"
                }
            ],
            "main": {
                "image": "/2/01/20160722142719_52348.jpg",
                "label": "",
                "sort_order": "",
                "is_thumbnails": "1",
                "is_detail": "1"
            }
        },
        "description": {
            "description_en": "3333",
            "description_zh": "",
            "description_fr": "",
            "description_de": "",
            "description_es": "",
            "description_pt": "",
            "description_ru": "",
            "description_it": ""
        },
        "short_description": {
            "short_description_en": "334343",
            "short_description_zh": "",
            "short_description_fr": "",
            "short_description_de": "",
            "short_description_es": "",
            "short_description_pt": "",
            "short_description_ru": "",
            "short_description_it": ""
        },
        "custom_option": null,
        "remark": "4444",
        "long": 0,
        "width": 0,
        "high": 0,
        "weight": "0.30",
        "volume_weight": "0.00",
        "package_number": 0,
        "favorite_count": null,
        "relation_sku": "",
        "buy_also_buy_sku": "",
        "see_also_see_sku": "",
        "attr_group": "clothes_group",
        "collar": "",
        "sleeve-length": "",
        "pattern-type": "",
        "style": "",
        "dresses-length": "",
        "color": "yellow1",
        "size": "S1",
        "reviw_rate_star_average": null,
        "review_count": null,
        "reviw_rate_star_average_lang": false,
        "review_count_lang": false,
        "reviw_rate_star_info": false,
        "reviw_rate_star_info_lang": false,
        "origin_mongo_id": null,
        "is_deputy": null,
        "brand_id": null
    }

```


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
    "message": "update product success",
    "data": {
        "updateData": {
            "_id": "5a1c2b2abfb7ae0a293ee286",
            "created_at": 1511795498,
            "created_user_id": 1,
            "updated_at": 1511921009,
            "name": {
                "name_en": "test computer  444444",
                "name_fr": "",
                "name_de": "",
                "name_es": "",
                "name_ru": "",
                "name_pt": "",
                "name_zh": "测试计算机"
            },
            "spu": "computer001",
            "sku": "computer001-xinghao1-cpu37",
            "weight": 0.3,
            "score": 0,
            "status": 1,
            "qty": 334,
            "min_sales_qty": 0,
            "is_in_stock": 1,
            "category": [
                "57beb586f656f275313bf57a"
            ],
            "price": 33,
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
            "final_price": 33,
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
                        "sort_order": ""
                    },
                    {
                        "image": "/2/01/20161024170457_21098.jpg",
                        "label": "",
                        "sort_order": ""
                    },
                    {
                        "image": "/2/01/20161101155240_26690.jpg",
                        "label": "",
                        "sort_order": ""
                    },
                    {
                        "image": "/2/01/20161101155240_56328.jpg",
                        "label": "",
                        "sort_order": ""
                    },
                    {
                        "image": "/2/01/20161101155240_94256.jpg",
                        "label": "",
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
            "attr_group": "test_group",
            "relation_sku": "",
            "buy_also_buy_sku": "",
            "see_also_see_sku": "",
            "url_key": "/test-computer-444444",
            "special_price": 32,
            "special_from": "2017-09-09",
            "special_to": "2018-09-09",
            "new_product_from": "2017-11-05",
            "new_product_to": "2017-12-05",
            "remark": "4444"
        }
    }
}

```

