Api- Product Review List
================

> vue 分类页面，得到分类信息的api

URL: `/catalog/reviewproduct/lists`

格式：`json`

方式：`get`


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


| 参数名称        | 是否必须    |  类型        |  描述     |
| ----------------| -----:      | :----:       |:----:     |
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
        "product": {
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
            "name": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl"
        },
        "reviewList": [
            {
                "_id": {
                    "$oid": "5818086ff656f20f292f0b77"
                },
                "product_spu": "p10001",
                "product_id": "580835d0f656f240742f0b7c",
                "rate_star": "3",
                "name": "terr fdf",
                "user_id": 17,
                "ip": "119.123.79.199",
                "summary": "fdsfds",
                "review_content": "fdsaf",
                "review_date": 1477970031,
                "store": "fecshop.appfront.fancyecommerce.com/fr",
                "lang_code": "fr",
                "status": 1,
                "audit_user": 2,
                "audit_date": 1477970038
            }
        ],
        "review_count": 1,
        "reviw_rate_star_average": 3
    }
}
```