Fecshop Api 产品
===============

> Api描述：按照分页，得到Product数据的列表

URL: `http://fecshop.appapi.fancyecommerce.com/v1/product/list`

格式：`json`

方式：`get`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| page            | 可选        |   Int       | 设置获取数据的当前页，如果为空，则代表为第一页|


**Response Header 参数:**


| 参数名称                    | 是否必须    |  类型       |  描述     |
| ----------------------------| -----:      | :----:      |:----:     |
| X-Pagination-Total-Count    | 必须        |   String    | 资源的总数量|
| X-Pagination-Page-Count     | 必须        |   String    | 资源的总页数|
| X-Pagination-Current-Page   | 必须        |   String    | 资源的当前页（目前是第几页）|
| X-Pagination-Per-Page       | 必须        |   String    | 每页资源的数量|
| X-Rate-Limit-Limit          | 可选        |   String    | 在开启速度限制后才会存在，同一个时间段所允许的请求的最大数目|
| X-Rate-Limit-Remaining      | 可选        |   String    | 在开启速度限制后才会存在，在当前时间段内剩余的请求的数量|
| X-Rate-Limit-Reset          | 可选        |   String    | 在开启速度限制后才会存在，为了得到最大请求数所等待的秒数|



**Response JSON Data(Body)：**

格式：`json`

| 参数名称        | 是否必须    |  类型       |  描述        |
| ----------------| -----:      | :----:      |:----:        | 
| code            | 必须        |   Number    | 200 代表成功 |
| message         | 必须        |   String    | 执行结果的文字描述信息  |
| data            | 必须        |   Array    | api获取的数据保存到data中  |

**Response JSON Data(Body Example)：**

```
{
    "code": 200,
    "message": "fetch product success",
    "data": [
        {
            "created_at": 1471852757,
            "created_user_id": 2,
            "updated_at": 1497865443,
            "name": {
                "name_en": "Off-the-Shoulder Long Sleeve High-Low Day Dress",
                "name_fr": "fr Off-the-Shoulder Long Sleeve High-Low Day Dress",
                "name_de": "de Off-the-Shoulder Long Sleeve High-Low Day Dress",
                "name_es": "es Off-the-Shoulder Long Sleeve High-Low Day Dress",
                "name_ru": "ru Off-the-Shoulder Long Sleeve High-Low Day Dress",
                "name_pt": "pt Off-the-Shoulder Long Sleeve High-Low Day Dress",
                "name_zh": "肩带长袖高低日礼服"
            },
            "spu": "kilw",
            "sku": "kilw0001",
            "weight": 99,
            "status": 1,
            "qty": 18,
            "is_in_stock": 1,
            "url_key": "/off-the-shoulder-long-sleeve-high-low-day-dress",
            "category": [
                "57b6abfff656f246653bf570",
                "57bea0d3f656f2ec1f3bf56e",
                "57bea0e3f656f275313bf56e",
                "57b6abfff656f246653bf570",
                "57bea0d3f656f2ec1f3bf56e"
            ],
            "price": 358,
            "cost_price": 444,
            "special_price": 124,
            "special_from": 1471708800,
            "special_to": 1570118400,
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
                "gallery": [
                    {
                        "image": "/1/22/12229472_2.jpg",
                        "label": "",
                        "sort_order": 2,
                        "is_thumbnails": "1",
                        "is_detail": "1"
                    }
                ],
                "main": {
                    "image": "/1/22/12229472_1.jpg",
                    "label": "BLUE",
                    "sort_order": 1,
                    "is_thumbnails": "1",
                    "is_detail": "1"
                }
            },
            "description": {
                "description_en": "Color: BLACK, BLUE, GRAY, RED, WHITE<br />Size: M, L, XL, 2XL<br />Category: Women &gt; Tops &gt; Tees &amp; T-Shirts<br /><br />Material: Rayon,Spandex<br />Clothing Length: Regular<br />Sleeve Length: Short<br />Collar: Skew Collar<br />Style: Casual<br />Season: Summer<br />Pattern Type: Floral<br />Weight: 0.3400kg<br />Package Contents: 1 x T-Shirt<br /><br /><br />",
                "description_fr": "",
                "description_de": "",
                "description_es": "",
                "description_ru": "",
                "description_pt": "",
                "description_zh": "<span id=\"result_box\" lang=\"zh-CN\"><span>颜色：黑色，蓝色，灰色，红色，白色</span><br /><span>尺寸：M，L，XL，2XL</span><br /><span>类别：女装&gt;上衣&gt; T恤＆T恤</span><br /><br /><span>材质：人造丝，氨纶</span><br /><span>服装长度：定期</span><br /><span>袖长：短</span><br /><span>衣领：歪斜领</span><br /><span>风格：休闲</span><br /><span>季节：夏季</span><br /><span>图案类型：花卉</span><br /><span>重量：0.3400kg</span><br /><span>包装内容：1 x T恤</span></span>"
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
            "attr_group": "clothes_group",
            "color": "black",
            "size": "L",
            "dresses-length": "Mid-Calf",
            "score": 99,
            "style": "Vintage ",
            "pattern-type": "Patchwork",
            "sleeve-length": "Sleeveless",
            "collar": "Round Neck",
            "final_price": 124,
            "tier_price": [],
            "reviw_rate_star_average": 5,
            "review_count": 1,
            "reviw_rate_star_average_lang": {
                "reviw_rate_star_average_lang_zh": 5
            },
            "review_count_lang": {
                "review_count_lang_zh": 1
            },
            "favorite_count": 5,
            "relation_sku": "",
            "buy_also_buy_sku": "",
            "see_also_see_sku": "",
            "my_remark": "",
            "my_email": "",
            "my_date": "",
            "id": "57bab0d5f656f2940a3bf56e"
        },
    ]
}
```