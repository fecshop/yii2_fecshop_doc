Api- Product Add Review
================

> 给产品增加评论页面，初始化评论的api

URL: `/catalog/reviewproduct/add`

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
| product_id      | 必须        |   String     | Product Id    |


**请求参数示例如下：**

```
{
    product_id: "580835d0f656f240742f0b7c"
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
| 1100003         | 登录：账户的token已经过期,或者没有登录                  | 
| 1300002         | 产品：产品不存在，或者已经下架                 | 
| 1300001         | 产品：产品不存在，或者已经下架                  | 




#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "product": { // 产品信息
            "product_id": "580835d0f656f240742f0b7c",
            "spu": "p10001",
            "price_info": {
                "price": {
                    "symbol": "€",
                    "value": 5.63,
                    "code": "EUR"
                },
                "special_price": {
                    "symbol": "€",
                    "value": 4.7,
                    "code": "EUR"
                }
            },
            "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/150/150/2/01/20160905101021_28071.jpg",
            "product_name": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl"
        },
        "customer_name": "44444 666",  // 当前用户的name
        "reviewCaptchaActive": true    // 是否需要验证码
    }
}
```