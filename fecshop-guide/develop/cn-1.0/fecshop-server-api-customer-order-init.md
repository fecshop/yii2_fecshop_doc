Api- Customer Order 列表
================

> vue 分类页面，得到分类信息的api

URL: `/customer/order/index`

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
| p               | 选填        |   Integer    | 页数  |

**请求参数示例如下：**

```
{
    p:1
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
| 1100003         | 登录：账户的token已经过期,或者没有登录                  | 



#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "orderList": [
            {
                "order_id": "883",                  // order id
                "increment_id": "1100000883",       // 订单编号
                "order_status": "processing",       //  订单状态
                "created_at": "2017-10-26 16:41:58",// 创建时间
                "items_count": "1",                 // 订单产品总数
                "total_weight": "55.00",            // 订单总重量
                "order_currency_code": "CNY",       // 订单货币
                "order_to_base_rate": "6.8700",     // 订单货币和基础货币的汇率
                "grand_total": "542.40",            // 订单的当前货币金额
                "base_grand_total": "78.95",        // 订单的基础货币金额
                "subtotal": "34.70",                // 订单的所有产品的当前货币总额
                "base_subtotal": "5.05",            // 订单的所有产品的基础货币总额
                "subtotal_with_discount": "0.00",   // 订单的当前货币的折扣金额
                "base_subtotal_with_discount": "0.00",   // 订单的基础货币的折扣金额
                "checkout_method": "standard",      // 订单的支付方式（标准支付还是快捷支付）
                "customer_id": "46",                // 用户的id
                "customer_group": null,             // 用户组
                "customer_email": "2358269014@qq.com",   // 用户的email
                "customer_firstname": "fdsafasd",   // 用户的first name
                "customer_lastname": "32423423432", // 用户的last name
                "customer_is_guest": "2",           // 用户是否是游客，1代表是游客，2代表是登录用户
                "coupon_code": null,                // 优惠卷码
                "payment_method": "alipay_standard",// 支付方式
                "shipping_method": "fast_shipping", // 货运方式 
                "shipping_total": "507.70",         // 订单当前货币运费
                "base_shipping_total": "73.90",     // 订单基础货币运费
                "customer_telephone": "312321",     // 用户电话
                "customer_address_country": "US",   // 国家
                "customer_address_state": "FL",     // 省
                "customer_address_city": "321312",  // 城市
                "customer_address_zip": "123123",   // 邮编
                "customer_address_street1": "321312",   // 街道详细1
                "customer_address_street2": "3213", // 街道详细2
                "currency_symbol":"€"               // 订单货币符号
                
            }, 
            // 数据格式看第一组数据，下面的不要看了，统一以第一组为准。
            {
                "order_id": "882",
                "increment_id": "1100000882",
                "order_status": "pending",
                "store": "fecshop.appserver.fancyecommerce.com",
                "created_at": "2017-10-26 16:26:56",
                "updated_at": "1509006416",
                "items_count": "1",
                "total_weight": "55.00",
                "order_currency_code": "USD",
                "order_to_base_rate": "1.0000",
                "grand_total": "78.96",
                "base_grand_total": "78.95",
                "subtotal": "5.05",
                "base_subtotal": "5.05",
                "subtotal_with_discount": "0.00",
                "base_subtotal_with_discount": "0.00",
                "is_changed": "1",
                "checkout_method": "standard",
                "customer_id": "46",
                "customer_group": null,
                "customer_email": "2358269014@qq.com",
                "customer_firstname": "fdsafasd",
                "customer_lastname": "32423423432",
                "customer_is_guest": "2",
                "remote_ip": null,
                "coupon_code": null,
                "payment_method": "check_money",
                "shipping_method": "fast_shipping",
                "shipping_total": "73.91",
                "base_shipping_total": "73.90",
                "customer_telephone": "312321",
                "customer_address_country": "US",
                "customer_address_state": "FL",
                "customer_address_city": "321312",
                "customer_address_zip": "123123",
                "customer_address_street1": "321312",
                
            },
            {
                "order_id": "881",
                "increment_id": "1100000881",
                "order_status": "processing",
                "store": "fecshop.appserver.fancyecommerce.com",
                "created_at": "2017-10-26 16:09:07",
                "updated_at": "1509005347",
                "items_count": "2",
                "total_weight": "110.00",
                "order_currency_code": "USD",
                "order_to_base_rate": "1.0000",
                "grand_total": "84.01",
                "base_grand_total": "84.00",
                "subtotal": "10.10",
                "base_subtotal": "10.10",
                "subtotal_with_discount": "0.00",
                "base_subtotal_with_discount": "0.00",
                "is_changed": "1",
                "checkout_method": "express",
                "customer_id": "46",
                "customer_group": null,
                "customer_email": "zqy234api1-facilitator-1@126.com",
                "customer_firstname": "test",
                "customer_lastname": "facilitator",
                "customer_is_guest": "1",
                "remote_ip": null,
                "coupon_code": null,
                "payment_method": "paypal_express",
                "shipping_method": "fast_shipping",
                "shipping_total": "73.91",
                "base_shipping_total": "73.90",
                "customer_telephone": "3232",
                "customer_address_country": "US",
                "customer_address_state": "NY",
                "customer_address_city": "New York",
                "customer_address_zip": "10021",
                "customer_address_street1": "4114 Sepulveda Blvd.",
                "customer_address_street2": "4114 Sepulveda Blvd.",
                "txn_type": "cart",
                "txn_id": "7C392389HD224815W",
                "payer_id": "FKL4V7D5GCACY",
                "ipn_track_id": null,
                "receiver_id": null,
                "verify_sign": null,
                "charset": null,
                "payment_fee": "2.74",
                "payment_type": "instant",
                "correlation_id": "9a55941f7c361",
                "base_payment_fee": "2.74",
                "protection_eligibility": "Ineligible",
                "protection_eligibility_type": "None",
                "secure_merchant_account_id": "H4KXD885J8LV2",
                "build": "39972400",
                "paypal_order_datetime": "1970-01-01 08:33:37",
                "theme_type": null,
                "if_is_return_stock": "2",
                "payment_token": "EC-9N923514H43490543",
                "version": "1"
            },
            {
                "order_id": "880",
                "increment_id": "1100000880",
                "order_status": "pending",
                "store": "fecshop.appserver.fancyecommerce.com",
                "created_at": "2017-10-26 11:36:46",
                "updated_at": "1508989006",
                "items_count": "1",
                "total_weight": "55.00",
                "order_currency_code": "USD",
                "order_to_base_rate": "1.0000",
                "grand_total": "78.96",
                "base_grand_total": "78.95",
                "subtotal": "5.05",
                "base_subtotal": "5.05",
                "subtotal_with_discount": "0.00",
                "base_subtotal_with_discount": "0.00",
                "is_changed": "1",
                "checkout_method": "standard",
                "customer_id": "46",
                "customer_group": null,
                "customer_email": "2358269014@qq.com",
                "customer_firstname": "fdsafasd",
                "customer_lastname": "32423423432",
                "customer_is_guest": "2",
                "remote_ip": null,
                "coupon_code": null,
                "payment_method": "paypal_standard",
                "shipping_method": "fast_shipping",
                "shipping_total": "73.91",
                "base_shipping_total": "73.90",
                "customer_telephone": "312321",
                "customer_address_country": "US",
                "customer_address_state": "FL",
                "customer_address_city": "321312",
                "customer_address_zip": "123123",
                "customer_address_street1": "321312",
                "customer_address_street2": "3213",
                "txn_type": null,
                "txn_id": null,
                "payer_id": null,
                "ipn_track_id": null,
                "receiver_id": null,
                "verify_sign": null,
                "charset": null,
                "payment_fee": null,
                "payment_type": null,
                "correlation_id": null,
                "base_payment_fee": null,
                "protection_eligibility": null,
                "protection_eligibility_type": null,
                "secure_merchant_account_id": null,
                "build": null,
                "paypal_order_datetime": null,
                "theme_type": null,
                "if_is_return_stock": "2",
                "payment_token": "EC-54K53891E0627335D",
                "version": "0"
            },
            {
                "order_id": "879",
                "increment_id": "1100000879",
                "order_status": "processing",
                "store": "fecshop.appserver.fancyecommerce.com",
                "created_at": "2017-10-26 11:32:40",
                "updated_at": "1508988760",
                "items_count": "2",
                "total_weight": "110.00",
                "order_currency_code": "USD",
                "order_to_base_rate": "1.0000",
                "grand_total": "140.10",
                "base_grand_total": "140.10",
                "subtotal": "10.10",
                "base_subtotal": "10.10",
                "subtotal_with_discount": "0.00",
                "base_subtotal_with_discount": "0.00",
                "is_changed": "1",
                "checkout_method": "standard",
                "customer_id": "46",
                "customer_group": null,
                "customer_email": "34343@3232.com",
                "customer_firstname": "111",
                "customer_lastname": "222",
                "customer_is_guest": "2",
                "remote_ip": null,
                "coupon_code": null,
                "payment_method": "paypal_standard",
                "shipping_method": "fast_shipping",
                "shipping_total": "130.00",
                "base_shipping_total": "130.00",
                "customer_telephone": "3232",
                "customer_address_country": "CN",
                "customer_address_state": "SD",
                "customer_address_city": "3232",
                "customer_address_zip": "ewewew",
                "customer_address_street1": "3232",
                "customer_address_street2": "3232",
                "txn_type": "cart",
                "txn_id": "0V169888BY981864X",
                "payer_id": "FKL4V7D5GCACY",
                "ipn_track_id": null,
                "receiver_id": null,
                "verify_sign": null,
                "charset": null,
                "payment_fee": "4.36",
                "payment_type": "instant",
                "correlation_id": "4fedee75b4a72",
                "base_payment_fee": "4.37",
                "protection_eligibility": "Ineligible",
                "protection_eligibility_type": "None",
                "secure_merchant_account_id": "H4KXD885J8LV2",
                "build": "39972400",
                "paypal_order_datetime": "1970-01-01 08:33:37",
                "theme_type": null,
                "if_is_return_stock": "2",
                "payment_token": "EC-5X839405FA652891R",
                "version": "0"
            },
            {
                "order_id": "878",
                "increment_id": "1100000878",
                "order_status": "pending",
                "store": "fecshop.appserver.fancyecommerce.com",
                "created_at": "2017-10-26 11:15:36",
                "updated_at": "1508987736",
                "items_count": "2",
                "total_weight": "110.00",
                "order_currency_code": "USD",
                "order_to_base_rate": "1.0000",
                "grand_total": "140.10",
                "base_grand_total": "140.10",
                "subtotal": "10.10",
                "base_subtotal": "10.10",
                "subtotal_with_discount": "0.00",
                "base_subtotal_with_discount": "0.00",
                "is_changed": "1",
                "checkout_method": "standard",
                "customer_id": "46",
                "customer_group": null,
                "customer_email": "34343@3232.com",
                "customer_firstname": "111",
                "customer_lastname": "222",
                "customer_is_guest": "2",
                "remote_ip": null,
                "coupon_code": null,
                "payment_method": "paypal_standard",
                "shipping_method": "fast_shipping",
                "shipping_total": "130.00",
                "base_shipping_total": "130.00",
                "customer_telephone": "3232",
                "customer_address_country": "CN",
                "customer_address_state": "SD",
                "customer_address_city": "3232",
                "customer_address_zip": "ewewew",
                "customer_address_street1": "3232",
                "customer_address_street2": "3232",
                "txn_type": null,
                "txn_id": null,
                "payer_id": null,
                "ipn_track_id": null,
                "receiver_id": null,
                "verify_sign": null,
                "charset": null,
                "payment_fee": null,
                "payment_type": null,
                "correlation_id": null,
                "base_payment_fee": null,
                "protection_eligibility": null,
                "protection_eligibility_type": null,
                "secure_merchant_account_id": null,
                "build": null,
                "paypal_order_datetime": null,
                "theme_type": null,
                "if_is_return_stock": "2",
                "payment_token": "EC-3PM16146CW569603M",
                "version": "0"
            },
            {
                "order_id": "877",
                "increment_id": "1100000877",
                "order_status": "pending",
                "store": "fecshop.appserver.fancyecommerce.com",
                "created_at": "2017-10-26 11:05:49",
                "updated_at": "1508987149",
                "items_count": "2",
                "total_weight": "110.00",
                "order_currency_code": "USD",
                "order_to_base_rate": "1.0000",
                "grand_total": "140.10",
                "base_grand_total": "140.10",
                "subtotal": "10.10",
                "base_subtotal": "10.10",
                "subtotal_with_discount": "0.00",
                "base_subtotal_with_discount": "0.00",
                "is_changed": "1",
                "checkout_method": "standard",
                "customer_id": "46",
                "customer_group": null,
                "customer_email": "34343@3232.com",
                "customer_firstname": "111",
                "customer_lastname": "222",
                "customer_is_guest": "2",
                "remote_ip": null,
                "coupon_code": null,
                "payment_method": "paypal_standard",
                "shipping_method": "fast_shipping",
                "shipping_total": "130.00",
                "base_shipping_total": "130.00",
                "customer_telephone": "3232",
                "customer_address_country": "CN",
                "customer_address_state": "SD",
                "customer_address_city": "3232",
                "customer_address_zip": "ewewew",
                "customer_address_street1": "3232",
                "customer_address_street2": "3232",
                "txn_type": null,
                "txn_id": null,
                "payer_id": null,
                "ipn_track_id": null,
                "receiver_id": null,
                "verify_sign": null,
                "charset": null,
                "payment_fee": null,
                "payment_type": null,
                "correlation_id": null,
                "base_payment_fee": null,
                "protection_eligibility": null,
                "protection_eligibility_type": null,
                "secure_merchant_account_id": null,
                "build": null,
                "paypal_order_datetime": null,
                "theme_type": null,
                "if_is_return_stock": "2",
                "payment_token": "EC-2CY34317TN339413P",
                "version": "0"
            },
            {
                "order_id": "875",
                "increment_id": "1100000875",
                "order_status": "pending",
                "store": "fecshop.appserver.fancyecommerce.com",
                "created_at": "2017-10-25 19:00:49",
                "updated_at": "1508929249",
                "items_count": "1",
                "total_weight": "55.00",
                "order_currency_code": "USD",
                "order_to_base_rate": "1.0000",
                "grand_total": "78.96",
                "base_grand_total": "78.95",
                "subtotal": "5.05",
                "base_subtotal": "5.05",
                "subtotal_with_discount": "0.00",
                "base_subtotal_with_discount": "0.00",
                "is_changed": "1",
                "checkout_method": "standard",
                "customer_id": "46",
                "customer_group": null,
                "customer_email": "2358269014@qq.com",
                "customer_firstname": "fdsafasd",
                "customer_lastname": "32423423432",
                "customer_is_guest": "2",
                "remote_ip": null,
                "coupon_code": null,
                "payment_method": "paypal_standard",
                "shipping_method": "fast_shipping",
                "shipping_total": "73.91",
                "base_shipping_total": "73.90",
                "customer_telephone": "312321",
                "customer_address_country": "US",
                "customer_address_state": "CT",
                "customer_address_city": "321312",
                "customer_address_zip": "123123",
                "customer_address_street1": "321312",
                "customer_address_street2": "3213",
                "txn_type": null,
                "txn_id": null,
                "payer_id": null,
                "ipn_track_id": null,
                "receiver_id": null,
                "verify_sign": null,
                "charset": null,
                "payment_fee": null,
                "payment_type": null,
                "correlation_id": null,
                "base_payment_fee": null,
                "protection_eligibility": null,
                "protection_eligibility_type": null,
                "secure_merchant_account_id": null,
                "build": null,
                "paypal_order_datetime": null,
                "theme_type": null,
                "if_is_return_stock": "2",
                "payment_token": null,
                "version": "0"
            },
            {
                "order_id": "874",
                "increment_id": "1100000874",
                "order_status": "pending",
                "store": "fecshop.appserver.fancyecommerce.com",
                "created_at": "2017-10-25 18:56:27",
                "updated_at": "1508928987",
                "items_count": "1",
                "total_weight": "55.00",
                "order_currency_code": "USD",
                "order_to_base_rate": "1.0000",
                "grand_total": "78.96",
                "base_grand_total": "78.95",
                "subtotal": "5.05",
                "base_subtotal": "5.05",
                "subtotal_with_discount": "0.00",
                "base_subtotal_with_discount": "0.00",
                "is_changed": "1",
                "checkout_method": "standard",
                "customer_id": "46",
                "customer_group": null,
                "customer_email": "2358269014@qq.com",
                "customer_firstname": "fdsafasd",
                "customer_lastname": "32423423432",
                "customer_is_guest": "2",
                "remote_ip": null,
                "coupon_code": null,
                "payment_method": "paypal_standard",
                "shipping_method": "fast_shipping",
                "shipping_total": "73.91",
                "base_shipping_total": "73.90",
                "customer_telephone": "312321",
                "customer_address_country": "US",
                "customer_address_state": "CT",
                "customer_address_city": "321312",
                "customer_address_zip": "123123",
                "customer_address_street1": "321312",
                "customer_address_street2": "3213",
                "txn_type": null,
                "txn_id": null,
                "payer_id": null,
                "ipn_track_id": null,
                "receiver_id": null,
                "verify_sign": null,
                "charset": null,
                "payment_fee": null,
                "payment_type": null,
                "correlation_id": null,
                "base_payment_fee": null,
                "protection_eligibility": null,
                "protection_eligibility_type": null,
                "secure_merchant_account_id": null,
                "build": null,
                "paypal_order_datetime": null,
                "theme_type": null,
                "if_is_return_stock": "2",
                "payment_token": null,
                "version": "0"
            },
            {
                "order_id": "873",
                "increment_id": "1100000873",
                "order_status": "pending",
                "store": "fecshop.appserver.fancyecommerce.com",
                "created_at": "2017-10-25 18:56:04",
                "updated_at": "1508928964",
                "items_count": "1",
                "total_weight": "55.00",
                "order_currency_code": "USD",
                "order_to_base_rate": "1.0000",
                "grand_total": "78.96",
                "base_grand_total": "78.95",
                "subtotal": "5.05",
                "base_subtotal": "5.05",
                "subtotal_with_discount": "0.00",
                "base_subtotal_with_discount": "0.00",
                "is_changed": "1",
                "checkout_method": "standard",
                "customer_id": "46",
                "customer_group": null,
                "customer_email": "2358269014@qq.com",
                "customer_firstname": "fdsafasd",
                "customer_lastname": "32423423432",
                "customer_is_guest": "2",
                "remote_ip": null,
                "coupon_code": null,
                "payment_method": "paypal_standard",
                "shipping_method": "fast_shipping",
                "shipping_total": "73.91",
                "base_shipping_total": "73.90",
                "customer_telephone": "312321",
                "customer_address_country": "US",
                "customer_address_state": "CT",
                "customer_address_city": "321312",
                "customer_address_zip": "123123",
                "customer_address_street1": "321312",
                "customer_address_street2": "3213",
                "txn_type": null,
                "txn_id": null,
                "payer_id": null,
                "ipn_track_id": null,
                "receiver_id": null,
                "verify_sign": null,
                "charset": null,
                "payment_fee": null,
                "payment_type": null,
                "correlation_id": null,
                "base_payment_fee": null,
                "protection_eligibility": null,
                "protection_eligibility_type": null,
                "secure_merchant_account_id": null,
                "build": null,
                "paypal_order_datetime": null,
                "theme_type": null,
                "if_is_return_stock": "2",
                "payment_token": null,
                "version": "0"
            }
        ],
        "count": "113"
    }
}
```