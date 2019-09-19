Api- Onepage Paypal Standard Review
================

> paypal standard支付，在paypal登录后，点击付款跳转回fecshop后，
> 执行的api,该api进行订单的paypal支付（paypal api支付）


URL: `/payment/paypal/standard/review`

格式：`json`

方式：`post`


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
| token           | 必须        |   String     | paypal token     |
| PayerID         | 必须        |   String     | paypal PayerID   |


**请求参数示例如下：**

```
{
    token: "EC-0WB612551K6101423",
    PayerID: "FKL4V7D5GCACY"
}
```

二：返回部分
----------

#### 1.Reponse Header

| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 选填        |   String     | 用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |

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
| 1500009         | Order: 通过paypal standard方式支付，获取token失败                  | 
| 1500011         | Order: 通过paypal standard方式支付，api支付订单成功后，更新订单信息失败                  | 
| 1500010         | Order: 通过paypal standard方式支付，通过api支付失败                  | 




#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": []
}
```