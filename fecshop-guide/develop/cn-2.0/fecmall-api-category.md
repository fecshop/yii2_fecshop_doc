Fecshop Api 分类 List
=========================

> Api描述：按照分页，得到分类数据的列表

URL: `http://fecshop.appapi.fancyecommerce.com/v1/category/list`

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
| numPerPage            | 可选        |   Int       | 设置获取数据每页的个数，如果为空，则会使用fecmall的默认值|

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
    "message": "fetch category success",
    "data": [
        {
            "created_at": 1471589375,   // 创建时间戳
            "created_user_id": 2,       // 创建客服user id
            "updated_at": 1500455296,   // 更新时间戳
            "parent_id": "0",           // 父分类的id，当父分类id为 "0",则代表该分类为1级分类
            "name": {                   // 分类的名字
                "name_en": "Wedding",
                "name_fr": "",
                "name_de": "",
                "name_es": "",
                "name_ru": "",
                "name_pt": "",
                "name_zh": "婚礼"
            },
            "status": 1,                // 分类的状态，1代表激活，2代表关闭
            "url_key": "/wedding",      // 分类的url key ， 用于在appfront  apphtml5端生成自定义url用，该字段唯一
            "description": {            // 分类的描述
                "description_en": "",
                "description_fr": "",
                "description_de": "",
                "description_es": "",
                "description_ru": "",
                "description_pt": "",
                "description_zh": ""
            },
            "title": {                  // 分类的标题
                "title_en": "Wedding",
                "title_fr": "",
                "title_de": "",
                "title_es": "",
                "title_ru": "",
                "title_pt": "",
                "title_zh": ""
            },
            "meta_description": {       // 分类的meta description
                "meta_description_en": "",
                "meta_description_fr": "",
                "meta_description_de": "",
                "meta_description_es": "",
                "meta_description_ru": "",
                "meta_description_pt": "",
                "meta_description_zh": ""
            },
            "meta_keywords": {          // 分类的meta keywords
                "meta_keywords_en": "",
                "meta_keywords_fr": "",
                "meta_keywords_de": "",
                "meta_keywords_es": "",
                "meta_keywords_ru": "",
                "meta_keywords_pt": "",
                "meta_keywords_zh": ""
            },
            "menu_custom": {            // 分类的自定义属性，用于在一级分类展开的子分类的右侧，显示一些图片等内容
                "menu_custom_en": "<a href=\"//fecshop.appfront.fancyecommerce.com/wedding\"><img alt=\"\" src=\"//img.fancyecommerce.com/custom/menu/what_a.jpg\" width=\"244\" /></a><a style=\"margin-left: 20px;\" href=\"//fecshop.appfront.fancyecommerce.com/wedding\"><img alt=\"\" src=\"//img.fancyecommerce.com/custom/menu/what_b.jpg\" width=\"244\" /></a>",
                "menu_custom_fr": "<a href=\"//fecshop.appfront.fancyecommerce.com/fr/wedding\"><img alt=\"\" src=\"//img.fancyecommerce.com/custom/menu/what_a.jpg\" width=\"244\" /></a><a style=\"margin-left: 20px;\" href=\"//fecshop.appfront.fancyecommerce.com/fr/wedding\"><img alt=\"\" src=\"//img.fancyecommerce.com/custom/menu/what_b.jpg\" width=\"244\" /></a>",
                "menu_custom_de": "",
                "menu_custom_es": "",
                "menu_custom_ru": "",
                "menu_custom_pt": "",
                "menu_custom_zh": ""
            },
            "level": 1,                // 分类的级别
            "filter_product_attr_selected": "style,dresses-length,pattern-type,sleeve-length,collar,color",    // 分类侧栏用于属性过滤的产品属性，填写后，会聚合所有的该分类下的产品对应的所有的该属性
            "filter_product_attr_unselected": "",            // 不聚合的产品属性，对于分类页面的侧栏属性过滤的属性，有一个全局配置，配置后，所有的分类都将存在该属性的过滤，如果这个值填写了该属性，那么在这个分类下，全局设置将会去除该属性
            "menu_show": 1,            // 是否在主菜单中显示该菜单 1，代表显示，2代表不显示
            "id": "57b6abfff656f246653bf570"  // 分类的id
        },
        
        {
        ...
        }
    ]
}
```