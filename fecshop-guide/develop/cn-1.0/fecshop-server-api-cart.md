Api- 得到Cart信息
================

> vue Cart页面，得到Cart信息的api



URL: `/checkout/cart/index`

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
| code            | 必须        |   Number    | 返回状态码，200 代表完成，完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md)  |
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
            "items_count": 2,
            "coupon_code": null,
            "shipping_method": "fast_shipping",
            "payment_method": null,
            "grand_total": "27.05",
            "shipping_cost": "0.00",
            "coupon_cost": "0.00",
            "product_total": "27.05",
            "base_grand_total": "27.05",
            "base_shipping_cost": "0.00",
            "base_coupon_cost": "0.00",
            "base_product_total": "27.05",
            "products": [
                {
                    "item_id": 391,
                    "product_id": "57c7da4af656f273013bf56e",
                    "sku": "sk0004",
                    "name": "Fashion Zigzag Stripe Fit and Flare Sleeveless Dress For Women",
                    "qty": 1,
                    "custom_option_sku": "",
                    "product_price": 22,
                    "product_row_price": 22,
                    "base_product_price": 22,
                    "base_product_row_price": 22,
                    "product_weight": 0,
                    "product_row_weight": 0,
                    "product_url": "/fashion-zigzag-stripe-fit-and-flare-sleeveless-dress-for-women",
                    "custom_option": [],
                    "spu_options": {
                        "color": "white & black",
                        "size": "S"
                    },
                    "img_url": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/150/150/2/01/20160707145718_97803.jpg",
                    "url": "/catalog/product/57c7da4af656f273013bf56e",
                    "custom_option_info": {
                        "color": "white & black",
                        "size": "S"
                    }
                },
                {
                    "item_id": 394,
                    "product_id": "580835d0f656f240742f0b7c",
                    "sku": "p10001-kahaki-xl",
                    "name": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
                    "qty": 1,
                    "custom_option_sku": "",
                    "product_price": 5.05,
                    "product_row_price": 5.05,
                    "base_product_price": 5.05,
                    "base_product_row_price": 5.05,
                    "product_weight": 55,
                    "product_row_weight": 55,
                    "product_url": "/raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122",
                    "custom_option": [],
                    "spu_options": {
                        "color": "khaki",
                        "size": "XL",
                        "test3": "t_1"
                    },
                    "img_url": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/150/150/2/01/20160905101021_28071.jpg",
                    "url": "/catalog/product/580835d0f656f240742f0b7c",
                    "custom_option_info": {
                        "color": "khaki",
                        "size": "XL",
                        "test3": "t_1"
                    }
                }
            ],
            "product_weight": 55
        },
        "currency": {
            "code": "USD",
            "rate": 1,
            "symbol": "$"
        }
    }
}
```