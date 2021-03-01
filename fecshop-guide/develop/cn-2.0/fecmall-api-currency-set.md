Fecmall Api 设置货币
===========

> Api描述：设置货币。


URL: `http://fecshop.appapi.fancyecommerce.com/v1/currency/setall`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| currencys         | 必须        |   Array    | 多语言配置内容 |

currencys 数组子项参数详细

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| currency_code         | 必须        |   String    | 货币简码 |
| currency_rate         | 必须        |   String    | 货币汇率 |
| currency_symbol         | 必须        |   String    | 货币符号 |
| is_default         | 必须        |   boolean    | 是否默认货币 |


**Request JSON Data(Body Example)：**

```
{
    "currencys": [
        
        {
            "currency_code": "EUR",
            "currency_rate": 0.93,
            "currency_symbol": "€",
            "is_default": false
        },
        {
            "currency_code": "USD",
            "currency_rate": 1,
            "currency_symbol": "$",
            "is_default": true
        },
        {
            "currency_code": "GBP",
            "currency_rate": 0.8,
            "currency_symbol": "£",
            "is_default": false
        },
        {
            "currency_code": "CNY",
            "currency_rate": 6.3,
            "currency_symbol": "￥",
            "is_default": false
        },
        {
            "currency_code": "JPY",
            "currency_rate": 104.02,
            "currency_symbol": "JP¥",
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
    "message": "set all currency success",
    "data": true
}

```


























































