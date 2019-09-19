Api- 得到分类产品
================

> vue 分类页面，得到分类信息的api



URL: `/catalog/category/product`

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
| categoryId      | 必须        |   String     | 分类Id    |
| sortColumn      | 必须        |   String     | 分类产品的排序字段   |
| filterAttrs     | 必须        |   ARRAY      | 分类侧栏的属性过滤，没有属性过滤则填写空数组   |
| filterPrice     | 必须        |   String     | 分类侧栏价格过滤     |
| p               | 必须        |   Integer    | 页数  |

**请求参数示例如下：**

```
{
    categoryId:"57b6ac42f656f246653bf576",
    sortColumn:"review_count",
    filterAttrs:{"color":"multicolor","size":"M"},
    filterPrice:"20-30",
    p:2
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
| 1200000         | 分类：分类不存在                                   | 


#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "products": [
            {
                "one": {
                    // 分类产品name 
                    "name": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
                    // 分类产品sku
                    "sku": "p10001-kahaki-xl",
                    // 分类产品id
                    "_id": "580835d0f656f240742f0b7c",
                    // 分类产品图片
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160905101021_28071.jpg",
                    // 分类产品价格
                    "price": {
                        "symbol": "$",
                        "value": 6.05,
                        "code": "USD"
                    },
                    // 分类产品特价
                    "special_price": {
                        "symbol": "$",
                        "value": 5.05,
                        "code": "USD"A
                    },
                    // 分类产品Url
                    "url": "/catalog/product/580835d0f656f240742f0b7c",
                    "product_id": "p10001"
                },
                "two": {
                    "name": "Leaves Pattern Waisted Zippered Dress",
                    "sku": "sk10002",
                    "_id": "57d60c6cf656f2b57ddf9deb",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160723113745_77121.jpg",
                    "price": {
                        "symbol": "$",
                        "value": 33,
                        "code": "USD"
                    },
                    "special_price": "",
                    "url": "/catalog/product/57d60c6cf656f2b57ddf9deb",
                    "product_id": "sk10002"
                }
            },
            {
                "one": {
                    "name": "Floral Pattern Concealed Zipper High-Waist Dress",
                    "sku": "sk10003-001",
                    "_id": "57d611b4f656f20070df9deb",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160617104826_51885.jpg",
                    "price": {
                        "symbol": "$",
                        "value": 21,
                        "code": "USD"
                    },
                    "special_price": "",
                    "url": "/catalog/product/57d611b4f656f20070df9deb",
                    "product_id": "sk10003"
                },
                "two": {
                    "name": "Sweet Polka Dot Open Back Summer Dress For Women",
                    "sku": "sk0003",
                    "_id": "57c7da9af656f2577a3bf56e",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160804090311_12690.jpg",
                    "price": {
                        "symbol": "$",
                        "value": 33,
                        "code": "USD"
                    },
                    "special_price": "",
                    "url": "/catalog/product/57c7da9af656f2577a3bf56e",
                    "product_id": "sk0003"
                }
            },
            {
                "one": {
                    "name": "Pair of Stylish Button Embellished Hollow Out Mesh Shape Knitted Boot Cuffs For Women",
                    "sku": "sk2001-blue-zo",
                    "_id": "57c3aaa9f656f24f353bf56e",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160722142719_52348.jpg",
                    "price": {
                        "symbol": "$",
                        "value": 267.3,
                        "code": "USD"
                    },
                    "special_price": {
                        "symbol": "$",
                        "value": 143.56,
                        "code": "USD"
                    },
                    "url": "/catalog/product/57c3aaa9f656f24f353bf56e",
                    "product_id": "sk2001"
                },
                "two": {
                    "name": "Stylish Striped Criss-Cross Women's Dress",
                    "sku": "sk0008",
                    "_id": "57c7da1ef656f20c713bf56e",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160810112221_81491.jpg",
                    "price": {
                        "symbol": "$",
                        "value": 33,
                        "code": "USD"
                    },
                    "special_price": "",
                    "url": "/catalog/product/57c7da1ef656f20c713bf56e",
                    "product_id": "sk0008"
                }
            }
        ]
    }
}

```