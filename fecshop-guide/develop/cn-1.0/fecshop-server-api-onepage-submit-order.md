Api- Onepage 更新信息
================

> vue checkout onepage 页面，填写完订单信息，点击提交按钮执行的api

URL: `/checkout/onepage/submitorder`

格式：`json`

方式：`post`


一：请求部分
---------

#### 1.Request Header


| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 必须        |   String     | 从localStorage取出来的值，识别用户登录状态的标示，用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |
| fecshop-uuid      | 必须        |   String     | 从localStorage取出来的值，用户的唯一标示，VUE第一次访问服务端，服务端会返回fecshop-uuid ，VUE将其保存到本地，后面的每一次请求都需要加上fecshop-uuid    |
| fecshop-currency  | 必须        |   String     | 从localStorage取出来的值，当前的货币值  |
| fecshop-lang      | 必须        |   String     | 从localStorage取出来的值，当前的语言code  |


#### 2.Request Body Form-Data：


| 参数名称          | 是否必须    |  类型       |  描述     |
| ----------------  | -----:      | :----:      |:----:     |
| address_id        | 必须        |   String    | 如果用户登录账户，使用的是保存的address信息，则这里需要传递address id   |
| billing           | 必须        |   Array     | 订单的用户信息和地址信息   |
| create_account    | 必须        |   String    |  是否创建新用户。0代表不创建账户，1代表创建账户，当游客下单的时候，可以勾选创建账户，在下单的时候，顺便创建用户， |
| customer_password | 必须        |   String    | create_account为1时有效，创建账户的密码字段    |
| confirm_password  | 必须        |   String    | create_account为1时有效，创建账户的确认密码字段，密码和确认密码需要一致    |
| shipping_method   | 必须        |   String    | 物流快递的code  |
| payment_method    | 必须        |   String    | 订单的支付渠道  |


**请求参数示例如下：**

```
{
    address_id:118,
    billing:{
        first_name: "2121",        
        last_name： "xxx",
        email: "fdfd@3232.com",
        telephone: "2121",
        street1: "2121",
        street2: "2121",
        country: "AT",
        state: "NO",
        city: "2121",
        zip: "2121"
    },
    customer_password:"",
    confirm_password:"",
    create_account:0,
    shipping_method:"fast_shipping",
    payment_method:"paypal_standard"
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

返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "redirectUrl": "/payment/paypal/standard/start" // 生成订单，根据支付房还是，进入相应的支付url，这个就是要跳转的url地址
    }
}
```