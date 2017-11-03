Api- Product Search 无限加载
================

> 产品搜索页面，无限加载产品使用的api

URL: `/catalogsearch/index/product`

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


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| q               | 必须        |   String     | 查询的内容   |
| filterAttrs     | 必须        |   ARRAY      | 分类侧栏的属性过滤，没有属性过滤则填写空数组   |
| price           | 必须        |   String     | 分类侧栏价格过滤     |
| p               | 必须        |   Integer    | 分页的页数    |


**请求参数示例如下：**


```
{
    q: "dress",
    filterAttrs:{
        "color":"red"
    },
    price:"20-30",
    p:2
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
| 1000012         | 确定为攻击返回的状态                               | 


#### 4.返回数据举例：

```
{
    "code": 200,
    "content": {
        "products": [ // 不需要注释了，都能看懂
            {
                "one": {
                    "name": "Alluring Long Sleeve Open Back Draped Maxi Dress",
                    "sku": "sk1000-blue",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160727121110_30054.jpg",
                    "price": {
                        "symbol": "€",
                        "value": 30.69,
                        "code": "EUR"
                    },
                    "special_price": "",
                    "url": "/catalog/product/",
                    "product_id": "57cfc282f656f21231df9ded"
                },
                "two": {
                    "name": "Round Collar Floral Print Sleeveless Dress For Women ",
                    "sku": "432432",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/1/7/17147202419675158.jpg",
                    "price": {
                        "symbol": "€",
                        "value": 20.46,
                        "code": "EUR"
                    },
                    "special_price": "",
                    "url": "/catalog/product/",
                    "product_id": "57bac5c6f656f2940a3bf570"
                }
            },
            {
                "one": {
                    "name": "Sweet Polka Dot Open Back Summer Dress For Women",
                    "sku": "sk0003",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160804090311_12690.jpg",
                    "price": {
                        "symbol": "€",
                        "value": 30.69,
                        "code": "EUR"
                    },
                    "special_price": "",
                    "url": "/catalog/product/",
                    "product_id": "57c7da9af656f2577a3bf56e"
                },
                "two": {
                    "name": "Elegant Round Neck Sleeveless Printed Jacquard Dress For Women",
                    "sku": "sk10004-001",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160418182628_30828.jpg",
                    "price": {
                        "symbol": "€",
                        "value": 40.92,
                        "code": "EUR"
                    },
                    "special_price": "",
                    "url": "/catalog/product/",
                    "product_id": "57d61233f656f2b57ddf9ded"
                }
            },
            {
                "one": {
                    "name": "Fashion Zigzag Stripe Fit and Flare Sleeveless Dress For Women",
                    "sku": "sk0004",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160707145718_97803.jpg",
                    "price": {
                        "symbol": "€",
                        "value": 20.46,
                        "code": "EUR"
                    },
                    "special_price": "",
                    "url": "/catalog/product/",
                    "product_id": "57c7da4af656f273013bf56e"
                },
                "two": {
                    "name": "Formal Evening Dress Sheath / Column One Shoulder Watteau Train Jersey with",
                    "sku": "po0001",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/r/nu/rnunew1467608090223.jpg",
                    "price": {
                        "symbol": "€",
                        "value": 113.46,
                        "code": "EUR"
                    },
                    "special_price": {
                        "symbol": "€",
                        "value": 112.53,
                        "code": "EUR"
                    },
                    "url": "/catalog/product/",
                    "product_id": "57e8d9a7f656f2e16b6234e5"
                }
            }
        ]
    }
}

```