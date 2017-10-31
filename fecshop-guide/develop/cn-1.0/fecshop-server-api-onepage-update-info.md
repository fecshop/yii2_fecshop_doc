Api- Onepage 得到更新信息
================

> vue checkout onepage页面，在更改address后，shipping cost（运费）需要重新计算
> ，进而cart信息需要进一步计算。

URL: `/checkout/onepage/getshippingandcartinfo`

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
| country         | 必须        |   String     | country code     |
| address_id      | 必须        |   String     | 如果用户登录账户，使用的是保存的address信息，则这里需要传递address id   |
| state           | 必须        |   String     | 省/州信息        |
| shipping_method | 必须        |   String     | 快递物流简码     |

**请求参数示例如下：**

```
{
    country: "US",
    address_id: "",
    state: "AC",
    shipping_method:"fast_shipping"
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
        "cart_info": {
            "store": "fecshop.appserver.fancyecommerce.com",
            "items_count": 15,
            "coupon_code": null,
            "shipping_method": "fast_shipping",
            "payment_method": "paypal_standard",
            "grand_total": "127.38",
            "shipping_cost": "68.73",
            "coupon_cost": "0.00",
            "product_total": "58.65",
            "base_grand_total": "136.90",
            "base_shipping_cost": "73.90",
            "base_coupon_cost": "0.00",
            "base_product_total": "63.00",
            "products": [
                {
                    "item_id": 274,
                    "product_id": "580835d0f656f240742f0b7c",
                    "sku": "p10001-kahaki-xl",
                    "name": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
                    "qty": 15,
                    "custom_option_sku": "",
                    "product_price": 3.91,
                    "product_row_price": 58.650000000000006,
                    "base_product_price": 4.2,
                    "base_product_row_price": 63,
                    "product_name": {
                        "name_en": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
                        "name_fr": "",
                        "name_de": "",
                        "name_es": "",
                        "name_ru": "",
                        "name_pt": "",
                        "name_zh": "袖子信件印刷船员颈部运动衫kahaki xl"
                    },
                    "product_weight": 55,
                    "product_row_weight": 825,
                    "product_url": "/raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122",
                    "product_image": {
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
                    "custom_option": [],
                    "spu_options": {
                        "color": "khaki",
                        "size": "XL",
                        "test3": "t_1"
                    },
                    "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/100/100/2/01/20160905101021_28071.jpg",
                    "custom_option_info": {
                        "color": "khaki",
                        "size": "XL",
                        "test3": "t_1"
                    }
                }
            ],
            "product_weight": 825
        },
        "shippings": [
            {
                "method": "free_shipping",
                "label": "Free shipping( 7-20 work days)",
                "name": "HKBRAM",
                "cost": "0.00",
                "symbol": "€",
                "checked": "",
                "shipping_i": 1
            },
            {
                "method": "fast_shipping",
                "label": "Fast Shipping( 5-10 work days)",
                "name": "HKDHL",
                "cost": 68.73,
                "symbol": "€",
                "checked": true,
                "shipping_i": 2
            }
        ]
    }
}
```