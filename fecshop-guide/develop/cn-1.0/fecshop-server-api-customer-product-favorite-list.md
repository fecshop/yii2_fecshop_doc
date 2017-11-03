Api- Customer 产品收藏列表
================

> Customer account 账户中心，产品收藏列表页面的api

URL: `/customer/productfavorite/index`

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
| 1100003         | 登录：账户的token已经过期,或者没有登录                  | 



#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "productList": [
            {
                // product id
                "_id": {
                    "$oid": "581ae91ff656f20f052f0b77"
                },
                // product name
                "name": "Reindeer Pattern Glitter Christmas Dress",
                // product URL，这个是appfront 和apphtml5有效的url方式，vue不使用这个
                "url_key": "/reindeer-pattern-glitter-christmas-dress",
                // 价格
                "price": 22.68,
                // 特价
                "special_price": 21.68,
                // 特价开始时间
                "special_from": 0,
                // 特价结束时间
                "special_to": 0,
                // 图片
                "image": {
                    // 细节图
                    "gallery": [
                        {
                            "image": "/2/01/20161024170457_10036.jpg",
                            "label": "",
                            "sort_order": "",
                            "is_thumbnails": "1",
                            "is_detail": "1"
                        },
                        {
                            "image": "/2/01/20161024170457_13851.jpg",
                            "label": "",
                            "sort_order": "",
                            "is_thumbnails": "1",
                            "is_detail": "1"
                        },
                        {
                            "image": "/2/01/20161024170457_21098.jpg",
                            "label": "",
                            "sort_order": "",
                            "is_thumbnails": "1",
                            "is_detail": "1"
                        },
                        {
                            "image": "/2/01/20161101155240_56328.jpg",
                            "label": "",
                            "sort_order": "",
                            "is_thumbnails": "1",
                            "is_detail": "1"
                        },
                        {
                            "image": "/2/01/20161101155240_94256.jpg",
                            "label": "",
                            "sort_order": "",
                            "is_thumbnails": "1",
                            "is_detail": "1"
                        }
                    ],
                    // 主图
                    "main": {
                        "image": "/2/01/20161101155240_26690.jpg",
                        "label": "",
                        "sort_order": "",
                        "is_thumbnails": "1",
                        "is_detail": "1"
                    }
                },
                // 收藏更新时间
                "updated_at": "2017-09-28 11:04:19",
                // 收藏表id
                "favorite_id": "59cc66b3bfb7ae575337da64",
                // 产品主图
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20161101155240_26690.jpg",
                // 产品计算后的几个信息，因此上面的价格信息不要使用，直接使用下面计算好的价格信息即可。
                "price_info": {
                    "price": {
                        "symbol": "€",
                        "value": 21.1,
                        "code": "EUR"
                    },
                    "special_price": {
                        "symbol": "€",
                        "value": 20.17,
                        "code": "EUR"
                    }
                },
                "product_id": "581ae91ff656f20f052f0b77"
            },
            {
                "_id": {
                    "$oid": "57c3aaa9f656f24f353bf56e"
                },
                "name": "Paire de Bouton élégant Agrémentée évider Mesh Shape tricoté Boot poignets pour les femmes",
                "url_key": "/pair-of-stylish-button-embellished-hollow-out-mesh-shape-knitted-boot-cuffs-for-women",
                "price": 267.3,
                "special_price": 143.56,
                "special_from": 0,
                "special_to": 0,
                "image": {
                    "gallery": [
                        {
                            "image": "/2/01/20160722142719_96573.jpg",
                            "label": "",
                            "sort_order": "",
                            "is_thumbnails": "1",
                            "is_detail": "1"
                        }
                    ],
                    "main": {
                        "image": "/2/01/20160722142719_52348.jpg",
                        "label": "",
                        "sort_order": "",
                        "is_thumbnails": "1",
                        "is_detail": "1"
                    }
                },
                "updated_at": "2017-09-14 12:23:44",
                "favorite_id": "59b9fb15bfb7ae5c51016bd2",
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160722142719_52348.jpg",
                "price_info": {
                    "price": {
                        "symbol": "€",
                        "value": 248.59,
                        "code": "EUR"
                    },
                    "special_price": {
                        "symbol": "€",
                        "value": 133.52,
                        "code": "EUR"
                    }
                },
                "product_id": "57c3aaa9f656f24f353bf56e"
            }
        ],
        "count": 2,
        "numPerPage": null
    }
}
```