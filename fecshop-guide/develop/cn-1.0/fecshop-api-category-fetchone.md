Fecshop Api 分类 FetchOne
=========================

> Api描述：根据传递的id或url_key，查询得到一行category数据


URL: `http://fecshop.appapi.fancyecommerce.com/v1/category/fetchone`

格式：`json`

方式：`get`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| id              | 可选        |   String    | category的表id，当page存储在mongodb时，id就是字符串，譬如mongodb的_id：57937114f656f2f42ce25ca5|
| url_key         | 可选        |   String    | category的url_key，url_key是唯一的|

**注意**: `id` 和`url_key`，应至少填写一个，否则将会报错，如果都填写，将以`id`
参数为准，`url_key`参数将会被忽略。

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
    "message": "fetch category success",
    "data": {
        "parent_id": "0",  
        "name": {
            "name_en": "Wedding",
            "name_fr": "",
            "name_de": "",
            "name_es": "",
            "name_ru": "",
            "name_pt": "",
            "name_zh": "婚礼"
        },
        "status": 1,
        "menu_show": 1,
        "url_key": "/wedding",
        "level": 1,
        "thumbnail_image": null,
        "image": null,
        "filter_product_attr_selected": "style,dresses-length,pattern-type,sleeve-length,collar,color",
        "filter_product_attr_unselected": "",
        "description": {
            "description_en": "",
            "description_fr": "",
            "description_de": "",
            "description_es": "",
            "description_ru": "",
            "description_pt": "",
            "description_zh": ""
        },
        "menu_custom": {
            "menu_custom_en": "<a href=\"//fecshop.appfront.fancyecommerce.com/wedding\"><img alt=\"\" src=\"//img.fancyecommerce.com/custom/menu/what_a.jpg\" width=\"244\" /></a><a style=\"margin-left: 20px;\" href=\"//fecshop.appfront.fancyecommerce.com/wedding\"><img alt=\"\" src=\"//img.fancyecommerce.com/custom/menu/what_b.jpg\" width=\"244\" /></a>",
            "menu_custom_fr": "<a href=\"//fecshop.appfront.fancyecommerce.com/fr/wedding\"><img alt=\"\" src=\"//img.fancyecommerce.com/custom/menu/what_a.jpg\" width=\"244\" /></a><a style=\"margin-left: 20px;\" href=\"//fecshop.appfront.fancyecommerce.com/fr/wedding\"><img alt=\"\" src=\"//img.fancyecommerce.com/custom/menu/what_b.jpg\" width=\"244\" /></a>",
            "menu_custom_de": "",
            "menu_custom_es": "",
            "menu_custom_ru": "",
            "menu_custom_pt": "",
            "menu_custom_zh": ""
        },
        "title": {
            "title_en": "Wedding",
            "title_fr": "",
            "title_de": "",
            "title_es": "",
            "title_ru": "",
            "title_pt": "",
            "title_zh": ""
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
        "meta_keywords": {
            "meta_keywords_en": "",
            "meta_keywords_fr": "",
            "meta_keywords_de": "",
            "meta_keywords_es": "",
            "meta_keywords_ru": "",
            "meta_keywords_pt": "",
            "meta_keywords_zh": ""
        },
        "include_in_menu": null,
        "is_feature": null,
        "available_sort_by": null,
        "default_sort_by": null,
        "theme": null,
        "active_from": null,
        "active_to": null,
        "created_at": 1471589375,
        "updated_at": 1500455296,
        "created_user_id": 2,
        "id": "57b6abfff656f246653bf570"
    }
}

```