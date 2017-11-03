Api- Product 详细信息
================

> vue 分类页面，得到分类信息的api

URL: `/catalog/product/index`

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


| 参数名称        | 是否必须    |  类型       |  描述         |
| ----------------| -----:      | :----:      |:----:         |
| product_id      | 必须        |   String    | Product Id    |


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

#### 3.参数code所有返回状态码：（完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md) ）

| code Value      |        描述                                        |
| ----------------| --------------------------------------------------:| 
| 200             | 成功状态码                                         |  
| 1300001         | 产品：产品不存在，或者已经下架                  | 





#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "product": {
            "name": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
            "sku": "p10001-kahaki-xl",
            "spu": "p10001",
            // 细节图
            "thumbnail_img": [
                "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/400/0/2/01/20160905101021_28071.jpg",
                "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/400/0/2/01/20160905101021_56532.jpg",
                "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/400/0/2/01/20160905101022_25969.jpg",
                "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/400/0/2/01/20160905101022_79159.jpg",
                "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/400/0/2/01/20160905101021_28071147710702992998.jpg",
                "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/400/0/2/01/20160905101021_28071147710703579813.jpg"
            ],
            // 产品评论信息
            "productReview": {
                "_id": {
                    "$oid": "580835d0f656f240742f0b7c"
                },
                "spu": "p10001",
                "review_count": 1,
                "coll": [
                    {
                        "_id": {
                            "$oid": "5818086ff656f20f292f0b77"
                        },
                        "product_spu": "p10001",
                        "product_id": "580835d0f656f240742f0b7c",
                        "rate_star": "3",  // 评论星级
                        "name": "terr fdf",
                        "user_id": 17,
                        "ip": "119.123.79.199",
                        "summary": "fdsfds", // 评论标题
                        "review_content": "fdsaf", // 评论内容
                        "review_date": 1477970031, // 评论日期
                        "store": "fecshop.appfront.fancyecommerce.com/fr",
                        "lang_code": "fr",
                        "status": 1,
                        "audit_user": 2,
                        "audit_date": 1477970038
                    }
                ],
                "noActiveStatus": 10
            },
            // 显示图图片的自定义属性
            "custom_option_showImg_attr": "my_color",
            // 在描述部分显示的图片
            "image_detail": [
                "//img.fancyecommerce.com/media/catalog/product/2/01/20160905101021_56532.jpg",
                "//img.fancyecommerce.com/media/catalog/product/2/01/20160905101022_25969.jpg",
                "//img.fancyecommerce.com/media/catalog/product/2/01/20160905101022_79159.jpg",
                "//img.fancyecommerce.com/media/catalog/product/2/01/20160905101021_28071147710702992998.jpg",
                "//img.fancyecommerce.com/media/catalog/product/2/01/20160905101021_28071147710703579813.jpg",
                "//img.fancyecommerce.com/media/catalog/product/2/01/20160905101021_28071.jpg"
            ],
            // 产品所属的属性组
            "attr_group": "men_group",
            // 产品评论数
            "review_count": 1,
            // 产品星级平均值
            "reviw_rate_star_average": 3,
            // 产品价格信息
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
            // 产品tier price 信息
            "tier_price": [
                [
                    "Qty:",
                    "3-5",
                    "5-8",
                    ">=8"
                ],
                [
                    "Price:",
                    "€4.47",
                    "€4.19",
                    "€3.91"
                ]
            ],
            // spu options部分
            "options": [
                {
                    "label": "color",
                    "value": [
                        {
                            "attr_val": "black",
                            "active": "active",
                            "_id": {
                                "$oid": "5808352af656f23f742f0b7a"
                            },
                            "name": {
                                "name_en": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt",
                                "name_fr": "",
                                "name_de": "",
                                "name_es": "",
                                "name_ru": "",
                                "name_pt": "",
                                "name_zh": "袖子信件印刷船员脖子运动衫"
                            },
                            "url_key": "/raglan-sleeves-letter-printed-crew-neck-sweatshirt-61337464",
                            "image": {
                                "gallery": [
                                    {
                                        "image": "/2/01/20161007110608_50811.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    }
                                ],
                                "main": {
                                    "image": "/2/01/20161007110608_78124.jpg",
                                    "label": "",
                                    "sort_order": "",
                                    "is_thumbnails": "1",
                                    "is_detail": "1"
                                }
                            },
                            "color": "black",
                            "size": "XL",
                            "test3": "t_1",
                            "main_img": "/2/01/20161007110608_78124.jpg",
                            "url": "/catalog/product/5808352af656f23f742f0b7a",
                            "show_as_img": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/50/55/2/01/20161007110608_78124.jpg"
                        },
                        {
                            "attr_val": "khaki",
                            "active": "current",
                            "_id": {
                                "$oid": "580835d0f656f240742f0b7c"
                            },
                            "name": {
                                "name_en": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
                                "name_fr": "",
                                "name_de": "",
                                "name_es": "",
                                "name_ru": "",
                                "name_pt": "",
                                "name_zh": "袖子信件印刷船员颈部运动衫kahaki xl"
                            },
                            "url_key": "/raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122",
                            "image": {
                                "gallery": [
                                    {
                                        "image": "/2/01/20160905101021_56532.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101022_25969.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101022_79159.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101021_28071147710702992998.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101021_28071147710703579813.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    }
                                ],
                                "main": {
                                    "image": "/2/01/20160905101021_28071.jpg",
                                    "label": "",
                                    "sort_order": "",
                                    "is_thumbnails": "1",
                                    "is_detail": "1"
                                }
                            },
                            "color": "khaki",
                            "size": "XL",
                            "test3": "t_1",
                            "main_img": "/2/01/20160905101021_28071.jpg",
                            "url": "/catalog/product/580835d0f656f240742f0b7c",
                            "show_as_img": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/50/55/2/01/20160905101021_28071.jpg"
                        }
                    ]
                },
                {
                    "label": "size",
                    "value": [
                        {
                            "attr_val": "S",
                            "active": "noactive"
                        },
                        {
                            "attr_val": "M",
                            "active": "noactive"
                        },
                        {
                            "attr_val": "L",
                            "active": "noactive"
                        },
                        {
                            "attr_val": "XL",
                            "active": "current",
                            "_id": {
                                "$oid": "580835d0f656f240742f0b7c"
                            },
                            "name": {
                                "name_en": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
                                "name_fr": "",
                                "name_de": "",
                                "name_es": "",
                                "name_ru": "",
                                "name_pt": "",
                                "name_zh": "袖子信件印刷船员颈部运动衫kahaki xl"
                            },
                            "url_key": "/raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122",
                            "image": {
                                "gallery": [
                                    {
                                        "image": "/2/01/20160905101021_56532.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101022_25969.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101022_79159.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101021_28071147710702992998.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101021_28071147710703579813.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    }
                                ],
                                "main": {
                                    "image": "/2/01/20160905101021_28071.jpg",
                                    "label": "",
                                    "sort_order": "",
                                    "is_thumbnails": "1",
                                    "is_detail": "1"
                                }
                            },
                            "color": "khaki",
                            "size": "XL",
                            "test3": "t_1",
                            "main_img": "/2/01/20160905101021_28071.jpg",
                            "url": "/catalog/product/580835d0f656f240742f0b7c"
                        },
                        {
                            "attr_val": "XXL",
                            "active": "active",
                            "_id": {
                                "$oid": "59290098bfb7ae30f71ad893"
                            },
                            "name": {
                                "name_en": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xxl",
                                "name_fr": "",
                                "name_de": "",
                                "name_es": "",
                                "name_ru": "",
                                "name_pt": "",
                                "name_zh": "袖子信件印刷船员脖子运动衫"
                            },
                            "url_key": "/raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122-48242124-96569912",
                            "image": {
                                "gallery": [
                                    {
                                        "image": "/2/01/20160905101021_56532.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101022_25969.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101022_79159.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    }
                                ],
                                "main": {
                                    "image": "/2/01/20160905101021_28071.jpg",
                                    "label": "",
                                    "sort_order": "",
                                    "is_thumbnails": "1",
                                    "is_detail": "1"
                                }
                            },
                            "color": "khaki",
                            "size": "XXL",
                            "test3": "t_1",
                            "main_img": "/2/01/20160905101021_28071.jpg",
                            "url": "/catalog/product/59290098bfb7ae30f71ad893"
                        }
                    ]
                },
                {
                    "label": "test3",
                    "value": [
                        {
                            "attr_val": "t_1",
                            "active": "current",
                            "_id": {
                                "$oid": "580835d0f656f240742f0b7c"
                            },
                            "name": {
                                "name_en": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
                                "name_fr": "",
                                "name_de": "",
                                "name_es": "",
                                "name_ru": "",
                                "name_pt": "",
                                "name_zh": "袖子信件印刷船员颈部运动衫kahaki xl"
                            },
                            "url_key": "/raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122",
                            "image": {
                                "gallery": [
                                    {
                                        "image": "/2/01/20160905101021_56532.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101022_25969.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101022_79159.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101021_28071147710702992998.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    },
                                    {
                                        "image": "/2/01/20160905101021_28071147710703579813.jpg",
                                        "label": "",
                                        "sort_order": "",
                                        "is_thumbnails": "1",
                                        "is_detail": "1"
                                    }
                                ],
                                "main": {
                                    "image": "/2/01/20160905101021_28071.jpg",
                                    "label": "",
                                    "sort_order": "",
                                    "is_thumbnails": "1",
                                    "is_detail": "1"
                                }
                            },
                            "color": "khaki",
                            "size": "XL",
                            "test3": "t_1",
                            "main_img": "/2/01/20160905101021_28071.jpg",
                            "url": "/catalog/product/580835d0f656f240742f0b7c"
                        },
                        {
                            "attr_val": "t_2",
                            "active": "noactive"
                        },
                        {
                            "attr_val": "t_4",
                            "active": "noactive"
                        }
                    ]
                }
            ],
            "custom_option": [],
            // 产品描述
            "description": "<div style=\"font-family:Tahoma;\">        <strong>Specification</strong><br />        <ul><li><strong>Color:</strong> BLACK, GRAY</li><li><strong>Size:</strong> M, L, XL, 2XL</li><li><strong>Category:</strong> Men &gt; Hoodies &amp; Sweatshirts &gt; Sweatshirts</li></ul></div>                        <br />                                                <br /><div>  </div><div class=\"xxkkk\">    <div class=\"xxkkk20\">            <strong>Material:</strong> Polyester <br />             <strong>Clothing Length:</strong> Regular <br />             <strong>Sleeve Length:</strong> Full <br />             <strong>Style:</strong> Casual <br />             <strong>Weight:</strong> 0.326kg <br />             <strong>Package Contents:</strong> 1 x Sweatshirt             </div>    </div>",
            "_id": "580835d0f656f240742f0b7c",
            // 买了的人还买了哪些产品
            "buy_also_buy": [
                {
                    "one": {
                        "name": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xxl",
                        "sku": "p10001-kahaki-xxl",
                        "_id": "",
                        "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/01/20160905101021_28071.jpg",
                        "price": {
                            "symbol": "€",
                            "value": 5.63,
                            "code": "EUR"
                        },
                        "special_price": {
                            "symbol": "€",
                            "value": 4.7,
                            "code": "EUR"
                        },
                        "url": "/catalog/product/580835edf656f26e122f0b79",
                        "product_id": "580835edf656f26e122f0b79"
                    },
                    "two": {
                        "name": "test computer",
                        "sku": "computer001-xinghao2-cpu2",
                        "_id": "",
                        "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/2/22/222147807273862010.jpg",
                        "price": {
                            "symbol": "€",
                            "value": 30.69,
                            "code": "EUR"
                        },
                        "special_price": "",
                        "url": "/catalog/product/581994c6f656f28b2a2f0b79",
                        "product_id": "581994c6f656f28b2a2f0b79"
                    }
                },
                {
                    "one": {
                        "name": "test computer",
                        "sku": "computer001-xinghao1-cpu1",
                        "_id": "",
                        "image": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/296/0/1/11/111.jpg",
                        "price": {
                            "symbol": "€",
                            "value": 30.69,
                            "code": "EUR"
                        },
                        "special_price": "",
                        "url": "/catalog/product/5819941ef656f28a2a2f0b77",
                        "product_id": "5819941ef656f28a2a2f0b77"
                    },
                    "two": []
                }
            ]
        }
    }
}
```