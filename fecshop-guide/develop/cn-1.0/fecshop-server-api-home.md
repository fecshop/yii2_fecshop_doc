Api- Home 得到首页信息
================

> vue 分类页面，得到分类信息的api

URL: `/cms/home/index`

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

无

**请求参数示例如下：**

```
无
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

#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "productList": [ // 产品信息
            {
                "one": {
                    "name": "Paire de Bouton élégant Agrémentée évider Mesh Shape tricoté Boot poignets pour les femmes",
                    "sku": "sk2001-blue-zo",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160722142719_52348.jpg",
                    "price": {
                        "symbol": "€",
                        "value": 248.59,
                        "code": "EUR"
                    },
                    "special_price": {
                        "symbol": "€",
                        "value": 133.52,
                        "code": "EUR"
                    },
                    "url": "/catalog/product/57c3aaa9f656f24f353bf56e",
                    "product_id": "57c3aaa9f656f24f353bf56e"
                },
                "two": {
                    "name": "Stylish Striped Criss-Cross Women's Dress",
                    "sku": "sk0008",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160810112221_81491.jpg",
                    "price": {
                        "symbol": "€",
                        "value": 30.69,
                        "code": "EUR"
                    },
                    "special_price": "",
                    "url": "/catalog/product/57c7da1ef656f20c713bf56e",
                    "product_id": "57c7da1ef656f20c713bf56e"
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
                    "url": "/catalog/product/57c7da4af656f273013bf56e",
                    "product_id": "57c7da4af656f273013bf56e"
                },
                "two": {
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
                    "url": "/catalog/product/57c7da9af656f2577a3bf56e",
                    "product_id": "57c7da9af656f2577a3bf56e"
                }
            },
            {
                "one": {
                    "name": "Spaghetti Strap Print Backless Bodycon Dress",
                    "sku": "sk0002",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160606112453_71094147323202778861.JPG",
                    "price": {
                        "symbol": "€",
                        "value": 30.69,
                        "code": "EUR"
                    },
                    "special_price": "",
                    "url": "/catalog/product/57c7daecf656f273013bf570",
                    "product_id": "57c7daecf656f273013bf570"
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
                    "url": "/catalog/product/57bac5c6f656f2940a3bf570",
                    "product_id": "57bac5c6f656f2940a3bf570"
                }
            },
            {
                "one": {
                    "name": "Bell Sleeve Off The Shoulder Lace Splicing Blouse",
                    "sku": "32332",
                    "_id": "",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/1/14/11471858072718.jpg",
                    "price": {
                        "symbol": "€",
                        "value": 20.46,
                        "code": "EUR"
                    },
                    "special_price": "",
                    "url": "/catalog/product/57bac59ef656f24f123bf56e",
                    "product_id": "57bac59ef656f24f123bf56e"
                },
                "two": []
            }
        ],
        "advertiseImg": { //广告信息
            "bigImgList": [
                {
                    "imgUrl": "//img.apphtml5.fancyecommerce.com/custom/home_img_1.jpg"
                },
                {
                    "imgUrl": "//img.apphtml5.fancyecommerce.com/custom/home_img_2.jpg"
                },
                {
                    "imgUrl": "//img.apphtml5.fancyecommerce.com/custom/home_img_3.jpg"
                }
            ],
            "smallImgList": [
                {
                    "imgUrl": "//img.apphtml5.fancyecommerce.com/custom/home_small_1.jpg"
                },
                {
                    "imgUrl": "//img.apphtml5.fancyecommerce.com/custom/home_small_2.jpg"
                }
            ]
        },
        "language": { // 语言信息
            "langList": [
                {
                    "code": "fr",
                    "language": "fr_FR",
                    "languageName": "Français"
                },
                {
                    "code": "en",
                    "language": "en_US",
                    "languageName": "English"
                },
                {
                    "code": "es",
                    "language": "es_ES",
                    "languageName": "Español"
                },
                {
                    "code": "zh",
                    "language": "zh_CN",
                    "languageName": "中文"
                }
            ],
            "currentLang": "fr"
        },
        "currency": {  // 货币信息
            "currencyList": {
                "EUR": {
                    "code": "EUR",
                    "rate": 0.93,
                    "symbol": "€"
                },
                "USD": {
                    "code": "USD",
                    "rate": 1,
                    "symbol": "$"
                },
                "GBP": {
                    "code": "GBP",
                    "rate": 0.8,
                    "symbol": "£"
                },
                "CNY": {
                    "code": "CNY",
                    "rate": 6.87,
                    "symbol": "￥"
                }
            },
            "currentCurrency": "EUR"
        }
    }
}
```