Api- Customer Order 查新订单详细
================

> 在账户中心的订单列表,点击view查看订单详情执行的api

URL: `/customer/order/view`

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
| order_id        | 必须        |   String     | Order Id    |


**请求参数示例如下：**

```
{
    order_id:907
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
        "order": {
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
            "currency_symbol":"€",              // 货币符号
            "customer_address_state_name": "Niederösterreich",  // 省全称
            "customer_address_country_name": "Austria"          // 国家全称
            "products": [
                {
                    // 产品图片
                    "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/100/100/2/01/20160905101021_28071.jpg",
                    // 产品name
                    "name": "Raglan Sleeves Letter Printed Crew Neck Sweatshirt kahaki-xl",
                    // 产品sku
                    "sku": "p10001-kahaki-xl",
                    // 产品个数
                    "qty": "15",
                    // 该产品的总额（单价*个数）
                    "row_total": "58.65",
                    // product id
                    "product_id": "580835d0f656f240742f0b7c",
                    // customer option 信息
                    "custom_option_info": {
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