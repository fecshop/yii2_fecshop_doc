Fecshop Api Page FetchOne
=========================

> Api描述：根据传递的id或url_key，查询得到一行page数据


URL: `http://fecshop.appapi.fancyecommerce.com/v1/article/fetchone`

格式：`json`

方式：`get`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| id              | 可选        |   String    | Page(Article)的表id，当page存储在mongodb时，id就是字符串，譬如mongodb的_id：57937114f656f2f42ce25ca5|
| url_key         | 可选        |   String    | Page(Article)的url_key，url_key是唯一的|

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
    "message": "fetch article success",
    "data":  {
        "id": "32",               // id
        "url_key": "/about-us",   // page的url key
        "title": {                // page的meta title，下面是各个语言的值
            "title_en": "about us",
            "title_fr": "",
            "title_de": "",
            "title_es": "",
            "title_ru": "",
            "title_pt": "",
            "title_zh": "关于我们"
        },
        "meta_keywords": {        // page的 meta keywords
            "meta_keywords_en": "about us",
            "meta_keywords_fr": "",
            "meta_keywords_de": "",
            "meta_keywords_es": "",
            "meta_keywords_ru": "",
            "meta_keywords_pt": "",
            "meta_keywords_zh": ""
        },
        "meta_description": {    // page的 meta description
            "meta_description_en": "",
            "meta_description_fr": "",
            "meta_description_de": "",
            "meta_description_es": "",
            "meta_description_ru": "",
            "meta_description_pt": "",
            "meta_description_zh": ""
        },
        "content": {            // page的 内容
            "content_en": "Fecshop called Fancy ECommerce Shop, is based on php Yii2 framework developed on a good open source electricity business system ...",
            "content_de": "",
            "content_es": "",
            "content_ru": "",
            "content_pt": "",
            "content_zh": "Fecshop 全称为Fancy ECommerce Shop ...."
        },
        "status": "1",         // page的 状态
        "created_at": "1489676914",   // page的 创建时间戳
        "updated_at": "1491903445",   // page的 更新时间戳
        "created_user_id": "2"        // page的创建人的user_id
    }
}

```