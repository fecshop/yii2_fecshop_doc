Fecmall Api 获取货币 List
=============


> 获取fecmall商城的货币部分的配置列表

### 获取fecmall的货币列表api



URL: `http://fecshop.appapi.fancyecommerce.com/v1/currency`

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
    "message": "fetch all currency success",
    "data": {
        "EUR": {
            "code": "EUR",
            "rate": "0.93",
            "symbol": "€"
        },
        "USD": {
            "code": "USD",
            "rate": "1",
            "symbol": "$"
        },
        "GBP": {
            "code": "GBP",
            "rate": "0.8",
            "symbol": "£"
        },
        "CNY": {
            "code": "CNY",
            "rate": "6.3",
            "symbol": "￥"
        },
        "JPY": {
            "code": "JPY",
            "rate": "104.02",
            "symbol": "JP¥"
        }
    }
}
```




































