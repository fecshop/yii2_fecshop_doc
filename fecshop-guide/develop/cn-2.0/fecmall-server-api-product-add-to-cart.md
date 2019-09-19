Api- Product 加入购物车
================

> 产品页面点击增加产品到购物车按钮后，访问的api

URL: `/checkout/cart/add`

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


| 参数名称        | 是否必须    |  类型        |  描述     |
| ----------------| -----:      | :----:       |:----:     |
| custom_option   | 必须        |   Object     | 用户的自定义属性的信息    |
| product_id      | 必须        |   String     | Product Id                |
| qty             | 必须        |   Integer    | 产品加入购物车的个数      |


**请求参数示例如下：**

```
{
    custom_option:{
        "my_color":"red",
        "my_size":"S",
        "my_size2":"S2",
        "my_size3":"S3"
    },
    product_id: "581c6833f656f2042f2f0b77",
    qty: 1
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
| 1400001         | Cart：产品加入购物车失败                  | 
| 1400002         | Cart：产品加入购物车传递参数无效                  | 




#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "items_count": 18   //购物车中产品总数
    }
}
```