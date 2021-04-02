Fecmall Api ShopFw-产品新增
=================


> Api描述：根据传递的json数据，新增一行product数据, 该api是专门给shopfw采集工具使用的。



URL: `http://fecshop.appapi.fancyecommerce.com/v1/product/shopfwaddone`

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
| weight            | 必须        |   Float     | 产品的重量kg|
| spu            | 可选        |   String     | spu编号，如果不填写，则由程序生成|
| sku            | 可选        |   String     | sku编号，如果不填写，则由程序生成|
| status            | 可选        |   Int       | 产品的状态，1代表激活，2代表关闭，如果不填写默认为激活|
| qty               | 可选        |   Int       | 产品的库存，如果不填写，则代表为0|
| is_in_stock       | 可选        |   Int       | 产品的上架状态，1代表上架，2代表下架，如果不填写，则默认为上架状态|
| brand_id             | 可选        |   int     | 产品品牌的id |
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
| url_key           | 可选        |   String    | 产品对应的url key，如果自定义的url_key存在，系统会添加一块字符串来保证唯一|
| title             | 可选        |   Array     | 【多语言属性】产品 的标题         |
| meta_keywords     | 可选        |   Array     | 【多语言属性】产品 的meta keywords|
| meta_description  | 可选        |   Array     | 【多语言属性】产品 的meta keywords|
| description       | 可选        |   Array     | 【多语言属性】产品的描述|
| image             | 可选        |   Array     | 产品图片，数组属性，您需要先使用api：[Fecmall Api 产品图片同步](fecmall-api-product-image-sync.md), 然后将api返回的图片相对路径填写上去 |
| third_refer_url       | 必须        |   string     | 对应的第三方平台的url，一般采集的产品数据对应的外部来源url |
| third_refer_code       |    必须     |   string     | 对应的第三方平台的产品外部编码 |
| third_product_code       | 可选        |   string     | 货号（采集的第三方平台的货号） |
| attr_group_normal       | 可选        |   Array     | 属性组对应的普通属性 |
| attr_group_custom       | 可选        |   Array     | 属性组对应的规格属性 |

对于多语言属性的`数据结构`和`必填`的详细说明参看： [AppApi多语言属性说明](fecshop-api-mutil-lang.md)

产品导入接口的数据示例：



**Request JSON Data(Body Example)：**

