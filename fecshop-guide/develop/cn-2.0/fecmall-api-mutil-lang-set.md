Fecmall Api 设置多语言
=============



> Api描述：设置多语言配置。



URL: `http://fecshop.appapi.fancyecommerce.com/v1/languages/setall`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| languages         | 必须        |   Array    | 多语言配置内容 |

languages 数组子项参数详细

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| lang_name         | 必须        |   String    | 语言名称 |
| lang_code         | 必须        |   String    | 语言简码 |
| is_default         | 必须        |   boolean    | 是否默认语言 |


**Request JSON Data(Body Example)：**

```
{
    "languages": [
        {
            "lang_name": "en-US",
            "lang_code": "en",
            "is_default": true
        },
        {
            "lang_name": "zh-CN",
            "lang_code": "zh",
            "is_default": false
        },
        {
            "lang_name": "fr-FR",
            "lang_code": "fr",
            "is_default": false
        },
        {
            "lang_name": "de-DE",
            "lang_code": "de",
            "is_default": false
        },
        {
            "lang_name": "es-ES",
            "lang_code": "es",
            "is_default": false
        },
        {
            "lang_name": "pt-PT",
            "lang_code": "pt",
            "is_default": false
        },
        {
            "lang_name": "ru-RU",
            "lang_code": "ru",
            "is_default": false
        },
        {
            "lang_name": "it-IT",
            "lang_code": "it",
            "is_default": false
        },
        {
            "lang_name": "jp-JP",
            "lang_code": "jp",
            "is_default": false
        }
    ]
    
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
    "message": "set all languages success",
    "data": true
}

```






































