Fecshop Api Page UpdateOne
=========================

> Api描述：根据传递的id或url_key，更新一行page数据


URL: `http://fecshop.appapi.fancyecommerce.com/v1/article/updateone`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| id              | 必填        |   String    | page 对应的id，该值是用来做update操作的唯一值 |
| url_key         | 可选        |   String    | page 对应的url key，如果自定义的url_key存在，系统会添加一块字符串来保证唯一|
| title           | 可选        |   String    | 【多语言属性】page 的标题         |
| meta_keywords   | 可选        |   String    | 【多语言属性】page 的meta keywords|
| meta_description| 可选        |   String    | 【多语言属性】page 的meta keywords|
| content         | 可选        |   String    | 【多语言属性】page 的内容部分|
| status          | 可选        |   String    | page的状态，1代表激活，10代表关闭，如果填写其他非法值，系统将强制设置为1|



对于多语言属性的`数据结构`和`必填`的详细说明参看： [AppApi多语言属性说明](fecshop-api-mutil-lang.md)

**Request JSON Data(Body Example)：**

```
{
    "id":"5a17f446bfb7ae261d64e95a",
    "url_key": "/myapipage1",
    "title": {
        "title_en": "about us",
        "title_fr": "",
        "title_de": "",
        "title_es": "",
        "title_ru": "",
        "title_pt": "",
        "title_zh": "关于我们"
    },
    "meta_keywords": {
        "meta_keywords_en": "about us",
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
    "content": {
        "content_en": "Fecshop called Fancy ECommerce Shop, is based on php Yii2 framework developed on a good open source electricity business system, follow OSL3.0 open source agreement, Fecshop support multi-language, multi-currency, architecture support pc, mobile phone, mobile app",
        "content_fr": "",
        "content_de": "",
        "content_es": "",
        "content_ru": "",
        "content_pt": "",
        "content_zh": "Fecshop 全称为Fancy ECommerce Shop，是基于php Yii2框架之上开发的一款优秀的开源电商系统，遵循OSL3.0开源协议，Fecshop支持多语言，多货币，架构上支持pc，手机web，手机app，和erp对接等入口"
    },
    "status":1
    
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
        "updateData": {
            "_id": "5a17f446bfb7ae261d64e95a",
            "url_key": "/myapipage1-31213786",
            "title": {
                "title_en": "about us",
                "title_fr": "",
                "title_de": "",
                "title_es": "",
                "title_ru": "",
                "title_pt": "",
                "title_zh": "关于我们"
            },
            "meta_keywords": {
                "meta_keywords_en": "about us",
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
            "content": {
                "content_en": "Fecshop called Fancy ECommerce Shop, is based on php Yii2 framework developed on a good open source electricity business system, follow OSL3.0 open source agreement, Fecshop support multi-language, multi-currency, architecture support pc, mobile phone, mobile app",
                "content_fr": "",
                "content_de": "",
                "content_es": "",
                "content_ru": "",
                "content_pt": "",
                "content_zh": "Fecshop 全称为Fancy ECommerce Shop，是基于php Yii2框架之上开发的一款优秀的开源电商系统，遵循OSL3.0开源协议，Fecshop支持多语言，多货币，架构上支持pc，手机web，手机app，和erp对接等入口"
            },
            "status": 10,
            "created_at": 1511519302,
            "updated_at": 1511536135,
            "created_user_id": 1
        }
    }
}

```

