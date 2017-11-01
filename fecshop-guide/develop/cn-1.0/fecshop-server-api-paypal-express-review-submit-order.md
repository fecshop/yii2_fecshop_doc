Api- Cart Paypal Express Review SubmitOrder
================

> 购物车页面点击paypal按钮，跳转到paypal登录，然后点击continue跳转回fecshop页面，
> 页面初始化后，编辑订单信息，然后点击提交后访问的api

URL: `/payment/paypal/express/submitorder`

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
| token             | 必须        |   String    | Paypal Token    |
| PayerID           | 必须        |   String    | Paypal PayerID  |
| shipping_method   | 必须        |   String    | 物流快递的code  |

**请求参数示例如下：**

```
{
    address_id:118,
    billing:{
        first_name: "test",
        last_name: "facilitator",
        email: "zqy234api1-facilitator-1@126.com",
        telephone: "2121",
        street1: "4114 Sepulveda Blvd.",
        street2: "4114 Sepulveda Blvd.",
        country: "US",
        state: "NY",
        city: "New York",
        zip: "10021"
    },
    token: "EC-1TN688728J034651L",
    PayerID: "FKL4V7D5GCACY",
    shipping_method: "fast_shipping"
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
    "data": []
}
```