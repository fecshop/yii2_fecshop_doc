Fecshop Api 更新订单状态 UpdateOrderStatus
=========================


> Api描述：根据传递的increment_id，更新订单的支付状态 order_status

**注意**：该接口更新订单的状态字段：order_status，
如果有 tracking_number 和 tracking_company，将会更新物流信息


URL: `http://fecshop.appapi.fancyecommerce.com/v1/order/updateorderstatus`

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
| tracking_number                  | 否        |   String    | 快递追踪号  |
| tracking_company                  | 否        |   String    | 快递公司  |

对于多语言属性的`数据结构`和`必填`的详细说明参看： [AppApi多语言属性说明](fecshop-api-mutil-lang.md)

**Request JSON Data(Body Example)：**

```
{
   "increment_id": "1100006617",
   "order_status": "dispatched",
   "tracking_number":"SF1410289486215",
   "tracking_company":"sf"
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
    "message": "update order status success",
    "data": {
        "updateData": {
            "order_id": 6617,
            "increment_id": "1100006617",
            "order_status": "dispatched",
            "store": "fecshop.appfront.fancyecommerce.com",
            "created_at": 1621217914,
            "updated_at": 1621217968,
            "items_count": 1,
            "total_weight": "0.30",
            "order_currency_code": "USD",
            "order_to_base_rate": "1.0000",
            "grand_total": "32.00",
            "base_grand_total": "32.00",
            "subtotal": "32.00",
            "base_subtotal": "32.00",
            "subtotal_with_discount": "0.00",
            "base_subtotal_with_discount": "0.00",
            "is_changed": 1,
            "checkout_method": "standard",
            "customer_id": 11113,
            "customer_group": null,
            "customer_email": "2358269014@qq.com",
            "customer_firstname": "赵地虎",
            "customer_lastname": "5454",
            "customer_is_guest": 2,
            "remote_ip": null,
            "coupon_code": "",
            "payment_method": "paypal_standard",
            "shipping_method": "free_shipping",
            "shipping_total": "0.00",
            "tracking_number": "SF1410289486215",
            "tracking_company": "sf",
            "base_shipping_total": "0.00",
            "customer_telephone": "18644444444",
            "customer_address_country": "CN",
            "customer_address_state": "HEB",
            "customer_address_city": "鸡西市",
            "customer_address_zip": "222222",
            "customer_address_street1": "xx区西乡街道333",
            "customer_address_street2": "",
            "order_remark": "",
            "txn_type": "cart",
            "txn_id": "62710464455523737",
            "payer_id": "FKL4V7D5GCACY",
            "ipn_track_id": null,
            "receiver_id": null,
            "verify_sign": null,
            "charset": null,
            "payment_fee": "1.23",
            "payment_type": "instant",
            "correlation_id": "74075ee7b28e4",
            "base_payment_fee": "1.23",
            "protection_eligibility": "Eligible",
            "protection_eligibility_type": "ItemNotReceivedEligible,UnauthorizedPaymentEligible",
            "secure_merchant_account_id": "H4KXD885J8LV2",
            "build": "55620159",
            "paypal_order_datetime": "1970-01-01 08:33:41",
            "theme_type": null,
            "if_is_return_stock": 2,
            "payment_token": "EC-69560820FR241293K",
            "version": 0,
            "is_reviewed": 2,
            "audited_at": null,
            "dispatched_at": null,
            "received_at": null,
            "reviewed_at": null
        }
    }
}

```

