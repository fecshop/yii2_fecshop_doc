Fecshop Api 分类 AddOne
=========================

> Api描述：根据传递的json数据，新增一行page数据



URL: `http://fecshop.appapi.fancyecommerce.com/v1/category/addone`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| url_key         | 可选        |   String    | Category 对应的url key，如果自定义的url_key存在，系统会添加一块字符串来保证唯一|
| title           | 可选        |   String    | 【多语言属性】page 的标题         |
| meta_keywords   | 可选        |   String    | 【多语言属性】page 的meta keywords|
| meta_description| 可选        |   String    | 【多语言属性】page 的meta keywords|
| parent_id       | 必须        |   String    | 父分类的id|
| name            | 必须        |   String    | 分类的名字|
| status          | 可选        |   String    | 分类的状态，1代表激活，2代表关闭，如果填写其他非法值，系统将强制设置为1|
| description     | 可选        |   String    | 分类的描述|
| menu_custom     | 可选        |   String    | 菜单的自定义属性，用于一级分类弹出的子分类部分，添加一些图片展示之类的东西|
| filter_product_attr_selected         | 可选        |   String    | 分类侧栏用于属性过滤的产品属性，填写后，会聚合所有的该分类下的产品对应的所有的该属性 |
| filter_product_attr_unselected       | 可选        |   String    | 不聚合的产品属性，对于分类页面的侧栏属性过滤的属性，有一个全局配置，配置后，所有的分类都将存在该属性的过滤，如果这个值填写了该属性，那么在这个分类下，全局设置将会去除该属性 |
| thumbnail_image | 可选        |   String    | 分类图 |
| image           | 可选        |   String    | 分类图 |



对于多语言属性的`数据结构`和`必填`的详细说明参看： [AppApi多语言属性说明](fecshop-api-mutil-lang.md)

**Request JSON Data(Body Example)：**

```
{
    "parent_id": "0",
    "name": {
        "name_en": "Wedding2222",
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
    "default_sort_by": null
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
    "message": "add article success",
    "data": {
        "addData": {
            "created_at": 1511708701,
            "created_user_id": 1,
            "_id": "5a1ad81dbfb7ae7f870b3bf3",
            "level": 1,
            "updated_at": 1511708701,
            "parent_id": "0",
            "name": {
                "name_en": "Wedding2222",
                "name_fr": "",
                "name_de": "",
                "name_es": "",
                "name_ru": "",
                "name_pt": "",
                "name_zh": "婚礼"
            },
            "status": 1,
            "menu_show": 1,
            "url_key": "/wedding-39678474",
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
            }
        }
    }
}

```