```
{
"products":[
    {
        "name": {
            "name_en": "test computer1111",
            "name_fr": "",
            "name_de": "",
            "name_es": "",
            "name_ru": "",
            "name_pt": "",
            "name_zh": "测试计算机"
        },
        "spu":"dddddddddddddddddddd",
        "sku":"dddddddddddddddd1",
        "weight": 0.3,
        "status": 1,
        "qty": 334,
        "is_in_stock": 1,
        "brand_id":114,
        "category": [
            1,2,3
        ],
        "price": 33,
        "special_price": 32,
        "special_from": "2017-09-09",
        "special_to": "2022-09-09",
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
                "image": "/f/yf/fyfvari26ef8m241612879330.jpg",
                "label": "",
                "sort_order": "",
                "is_thumbnails": "1",
                "is_detail": "1"
            },
            "gallery": [
                {
                    "image": "/8/oq/8oqxe7gax8wt6qd1612879344.jpg",
                    "label": "",
                    "is_thumbnails": "1",
                    "is_detail": "1",
                    "sort_order": ""
                },
                {
                    "image": "/1/c3/1c3jrvnmbiaqjoj1612879357.jpg",
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
        "third_refer_url": "http://www.taobao.com/xxxxx",
        "third_refer_code": "xxxxxxxxxx1",
        "third_product_code": "yyyyyyyyy1",
        "attr_group": "clothes_group",
        "attr_group_normal":{
            "remark": "4444",
            "memory_capacity": {
                "memory_capacity_en": "",
                "memory_capacity_fr": "",
                "memory_capacity_de": "",
                "memory_capacity_es": "",
                "memory_capacity_ru": "",
                "memory_capacity_pt": "",
                "memory_capacity_zh": ""
            }
        },
        "attr_group_custom":{
            "color": "Red",
            "size": "L"
        }
        
    },
    {
        "name": {
            "name_en": "test computer1111",
            "name_fr": "",
            "name_de": "",
            "name_es": "",
            "name_ru": "",
            "name_pt": "",
            "name_zh": "测试计算机"
        },
        
        "spu":"dddddddddddddddddddd",
        "sku":"dddddddddddddddd2",
        "weight": 0.3,
        "status": 1,
        "qty": 34,
        "is_in_stock": 1,
        "brand_id":114,
        "category": [
            1,2,3
        ],
        "price": 31.2,
        "special_price": 32,
        "special_from": "2017-09-09",
        "special_to": "2022-09-09",
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
                "image": "/f/yf/fyfvari26ef8m241612879330.jpg",
                "label": "",
                "sort_order": "",
                "is_thumbnails": "1",
                "is_detail": "1"
            },
            "gallery": [
                {
                    "image": "/8/oq/8oqxe7gax8wt6qd1612879344.jpg",
                    "label": "",
                    "is_thumbnails": "1",
                    "is_detail": "1",
                    "sort_order": ""
                },
                {
                    "image": "/1/c3/1c3jrvnmbiaqjoj1612879357.jpg",
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
        "third_refer_url": "http://www.taobao.com/xxxxx",
        "third_refer_code": "xxxxxxxxxx1",
        "third_product_code": "yyyyyyyyy1",
        "attr_group": "clothes_group",
        "attr_group_normal":{
            "remark": "4444",
            "memory_capacity": {
                "memory_capacity_en": "",
                "memory_capacity_fr": "",
                "memory_capacity_de": "",
                "memory_capacity_es": "",
                "memory_capacity_ru": "",
                "memory_capacity_pt": "",
                "memory_capacity_zh": ""
            }
        },
        "attr_group_custom":{
            "color": "Blue",
            "size": "L"
        }
    },
    {
        "name": {
            "name_en": "test computer1111",
            "name_fr": "",
            "name_de": "",
            "name_es": "",
            "name_ru": "",
            "name_pt": "",
            "name_zh": "测试计算机"
        },
        
        "spu":"dddddddddddddddddddd",
        "sku":"dddddddddddddddd3",
        "weight": 0.3,
        "status": 1,
        "qty": 334,
        "is_in_stock": 1,
        "brand_id":114,
        "category": [
            1,2,3
        ],
        "price": 33.2,
        "special_price": 32,
        "special_from": "2017-09-09",
        "special_to": "2022-09-09",
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
                "image": "/f/yf/fyfvari26ef8m241612879330.jpg",
                "label": "",
                "sort_order": "",
                "is_thumbnails": "1",
                "is_detail": "1"
            },
            "gallery": [
                {
                    "image": "/8/oq/8oqxe7gax8wt6qd1612879344.jpg",
                    "label": "",
                    "is_thumbnails": "1",
                    "is_detail": "1",
                    "sort_order": ""
                },
                {
                    "image": "/1/c3/1c3jrvnmbiaqjoj1612879357.jpg",
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
        "third_refer_url": "http://www.taobao.com/xxxxx",
        "third_refer_code": "xxxxxxxxxx1",
        "third_product_code": "yyyyyyyyy1",
        "attr_group": "clothes_group",
        "attr_group_normal":{
            "remark": "4444",
            "memory_capacity": {
                "memory_capacity_en": "",
                "memory_capacity_fr": "",
                "memory_capacity_de": "",
                "memory_capacity_es": "",
                "memory_capacity_ru": "",
                "memory_capacity_pt": "",
                "memory_capacity_zh": ""
            }
        },
        "attr_group_custom":{
            "color": "Red",
            "size": "M"
        }
    }
]}
```

数据格式说明：

1.产品图片部分说明

`image.main`  这个是产品的主图

`image.gallery` 这个是产品的详细图

对于图片的各个item，详细说明如下：

```
"image": "/1/11/111147807271192428.jpg",    // 【必填】图片的相对路径
"label": "",         // 【选填】图片的文字描述
"sort_order": "",   // 【选填】 图片的排序
"is_thumbnails": "1",  // 【必填】是否是橱窗图，1代表是，2代表不是   （橱窗图，代表是商城产品详情页，在顶部显示的产品图片）
"is_detail": "1"  // 【必填】是否是详情图，1代表是，2代表不是 （橱窗图，代表是商城产品详情页，在描述里面显示的图片。）

```

