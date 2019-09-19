Api- 得到分类信息
==============

> vue 分类页面，得到分类信息的api



URL: `/catalog/category/index`

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
| categoryId      | 必须       |   String     | 分类Id    |
| sortColumn      | 必须       |   String     | 分类产品的排序字段   |
| filterAttrs     | 必须       |   ARRAY      | 分类侧栏的属性过滤，没有属性过滤则填写空数组   |
| filterPrice     | 必须       |   String     | 分类侧栏价格过滤     |


**请求参数示例如下：**

```
{
    categoryId:"57b6ac42f656f246653bf576",
    sortColumn:"review_count",
    filterAttrs:{"color":"multicolor","size":"M"},
    filterPrice:"20-30"
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
| code            | 必须        |   Number    | 返回状态码，200 代表完成，完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md)  |
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
        "name": "Men", // 分类的name
        "title": null, // 分类的title
        "image": "",   // 分类的图片（有时候在分类页面，内容部分的顶部会搞个宣传图）
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
                    "name": "Bell Sleeve Off The Shoulder Lace Splicing Blouse",
                    "sku": "32332",
                    "_id": "57bac59ef656f24f123bf56e",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/1/14/11471858072718.jpg",
                    "price": {
                        "symbol": "$",
                        "value": 22,
                        "code": "USD"
                    },
                    "special_price": "",
                    "url": "/catalog/product/57bac59ef656f24f123bf56e",
                    "product_id": "323232"
                }
            },
            {
                "one": {
                    "name": "Round Neck Floral 3D Print Pattern Short Sleeve Men's T-Shirt",
                    "sku": "men0003",
                    "_id": "57d6307df656f2b018df9deb",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160425122144_71146.jpg",
                    "price": {
                        "symbol": "$",
                        "value": 35,
                        "code": "USD"
                    },
                    "special_price": {
                        "symbol": "$",
                        "value": 21,
                        "code": "USD"
                    },
                    "url": "/catalog/product/57d6307df656f2b018df9deb",
                    "product_id": "men0003"
                },
                "two": {
                    "name": "Round Neck 3D Colorful Splash-Ink Print Short Sleeve Men's T-Shirt",
                    "sku": "men0002",
                    "_id": "57d62e84f656f2b57ddf9def",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160525142537_74758.jpg",
                    "price": {
                        "symbol": "$",
                        "value": 12,
                        "code": "USD"
                    },
                    "special_price": "",
                    "url": "/catalog/product/57d62e84f656f2b57ddf9def",
                    "product_id": "men0002"
                }
            },
            {
                "one": {
                    "name": "Round Neck Printed Short Sleeve Men's T-Shirt",
                    "sku": "men0001",
                    "_id": "57d61555f656f29808df9ded",
                    "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160624120255_80096.jpg",
                    "price": {
                        "symbol": "$",
                        "value": 33,
                        "code": "USD"
                    },
                    "special_price": "",
                    "url": "/catalog/product/57d61555f656f29808df9ded",
                    "product_id": "men0001"
                },
                "two": []
            }
        ],
        "query_item": {
            "frontNumPerPage": [],
            "frontSort": [
                {
                    "label": "Hot",
                    "value": "hot",
                    "selected": false
                },
                {
                    "label": "Review",
                    "value": "review_count",
                    "selected": true
                },
                {
                    "label": "Favorite",
                    "value": "favorite_count",
                    "selected": false
                },
                {
                    "label": "New",
                    "value": "new",
                    "selected": false
                },
                {
                    "label": "$ Low to High",
                    "value": "low-to-high",
                    "selected": false
                },
                {
                    "label": "$ High to Low",
                    "value": "high-to-low",
                    "selected": false
                }
            ]
        },
        "refine_by_info": [],
        "filter_info": {
            "color": {
                "label": "color",
                "items": [
                    {
                        "_id": "khaki",
                        "count": 5,
                        "selected": false
                    },
                    {
                        "_id": "multicolor",
                        "count": 2,
                        "selected": false
                    },
                    {
                        "_id": "black",
                        "count": 5,
                        "selected": false
                    }
                ]
            },
            "size": {
                "label": "size",
                "items": [
                    {
                        "_id": "S",
                        "count": 1,
                        "selected": false
                    },
                    {
                        "_id": "L",
                        "count": 2,
                        "selected": false
                    },
                    {
                        "_id": "XXL",
                        "count": 2,
                        "selected": false
                    },
                    {
                        "_id": "XL",
                        "count": 3,
                        "selected": false
                    },
                    {
                        "_id": "M",
                        "count": 4,
                        "selected": false
                    }
                ]
            },
            "style": {
                "label": "style",
                "items": [
                    {
                        "_id": "Work",
                        "count": 8,
                        "selected": false
                    },
                    {
                        "_id": "Bohemian",
                        "count": 1,
                        "selected": false
                    },
                    {
                        "_id": "Cute",
                        "count": 3,
                        "selected": false
                    }
                ]
            },
            "dresses-length": {
                "label": "dresses Length",
                "items": [
                    {
                        "_id": "",
                        "count": 12,
                        "selected": false
                    }
                ]
            },
            "pattern-type": {
                "label": "pattern Type",
                "items": [
                    {
                        "_id": "Leopard ",
                        "count": 1,
                        "selected": false
                    },
                    {
                        "_id": "Floral",
                        "count": 1,
                        "selected": false
                    },
                    {
                        "_id": "Letter",
                        "count": 10,
                        "selected": false
                    }
                ]
            },
            "sleeve-length": {
                "label": "sleeve Length",
                "items": [
                    {
                        "_id": "Short-Sleeves",
                        "count": 12,
                        "selected": false
                    }
                ]
            },
            "collar": {
                "label": "collar",
                "items": [
                    {
                        "_id": "V-Neck",
                        "count": 1,
                        "selected": false
                    },
                    {
                        "_id": "Round Neck",
                        "count": 11,
                        "selected": false
                    }
                ]
            }
        },
        "filter_price": {
            "price": [
                {
                    "selected": false,
                    "label": "---$10",
                    "val": "0-10"
                },
                {
                    "selected": false,
                    "label": "$10---$20",
                    "val": "10-20"
                },
                {
                    "selected": false,
                    "label": "$20---$30",
                    "val": "20-30"
                },
                {
                    "selected": false,
                    "label": "$30---$50",
                    "val": "30-50"
                },
                {
                    "selected": false,
                    "label": "$50---$100",
                    "val": "50-100"
                },
                {
                    "selected": false,
                    "label": "$100---$150",
                    "val": "100-150"
                },
                {
                    "selected": false,
                    "label": "$150---$300",
                    "val": "150-300"
                },
                {
                    "selected": false,
                    "label": "$300---$500",
                    "val": "300-500"
                },
                {
                    "selected": false,
                    "label": "$500---$1000",
                    "val": "500-1000"
                },
                {
                    "selected": false,
                    "label": "$1000---",
                    "val": "1000-"
                }
            ]
        },
        "filter_category": {
            "57beb692f656f24e623bf578": {
                "name": "Shirts",
                "url_key": "/shirts",
                "parent_id": "57b6ac42f656f246653bf576",
                "current": false,
                "url": "catalog/category/57beb692f656f24e623bf578"
            },
            "57beb6a0f656f275313bf580": {
                "name": "Shorts",
                "url_key": "/shorts",
                "parent_id": "57b6ac42f656f246653bf576",
                "current": false,
                "url": "catalog/category/57beb6a0f656f275313bf580"
            }
        },
        "page_count": 1
    }
}

```