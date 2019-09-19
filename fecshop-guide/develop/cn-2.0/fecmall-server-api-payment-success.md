Api- Payment Success
================

> 支付成功后，跳转到支付成功页面，访问的api

URL: `/payment/success`

格式：`json`

方式：`post`


一：请求部分
---------

#### 1.Request Header


| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 必须        |   String     | 从localStorage取出来的值，识别用户登录状态的标示，用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |
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
| 1500012         | order：无法从dbsession中获取order increment id                  | 



#### 4.返回数据举例：

各个字段的具体函数参看[fecshop-server-api-onepage.md](fecshop-server-api-onepage.md)


```
{
    "code": 200,
    "message": "process success",
    "data": { 
        "increment_id": "1100000909",       // 订单编号
        "order": {
            "order_id": 909,                // 订单id
            "increment_id": "1100000909",   // 订单编号
            "order_status": "processing",   //
            "store": "fecshop.appserver.fancyecommerce.com", //
            "created_at": 1509504001,       //
            "updated_at": 1509504001,       //
            "items_count": 1,               //
            "total_weight": "55.00",        //
            "order_currency_code": "EUR",   //
            "order_to_base_rate": "0.9300", //
            "grand_total": "125.60",        //
            "base_grand_total": "135.05",   //
            "subtotal": "4.70",             //
            "base_subtotal": "5.05",        //
            "subtotal_with_discount": "0.00",       //
            "base_subtotal_with_discount": "0.00",  //
            "is_changed": 1,                //
            "checkout_method": "standard",  //
            "customer_id": 46,              //
            "customer_group": null,         //
            "customer_email": "fdfd@3232.com",      //
            "customer_firstname": "2121",   //
            "customer_lastname": "2121",    //
            "customer_is_guest": 2,         //
            "remote_ip": null,              //
            "coupon_code": null,            //
            "payment_method": "paypal_standard",    //
            "shipping_method": "fast_shipping",     //
            "shipping_total": "120.90",     //
            "base_shipping_total": "130.00",//
            "customer_telephone": "2121",   //
            "customer_address_country": "AT",       //
            "customer_address_state": "NO", //
            "customer_address_city": "2121",//
            "customer_address_zip": "2121", //
            "customer_address_street1": "2121",     //
            "customer_address_street2": "2121",     //
            "txn_type": "cart",             //
            "txn_id": "6PT41125E9069713B",  //
            "payer_id": "FKL4V7D5GCACY",    //
            "ipn_track_id": null,           //
            "receiver_id": null,            //
            "verify_sign": null,            //
            "charset": null,                //
            "payment_fee": "3.99",          //
            "payment_type": "instant",      //
            "correlation_id": "4d88d1a3eb320",              //
            "base_payment_fee": "4.30",     //
            "protection_eligibility": "Eligible",           //
            //
            "protection_eligibility_type": "ItemNotReceivedEligible,UnauthorizedPaymentEligible",
            "secure_merchant_account_id": "H4KXD885J8LV2",  //
            "build": "40402625",            //
            "paypal_order_datetime": "1970-01-01 08:33:37", //
            "theme_type": null,             //
            "if_is_return_stock": 2,        //
            "payment_token": "EC-0WB612551K6101423",        //
            "version": 0,                   //
            "items": [
                {
                    "item_id": "936",
                    "store": "fecshop.appserver.fancyecommerce.com",
                    "order_id": "909",
                    "created_at": "1509504001",
                    "updated_at": "1509504001",
                    "product_id": "580835d0f656f240742f0b7c",
                    "sku": "p10001-kahaki-xl",
                    "name": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
                    "custom_option_sku": "",
                    "image": "/2/01/20160905101021_28071.jpg", //
                    "weight": "55.00",              //
                    "qty": "1",                     //
                    "row_weight": "55.00",          //
                    "price": "4.70",                //
                    "base_price": "4.70",           //
                    "row_total": "4.70",            //
                    "base_row_total": "5.05",       //
                    "redirect_url": "/raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122",
                    "spu_options": {                //
                        "color": "khaki",
                        "size": "XL",
                        "test3": "t_1"
                    },
                    "custom_option": [],
                    "custom_option_info": {         //
                        "color": "khaki",
                        "size": "XL",
                        "test3": "t_1"
                    }
                }
            ]
        }
    }
}
```