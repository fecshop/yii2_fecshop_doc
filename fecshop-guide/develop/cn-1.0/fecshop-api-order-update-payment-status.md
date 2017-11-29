Fecshop Api 订单 UpdatePaymentStatus
=========================

> Api描述：开发中...

Fecshop Api 分类 UpdateOne
=========================

> Api描述：根据传递的increment_id，更新订单的支付状态 order_status

**注意**：该接口只能简单的更新订单的状态字段：order_status，
而不去做其他任何事情，因此，您如果需求很多，可以自行重写扩展。


URL: `http://fecshop.appapi.fancyecommerce.com/v1/update/updateone`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称                      | 是否必须    |  类型       |  描述     |
| ------------------------------| -----:      | :----:      |:----:     |
| increment_id                  | 必须        |   String    | 订单编号  |
| order_status                  | 必须        |   String    | 订单状态  |


对于多语言属性的`数据结构`和`必填`的详细说明参看： [AppApi多语言属性说明](fecshop-api-mutil-lang.md)

**Request JSON Data(Body Example)：**

```
{
   "increment_id": "1000000001",
   "order_status": "processing"
}
```


**Response Header 参数:**


| 参数名称                    | 是否必须    |  类型       |  描述     |
| ----------------------------| -----:      | :----:      |:----:     |
| X-Rate-Limit-Limit          | 可选        |   String    | 在开启速度限制后才会存在，同一个时间段所允许的请求的最大数目|
| X-Rate-Limit-Remaining      | 可选        |   String    | 在开启速度限制后才会存在，在当前时间段内剩余的请求的数量|
| X-Rate-Limit-Reset          | 可选        |   String    | 在开启速度限制后才会存在，为了得到最大请求数所等待的秒数|



**Response JSON Data(Body)：**

格式：`json`

| 参数名称        | 是否必须    |  类型       |  描述        |
| ----------------| -----:      | :----:      |:----:        | 
| code            | 必须        |   Number    | 200 代表成功 |
| message         | 必须        |   String    | 执行结果的文字描述信息  |
| data            | 必须        |   Object    | api获取的数据保存到data中  |

**Response JSON Data(Body Example)**：将会返回保存到数据库中的数据最终值

```
{
    "code": 200,
    "message": "update category success",
    "data": {
        "updateData": {
            "order_id": 1,
            "increment_id": "1000000001",
            "order_status": "processing",
            "store": "fecshop.appfront.fancyecommerce.com",
            "created_at": 1488957225,
            "updated_at": 1488957225,
            "items_count": 2,
            "total_weight": "0.00",
            "order_currency_code": "USD",
            "order_to_base_rate": "1.0000",
            "grand_total": "66.00",
            "base_grand_total": "66.00",
            "subtotal": "66.00",
            "base_subtotal": "66.00",
            "subtotal_with_discount": null,
            "base_subtotal_with_discount": null,
            "is_changed": 1,
            "checkout_method": "standard",
            "customer_id": null,
            "customer_group": null,
            "customer_email": "11@23.com",
            "customer_firstname": "111",
            "customer_lastname": "11",
            "customer_is_guest": 1,
            "remote_ip": null,
            "coupon_code": null,
            "payment_method": "paypal_standard",
            "shipping_method": "fast_shipping",
            "shipping_total": "0.00",
            "base_shipping_total": "0.00",
            "customer_telephone": "2121",
            "customer_address_country": "US",
            "customer_address_state": "FM",
            "customer_address_city": "3121",
            "customer_address_zip": "323223",
            "customer_address_street1": "2121",
            "customer_address_street2": "2121",
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
            "if_is_return_stock": 1,
            "payment_token": null,
            "version": 0
        }
    }
}

```

