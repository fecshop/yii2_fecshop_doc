Api 获取可备货订单信息
===============

> Api描述：按照分页，得到可备货订单列表，可备货订单指的是，订单在后台审核通过后的订单列表

URL: `http://enterprise.appapi.fancyecommerce.com/v2/order/Waitingdispatchlist`

格式：`json`

方式：`get`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| page            | 可选        |   Int       | 设置获取数据的当前页，如果为空，则代表为第一页|
| begin_date            | 可选        |   String       | 格式：`2019-04-08 00:00:00`, 订单过滤的begin时间字符串|
| end_date            | 可选        |   String       | 格式：`2019-04-08 00:00:00`, 订单过滤的end时间字符串|


**Response Header 参数:**


| 参数名称                    | 是否必须    |  类型       |  描述     |
| ----------------------------| -----:      | :----:      |:----:     |
| X-Pagination-Total-Count    | 必须        |   String    | 资源的总数量|
| X-Pagination-Page-Count     | 必须        |   String    | 资源的总页数|
| X-Pagination-Current-Page   | 必须        |   String    | 资源的当前页（目前是第几页）|
| X-Pagination-Per-Page       | 必须        |   String    | 每页资源的数量|
| X-Rate-Limit-Limit          | 可选        |   String    | 在开启速度限制后才会存在，同一个时间段所允许的请求的最大数目|
| X-Rate-Limit-Remaining      | 可选        |   String    | 在开启速度限制后才会存在，在当前时间段内剩余的请求的数量|
| X-Rate-Limit-Reset          | 可选        |   String    | 在开启速度限制后才会存在，为了得到最大请求数所等待的秒数|



**Response JSON Data(Body)：**

格式：`json`

| 参数名称        | 是否必须    |  类型       |  描述        |
| ----------------| -----:      | :----:      |:----:        | 
| code            | 必须        |   Number    | 200 代表成功 |
| message         | 必须        |   String    | 执行结果的文字描述信息  |
| data            | 必须        |   Array     | api获取的数据保存到data中  |

**Response JSON Data(Body Example)：**

```
{
    "code": 200,
    "message": "fetch order success",
    "data": [
        {
            "order_id": "1",                // 订单id
            "increment_id": "1000000001",   // 订单编号
            "order_status": "canceled",     // 订单状态
            "store": "fecshop.appfront.fancyecommerce.com", // 订单的store
            "created_at": "1488957225",     // 订单创建时间戳
            "updated_at": "1488957225",     // 订单更新时间戳
            "items_count": "2",             // 订单的产品数量
            "total_weight": "0.00",         // 订单的总重 kg
            "order_currency_code": "USD",   // 订单的货币
            "order_to_base_rate": "1.0000", // 订单的货币和基础货币的汇率
            "grand_total": "66.00",         // 订单的总金额（当前货币）
            "base_grand_total": "66.00",    // 订单的总金额（基础货币）
            "subtotal": "66.00",            // 订单的产品总额（当前货币）
            "base_subtotal": "66.00",       // 订单的产品总额（基础货币）
            "subtotal_with_discount": null, // 订单的折扣总额（当前货币）
            "base_subtotal_with_discount": null, // 订单的产品总额（基础货币）
            "is_changed": "1",      
            "checkout_method": "standard",  // 订单的支付类型
            "customer_id": null,            // 订单的用户id  
            "customer_group": null,         // 订单的用户组
            "customer_email": "11@23.com",  // 订单的用户email
            "customer_firstname": "111",    // 订单的用户first name
            "customer_lastname": "11",      // 订单的用户last name
            "customer_is_guest": "1",       // 订单是否是游客下单
            "remote_ip": null,
            "coupon_code": null,            // 订单使用的优惠卷码
            "payment_method": "paypal_standard",    // 订单的支付方式
            "shipping_method": "fast_shipping",     // 订单的发货方式
            "shipping_total": "0.00",               // 订单的物流费用（当前货币）
            "base_shipping_total": "0.00",          // 订单的物流费用（基础货币）
            "customer_telephone": "2121",           // 订单的用户电话
            "customer_address_country": "US",       // 订单的用户国家
            "customer_address_state": "FM",         // 订单的用户省/州
            "customer_address_city": "3121",        // 订单的用户城市
            "customer_address_zip": "323223",       // 订单的用户邮编
            "customer_address_street1": "2121",     // 订单的用户街道地址1
            "customer_address_street2": "2121",     // 订单的用户街道地址2
            "txn_type": null,
            "txn_id": null,                         // 订单的交易号
            "payer_id": null,
            "ipn_track_id": null,
            "receiver_id": null,
            "verify_sign": null,
            "charset": null,
            "payment_fee": null,                    // 订单的交易费（譬如使用paypal支付，paypal需要收取交易费）
            "payment_type": null,
            "correlation_id": null,
            "base_payment_fee": null,
            "protection_eligibility": null,
            "protection_eligibility_type": null,
            "secure_merchant_account_id": null,
            "build": null,
            "paypal_order_datetime": null,
            "theme_type": null,
            "if_is_return_stock": "1",
            "payment_token": null,
            "version": "0",
            "customer_address_state_name": "Federated States Of Micronesia", // 省州全称
            "customer_address_country_name": "United States",   // 国家全称
            "currency_symbol": "$",                             // 当前订单货币符号
            "products": [
                {
                    "item_id": "1",
                    "store": "fecshop.appfront.fancyecommerce.com",
                    "order_id": "1",
                    "created_at": "1488957225",
                    "updated_at": "1488957225",
                    "product_id": "57d60c6cf656f2b57ddf9deb",
                    "sku": "sk10002",
                    "name": "Leaves Pattern Waisted Zippered Dress",
                    "custom_option_sku": null,
                    "image": "/2/01/20160723113745_77121.jpg",
                    "weight": "0.00",                   // 产品单重kg
                    "qty": "1",                         // 产品数量
                    "row_weight": "0.00",               // 产品总数量kg
                    "price": "33.00",                   // 订单产品价格（当前货币）
                    "base_price": "33.00",              // 订单产品价格（基础货币）
                    "row_total": "33.00",               // 订单产品价格*个数的总值（当前货币）
                    "base_row_total": "33.00",          // 订单产品价格*个数的总值（基础货币）
                    "redirect_url": "/leaves-pattern-waisted-zippered-dress",  产品url key
                    "spu_options": {                    // 订单产品 的spu属性
                        "color": "multicolor",
                        "size": "M"
                    },
                    "custom_option": [],
                    "custom_option_info": {             // 订单产品的自定义属性
                        "color": "multicolor",
                        "size": "M"
                    }
                },
                {
                    "item_id": "2",
                    "store": "fecshop.appfront.fancyecommerce.com",
                    "order_id": "1",
                    "created_at": "1488957225",
                    "updated_at": "1488957225",
                    "product_id": "57c7da9af656f2577a3bf56e",
                    "sku": "sk0003",
                    "name": "Sweet Polka Dot Open Back Summer Dress For Women",
                    "custom_option_sku": null,
                    "image": "/2/01/20160804090311_12690.jpg",
                    "weight": "0.00",
                    "qty": "1",
                    "row_weight": "0.00",
                    "price": "33.00",
                    "base_price": "33.00",
                    "row_total": "33.00",
                    "base_row_total": "33.00",
                    "redirect_url": "/sweet-polka-dot-open-back-summer-dress-for-women",
                    "spu_options": {
                        "color": "red",
                        "size": "L"
                    },
                    "custom_option": [],
                    "custom_option_info": {
                        "color": "red",
                        "size": "L"
                    }
                }
            ]
        },
        {
            ...
        }
    ]
}
```