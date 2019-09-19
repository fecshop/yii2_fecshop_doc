Fecshop Api 产品 FetchOne
=========================

> Api描述：根据传递的id，查询得到一行product数据


URL: `http://fecshop.appapi.fancyecommerce.com/v1/product/fetchone`

格式：`json`

方式：`get`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| id              | 可选        |   String    | product的表id，譬如：57937114f656f2f42ce25ca5|



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

**Response JSON Data(Body Example)：**

```
{
    "code": 200,
    "message": "fetch product success",
    "data": {
        "created_at": 1478071424,
        "created_user_id": 2,
        "updated_at": 1497865297,
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
        "sku": "computer001-xinghao1-cpu3",
        "weight": 0,
        "score": 0,
        "status": 1,
        "qty": 334,
        "is_in_stock": 1,
        "url_key": "/test-computer-98383376",
        "category": [
            "57beb586f656f275313bf57a"
        ],
        "price": 33,
        "cost_price": 0,
        "special_price": 0,
        "special_from": 0,
        "special_to": 0,
        "tier_price": [],
        "final_price": 33,
        "new_product_from": 0,
        "new_product_to": 0,
        "meta_title": {
            "meta_title_en": "",
            "meta_title_fr": "",
            "meta_title_de": "",
            "meta_title_es": "",
            "meta_title_ru": "",
            "meta_title_pt": "",
            "meta_title_zh": ""
        },
        "meta_keywords": {
            "meta_keywords_en": "",
            "meta_keywords_fr": "",
            "meta_keywords_de": "",
            "meta_keywords_es": "",
            "meta_keywords_ru": "",
            "meta_keywords_pt": "",
            "meta_keywords_zh": ""
        },
        "meta_description": {
            "meta_description_en": "",
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
            }
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
            "short_description_en": "",
            "short_description_fr": "",
            "short_description_de": "",
            "short_description_es": "",
            "short_description_ru": "",
            "short_description_pt": "",
            "short_description_zh": ""
        },
        "custom_option": [],
        "remark": "",
        "attr_group": "computer_group",
        "memory_capacity": {
            "memory_capacity_en": "",
            "memory_capacity_fr": "",
            "memory_capacity_de": "",
            "memory_capacity_es": "",
            "memory_capacity_ru": "",
            "memory_capacity_pt": "",
            "memory_capacity_zh": ""
        },
        "xinghao": "xinghao1",
        "cpu": "cpu3",
        "relation_sku": "",
        "buy_also_buy_sku": "",
        "see_also_see_sku": "",
        "favorite_count": 1,
        "reviw_rate_star_average": 5,
        "review_count": 1,
        "reviw_rate_star_average_lang": {
            "reviw_rate_star_average_lang_en": 5
        },
        "review_count_lang": {
            "review_count_lang_en": 1
        },
        "id": "58199480f656f28a2a2f0b7b"
    }
}
```