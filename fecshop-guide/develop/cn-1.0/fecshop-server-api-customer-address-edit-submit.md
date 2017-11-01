Api- Customer address 编辑提交
================

> customer address 账户中心编辑address后，保存address的api

URL: `/customer/address/save`

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


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| address_id      | 必须        |   String    | Address Id    |
| first_name      | 必须        |   String    | 用户收货地址填写的first name   |
| last_name       | 必须        |   String    | 用户收货地址填写的last  name   |
| email           | 必须        |   String    | 用户的email          |
| telephone       | 必须        |   String    | 收货地址的telephone  |
| addressCountry  | 必须        |   String    | 收货地址的国家       |
| addressState    | 必须        |   String    | 收货地址的州/省      |
| city            | 必须        |   String    | 收货地址的城市       |
| street1         | 必须        |   String    | 收货地址的详细街道地址1  |
| street2         | 必须        |   String    | 收货地址的详细街道地址2  |
| isDefaultActive | 必须        |   Integer   | 是否是默认收货地址，1代表是，0代表不是  |
| zip             | 必须        |   String    | 收货地址的邮编       |

**请求参数示例如下：**

```
{
    address_id:118
    first_name:2121
    last_name:2121
    email:fdfd@3232.com
    telephone:2121
    addressCountry:AT
    addressState:NO
    city:2121
    street1:2121
    street2:2121
    isDefaultActive:1
    zip:2121
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