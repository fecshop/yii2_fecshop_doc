Api- Onepage Alipay Standard Review
================

> 标准支付，选择alipay支付方式支付成功后返回fecshop页面加载的api，用于访问支付宝
> ,验证当前订单是否支付成功。

URL: `/payment/alipay/standard/review`

格式：`json`

方式：`get`


一：请求部分
---------

#### 1.Request Header


| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 必须        |   String     | 从localStorage取出来的值，识别用户登录状态的标示，用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |
| fecshop-currency  | 必须        |   String     | 从localStorage取出来的值，当前的货币值  |
| fecshop-lang      | 必须        |   String     | 从localStorage取出来的值，当前的语言code  |


#### 2.Request Body Form-Data：


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| total_amount    | 必须        |   String    | 订单的总金额    |
| timestamp       | 必须        |   String    | 支付时间   |
| sign            | 必须        |   String    | 签名，用于安全认证的 |
| trade_no        | 必须        |   String    | 支付宝的订单号     |
| sign_type       | 必须        |   String    | 签名类型  |
| auth_app_id     | 必须        |   String    | 支付宝的appId，用于身份验证的  |
| charset         | 必须        |   String    | 编码  |
| seller_id       | 必须        |   String    | 商家id，用于身份验证  |
| method          | 必须        |   String    | 请求的api的method  |
| app_id          | 必须        |   String    | appid  |
| out_trade_no    | 必须        |   String    | 详细看支付宝接口  |
| version         | 必须        |   String    | 支付宝支付接口的版本号  |


**请求参数示例如下：**

```
{
    total_amount: "927.80",
    timestamp: "2017-11-01 11:39:51",
    sign: "UynUHkgJWkWYIz3F7/bqu+nJcjKsGYijDsERELtnUBGBDa9utAsMdMv7AC6tN+/ANFoXh6yzmNh+gJ7Sws4Ka4Ea8PiAHCQCRPUhZ6lPCfKUB0RPq9bdVZ6yBoF54iODEjveeIsjAQR3pnSLzy5xf+oZyLsYWLxuFuLR/2OfJeuIU1quFH4kKCGAIYbgzfCk77cQ9mpufE4W9jKqH3A2EILJR8X78E6B09sMki+FysZ+ZiFkIJNUQTk9liDXN+98g89Tf+AUOAlm16UnyLMCHJvhc9/GCMRP8WNMOaisuC8VKqMpEFPHF5g/8LFy9fA2JCFnZt5JRvqIZR6vv6swEw==",
    trade_no: "2017110121001004590200337793",
    sign_type: "RSA2",
    auth_app_id: "2016080500172713",
    charset: "UTF-8",
    seller_id: "2088102170055546",
    method: "alipay.trade.wap.pay.return",
    app_id: "2016080500172713",
    out_trade_no: "1100000914",
    version: "1.0"
}
```

二：返回部分
----------

#### 1.Reponse Header

| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 选填        |   String     | 用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |
| fecshop-uuid      | 必须        |   String     | 用户的唯一标示，VUE第一次访问服务端，服务端会返回fecshop-uuid ，VUE将其保存到本地，后面的每一次请求都需要加上fecshop-uuid    |

#### 2.Reponse Body Form-Data：

格式：`json`

| 参数名称        | 是否必须    |  类型       |  描述        |
| ----------------| -----:      | :----:      |:----:        | 
| code            | 必须        |   Number    | 返回状态码，200 代表完成，完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md) |
| message         | 必须        |   String    | 返回状态字符串描述  |
| data            | 必须        |   Array     | 返回详细数据        |


#### 3.参数code所有返回状态码：（完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md) ）

| code Value      |        描述                                        |
| ----------------| --------------------------------------------------:| 
| 200             | 成功状态码                                         |  
| 1500019         | Order: 下订单，支付宝支付订单失败                  | 



#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {}
}
```