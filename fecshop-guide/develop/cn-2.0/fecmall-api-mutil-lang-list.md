Fecmall Api 获取多语言 List
=====================

> 获取fecmall商城的多语言部分的配置列表

### 获取fecmall的语言列表api



URL: `http://fecshop.appapi.fancyecommerce.com/v1/languages`

格式：`json`

方式：`get`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|



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
    "message": "fetch all languages success",
    "data": [
        {
            "name": "en-US",
            "code": "en",
            "is_default": true
        },
        {
            "name": "zh-CN",
            "code": "zh",
            "is_default": false
        },
        {
            "name": "fr-FR",
            "code": "fr",
            "is_default": false
        },
        {
            "name": "de-DE",
            "code": "de",
            "is_default": false
        },
        {
            "name": "es-ES",
            "code": "es",
            "is_default": false
        },
        {
            "name": "pt-PT",
            "code": "pt",
            "is_default": false
        },
        {
            "name": "ru-RU",
            "code": "ru",
            "is_default": false
        },
        {
            "name": "it-IT",
            "code": "it",
            "is_default": false
        },
        {
            "name": "jp-JP",
            "code": "jp",
            "is_default": false
        }
    ]
}
```