2.产品属性组里面的产品属性


对于产品属性组里面的产品属性，在上面的数据格式中没有说明，您在request post数组中添加即可，
譬如：xx属性组的属性如下

```
"style": "Cute",
"dresses-length": "Mini",
"pattern-type": "Animal",
"sleeve-length": "Sleeveless",
"collar": "Round Neck",
```
直接插入到Request JSON Data里面即可。


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
        "addData": [
            {
                "id": 190,
                "created_at": 1612920101,
                "created_user_id": 2,
                "updated_at": 1612920101,
                "name": {
                    "name_en": "test computer1111",
                    "name_fr": "",
                    "name_de": "",
                    "name_es": "",
                    "name_ru": "",
                    "name_pt": "",
                    "name_zh": "测试计算机"
                },
                "spu": "cikj1612920101",
                "sku": "cikj1612920101-4sekic",
                "score": 0,
                "status": 1,
                "qty": 334,
                "min_sales_qty": null,
                "is_in_stock": 1,
                "url_key": "/test-computer1111-63998226",
                "meta_title": null,
                "price": 33,
                "cost_price": 10,
                "special_price": 32,
                "special_from": 1504886400,
                "special_to": 1662739199,
                "tier_price": "a:2:{i:0;a:2:{s:3:\"qty\";i:2;s:5:\"price\";i:30;}i:1;a:2:{s:3:\"qty\";i:4;s:5:\"price\";i:28;}}",
                "final_price": 32,
                "new_product_from": 1509811200,
                "new_product_to": 1512489599,
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
                        "image": "/f/yf/fyfvari26ef8m241612879330.jpg",
                        "label": "",
                        "sort_order": "",
                        "is_thumbnails": 1,
                        "is_detail": 1
                    },
                    "gallery": [
                        {
                            "image": "/8/oq/8oqxe7gax8wt6qd1612879344.jpg",
                            "label": "",
                            "is_thumbnails": "1",
                            "is_detail": "1",
                            "sort_order": ""
                        },
                        {
                            "image": "/1/c3/1c3jrvnmbiaqjoj1612879357.jpg",
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
                "custom_option": null,
                "remark": "s:4:\"4444\";",
                "long": null,
                "width": null,
                "high": null,
                "weight": 0.3,
                "volume_weight": null,
                "package_number": null,
                "favorite_count": null,
                "relation_sku": null,
                "buy_also_buy_sku": null,
                "see_also_see_sku": null,
                "attr_group": "clothes_group",
                "attr_group_info": {
                    "color": "Red",
                    "size": "L"
                },
                "reviw_rate_star_average": null,
                "review_count": null,
                "reviw_rate_star_average_lang": null,
                "review_count_lang": null,
                "reviw_rate_star_info": null,
                "reviw_rate_star_info_lang": null,
                "origin_mongo_id": null,
                "is_deputy": 1,
                "brand_id": null,
                "third_refer_url": "http://www.taobao.com/xxxxx",
                "third_refer_code": "xxxxxxxxxx1",
                "third_product_code": "yyyyyyyyy1"
            },
            {
                "id": 191,
                "created_at": 1612920101,
                "created_user_id": 2,
                "updated_at": 1612920101,
                "name": {
                    "name_en": "test computer1111",
                    "name_fr": "",
                    "name_de": "",
                    "name_es": "",
                    "name_ru": "",
                    "name_pt": "",
                    "name_zh": "测试计算机"
                },
                "spu": "cikj1612920101",
                "sku": "cikj1612920101-qvx73a",
                "score": 0,
                "status": 1,
                "qty": 34,
                "min_sales_qty": null,
                "is_in_stock": 1,
                "url_key": "/test-computer1111-25888587",
                "meta_title": null,
                "price": 31.2,
                "cost_price": 10,
                "special_price": 32,
                "special_from": 1504886400,
                "special_to": 1662739199,
                "tier_price": "a:2:{i:0;a:2:{s:3:\"qty\";i:2;s:5:\"price\";i:30;}i:1;a:2:{s:3:\"qty\";i:4;s:5:\"price\";i:28;}}",
                "final_price": 32,
                "new_product_from": 1509811200,
                "new_product_to": 1512489599,
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
                        "image": "/f/yf/fyfvari26ef8m241612879330.jpg",
                        "label": "",
                        "sort_order": "",
                        "is_thumbnails": 1,
                        "is_detail": 1
                    },
                    "gallery": [
                        {
                            "image": "/8/oq/8oqxe7gax8wt6qd1612879344.jpg",
                            "label": "",
                            "is_thumbnails": "1",
                            "is_detail": "1",
                            "sort_order": ""
                        },
                        {
                            "image": "/1/c3/1c3jrvnmbiaqjoj1612879357.jpg",
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
                "custom_option": null,
                "remark": "s:4:\"4444\";",
                "long": null,
                "width": null,
                "high": null,
                "weight": 0.3,
                "volume_weight": null,
                "package_number": null,
                "favorite_count": null,
                "relation_sku": null,
                "buy_also_buy_sku": null,
                "see_also_see_sku": null,
                "attr_group": "clothes_group",
                "attr_group_info": {
                    "color": "Blue",
                    "size": "L"
                },
                "reviw_rate_star_average": null,
                "review_count": null,
                "reviw_rate_star_average_lang": null,
                "review_count_lang": null,
                "reviw_rate_star_info": null,
                "reviw_rate_star_info_lang": null,
                "origin_mongo_id": null,
                "is_deputy": 2,
                "brand_id": null,
                "third_refer_url": "http://www.taobao.com/xxxxx",
                "third_refer_code": "xxxxxxxxxx1",
                "third_product_code": "yyyyyyyyy1"
            },
            {
                "id": 192,
                "created_at": 1612920101,
                "created_user_id": 2,
                "updated_at": 1612920101,
                "name": {
                    "name_en": "test computer1111",
                    "name_fr": "",
                    "name_de": "",
                    "name_es": "",
                    "name_ru": "",
                    "name_pt": "",
                    "name_zh": "测试计算机"
                },
                "spu": "cikj1612920101",
                "sku": "cikj1612920101-rkw4od",
                "score": 0,
                "status": 1,
                "qty": 334,
                "min_sales_qty": null,
                "is_in_stock": 1,
                "url_key": "/test-computer1111-76751162",
                "meta_title": null,
                "price": 33.2,
                "cost_price": 10,
                "special_price": 32,
                "special_from": 1504886400,
                "special_to": 1662739199,
                "tier_price": "a:2:{i:0;a:2:{s:3:\"qty\";i:2;s:5:\"price\";i:30;}i:1;a:2:{s:3:\"qty\";i:4;s:5:\"price\";i:28;}}",
                "final_price": 32,
                "new_product_from": 1509811200,
                "new_product_to": 1512489599,
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
                        "image": "/f/yf/fyfvari26ef8m241612879330.jpg",
                        "label": "",
                        "sort_order": "",
                        "is_thumbnails": 1,
                        "is_detail": 1
                    },
                    "gallery": [
                        {
                            "image": "/8/oq/8oqxe7gax8wt6qd1612879344.jpg",
                            "label": "",
                            "is_thumbnails": "1",
                            "is_detail": "1",
                            "sort_order": ""
                        },
                        {
                            "image": "/1/c3/1c3jrvnmbiaqjoj1612879357.jpg",
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
                "custom_option": null,
                "remark": "s:4:\"4444\";",
                "long": null,
                "width": null,
                "high": null,
                "weight": 0.3,
                "volume_weight": null,
                "package_number": null,
                "favorite_count": null,
                "relation_sku": null,
                "buy_also_buy_sku": null,
                "see_also_see_sku": null,
                "attr_group": "clothes_group",
                "attr_group_info": {
                    "color": "Red",
                    "size": "M"
                },
                "reviw_rate_star_average": null,
                "review_count": null,
                "reviw_rate_star_average_lang": null,
                "review_count_lang": null,
                "reviw_rate_star_info": null,
                "reviw_rate_star_info_lang": null,
                "origin_mongo_id": null,
                "is_deputy": 2,
                "brand_id": null,
                "third_refer_url": "http://www.taobao.com/xxxxx",
                "third_refer_code": "xxxxxxxxxx1",
                "third_product_code": "yyyyyyyyy1"
            }
        ]
    }
}

```




































