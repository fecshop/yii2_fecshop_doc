Fecshop Api 分类 UpdateOne-2
=========================

> Api描述：根据传递的id或url_key，更新一行page数据

用于erp传递分类数据。

URL: `http://fecshop.appapi.fancyecommerce.com/v1/category/upsertone2`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称                      | 是否必须    |  类型       |  描述     |
| ------------------------------| -----:      | :----:      |:----:     |
| remote_id                            | 必填        |   String    | 分类对应的id，该值是用来做update操作的唯一值 |
| remote_parent_id                     | 必填        |   String    | 分类的父类id，如果是一级分类，那么parent_id为字符串"0"|
| name                          | 必填        |   String    | 【多语言属性】分类的名字         |
| description                   | 必填        |   String    | 【多语言属性】分类的描述         |
| menu_custom                   | 可选        |   String    | 【多语言属性】分类的一个自定义属性         |
| filter_product_attr_selected  | 可选        |   String    | 用于在分类侧栏过滤的产品属性         |
| filter_product_attr_unselected| 可选        |   String    | 不用于在分类侧栏过滤的产品属性（可以从分类的全局设置中剔除）         |
| thumbnail_image               | 可选        |   String    | 分类图片         |
| image                         | 可选        |   String    | 分类图片         |
| url_key                       | 可选        |   String    | 分类 对应的url key，如果自定义的url_key存在，系统会添加一块字符串来保证唯一，如果不填写，则使用name（默认语言）的值来生成|
| menu_show                     | 可选        |   String    | 分类是否在菜单栏中显示|
| title                         | 可选        |   String    | 【多语言属性】分类 的标题         |
| meta_keywords                 | 可选        |   String    | 【多语言属性】分类 的meta keywords|
| meta_description              | 可选        |   String    | 【多语言属性】分类 的meta keywords|
| status                        | 必填        |   String    | 分类的状态，1代表激活，2代表关闭，如果填写其他非法值，系统将强制设置为1|


**补充1**：`remote_id`为远程数据表的category_id, 当fecmall的`remote_id`存在该值，则进行更新，如果不存在则插入。

**补充2**：对于获取的分类参数，您在获取之前，应该先按照`level`进行排序，否则可能会出现找不到`remote_parent_id`的现象。


对于多语言属性的`数据结构`和`必填`的详细说明参看： [AppApi多语言属性说明](fecshop-api-mutil-lang.md)

**Request JSON Data(Body Example)：**

```
{
    "remote_id": "101",
    "remote_parent_id": "100",
    "name": {
        "name_en": "Wedding998",
        "name_fr": "",
        "name_de": "",
        "name_es": "",
        "name_ru": "",
        "name_pt": "",
        "name_zh": "婚礼"
    },
    "status": 1,
    "menu_show": 1,
    "url_key": "/wedding-31685117",
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
    }
    
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
    "message": "update category success",
    "data": {
        "updateData": {
            "id": 69,
            "created_at": 1618922822,
            "created_user_id": 2,
            "updated_at": 1618922985,
            "parent_id": 68,
            "name": {
                "name_en": "Wedding998",
                "name_fr": "",
                "name_de": "",
                "name_es": "",
                "name_ru": "",
                "name_pt": "",
                "name_zh": "婚礼"
            },
            "status": 1,
            "url_key": "/wedding-26461548",
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
            "level": 2,
            "filter_product_attr_selected": "style,dresses-length,pattern-type,sleeve-length,collar,color",
            "filter_product_attr_unselected": null,
            "menu_show": 1,
            "thumbnail_image": null,
            "image": null,
            "origin_mongo_id": null,
            "origin_mongo_parent_id": null,
            "sort_order": null,
            "remote_id": "101",
            "remote_parent_id": "100"
        }
    }
}

```

