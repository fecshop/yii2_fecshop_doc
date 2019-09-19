Api- Product Search
================

> 产品搜索页面使用的api

URL: `/catalogsearch/index/index`

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
| q               | 必须        |   String     | 查询的内容   |
| filterAttrs     | 必须        |   ARRAY      | 分类侧栏的属性过滤，没有属性过滤则填写空数组   |
| price           | 必须        |   String     | 分类侧栏价格过滤     |


**请求参数示例如下：**

```
{
    q: "dress",
    filterAttrs:{
        "color":"red"
    },
    price:"20-30"
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

#### 4.返回数据举例：

```
{
    "code": 200,
    "content": {
        "searchText": "dress",  // 搜索词
        "products": [ // 不需要注释了，都能看懂
            {
                "one": {
                    "name": "Reindeer Pattern Glitter Christmas Dress",
                    "sku": "22221",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20161101155240_26690.jpg",
                    "price": {
                        "symbol": "€",
                        "value": 21.1,
                        "code": "EUR"
                    },
                    "special_price": {
                        "symbol": "€",
                        "value": 20.17,
                        "code": "EUR"
                    },
                    "url": "/catalog/product/",
                    "product_id": "581ae91ff656f20f052f0b77"
                },
                "two": {
                    "name": "Leaves Pattern Waisted Zippered Dress",
                    "sku": "sk10002-002",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160723113749_21685.jpg",
                    "price": {
                        "symbol": "€",
                        "value": 20.46,
                        "code": "EUR"
                    },
                    "special_price": "",
                    "url": "/catalog/product/",
                    "product_id": "57d610e8f656f29808df9deb"
                }
            },
            {
                "one": {
                    "name": "Floral Pattern Concealed Zipper High-Waist Dress",
                    "sku": "sk10003-001",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160617104826_51885.jpg",
                    "price": {
                        "symbol": "€",
                        "value": 19.53,
                        "code": "EUR"
                    },
                    "special_price": "",
                    "url": "/catalog/product/",
                    "product_id": "57d611b4f656f20070df9deb"
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
                    "name": "Reindeer Pattern Glitter Christmas Dress222",
                    "sku": "222212",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20161024170457_10036.jpg",
                    "price": {
                        "symbol": "€",
                        "value": 21.39,
                        "code": "EUR"
                    },
                    "special_price": {
                        "symbol": "€",
                        "value": 17.67,
                        "code": "EUR"
                    },
                    "url": "/catalog/product/",
                    "product_id": "581c6833f656f2042f2f0b77"
                }
            }
        ],
        "refine_by_info": [
            {
                "attr": "clearAll",
                "val": "clear all"
            },
            {
                "attr": "price",
                "val": "20-30"
            }
        ],
        "filter_info": {
            "color": {
                "label": "color",
                "items": [
                    {
                        "_id": "red",
                        "count": 1,
                        "selected": false
                    },
                    {
                        "_id": "multicolor",
                        "count": 1,
                        "selected": false
                    },
                    {
                        "_id": "",
                        "count": 3,
                        "selected": false
                    },
                    {
                        "_id": "white & black",
                        "count": 1,
                        "selected": false
                    }
                ]
            },
            "size": {
                "label": "size",
                "items": [
                    {
                        "_id": "L",
                        "count": 1,
                        "selected": false
                    },
                    {
                        "_id": "",
                        "count": 4,
                        "selected": false
                    },
                    {
                        "_id": "S",
                        "count": 1,
                        "selected": false
                    }
                ]
            }
        },
        "filter_price": {
            "price": [
                {
                    "selected": false,
                    "label": "---€10",
                    "val": "0-10"
                },
                {
                    "selected": false,
                    "label": "€10---€20",
                    "val": "10-20"
                },
                {
                    "selected": true,
                    "label": "€20---€30",
                    "val": "20-30"
                },
                {
                    "selected": false,
                    "label": "€30---€50",
                    "val": "30-50"
                },
                {
                    "selected": false,
                    "label": "€50---€100",
                    "val": "50-100"
                },
                {
                    "selected": false,
                    "label": "€100---€150",
                    "val": "100-150"
                },
                {
                    "selected": false,
                    "label": "€150---€300",
                    "val": "150-300"
                },
                {
                    "selected": false,
                    "label": "€300---€500",
                    "val": "300-500"
                },
                {
                    "selected": false,
                    "label": "€500---€1000",
                    "val": "500-1000"
                },
                {
                    "selected": false,
                    "label": "€1000---",
                    "val": "1000-"
                }
            ]
        }
    }
}
```