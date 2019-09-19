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
| code            | 必须        |   Number    | 返回状态码，200 代表完成，完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md)  |
| message         | 必须        |   String    | 返回状态字符串描述  |
| data            | 必须        |   Array     | 返回详细数据        |


#### 3.参数code所有返回状态码：（完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md) ）

| code Value      |        描述                                        |
| ----------------| --------------------------------------------------:| 
| 200             | 成功状态码                                         |  


#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "cart_info": {
            "store": "fecshop.appserver.fancyecommerce.com", // store名称
            "items_count": 2,  // 购物车产品个数
            "coupon_code": null,  // 优惠卷码
            "shipping_method": "fast_shipping",  // 物流简码
            "payment_method": null,        // 支付方式
            "grand_total": "27.05",        // 所有的总额（相当于订单总额）
            "shipping_cost": "0.00",       // 运费金额
            "coupon_cost": "0.00",         // 优惠券折扣金额
            "product_total": "27.05",      // 购物车中所有产品的金额
            "base_grand_total": "27.05",   // 基础货币的总额
            "base_shipping_cost": "0.00",  // 基础货币运费金额
            "base_coupon_cost": "0.00",    // 基础货币优惠券金额
            "base_product_total": "27.05", // 基础货币购物车中产品总额
            "products": [
                {
                    "item_id": 391,  // cart product表的item _id   
                    "product_id": "57c7da4af656f273013bf56e", // 产品id
                    "sku": "sk0004", //product sku
                    "name": "Fashion Zigzag Stripe Fit and Flare Sleeveless Dress For Women", //产品name
                    "qty": 1, // product qty
                    "custom_option_sku": "",        // custom option存在值的产品，提交后这里会保存相应的值
                    "product_price": 22,            // 购物车产品当前货币单价
                    "product_row_price": 22,        // 购物车产品当前货币总价（单价*个数）
                    "base_product_price": 22,       // 购物车产品基础货币单价
                    "base_product_row_price": 22,   // 购物车产品基础货币总价（单价*个数）
                    "product_weight": 0,            // 购物车产品的单重
                    "product_row_weight": 0,        // 购物车产品的总重（单重*个数）
                    "product_url": "/fashion-zigzag-stripe-fit-and-flare-sleeveless-dress-for-women",  // urlkey方式的url，在当前vue中没有使用这种方式，这是appfront  apphtml模式下使用的url
                    "custom_option": [],   // 产品的custom_option属性的值
                    "spu_options": {       // 产品的sku属性
                        "color": "white & black",
                        "size": "S"
                    },
                    //产品的主图
                    "img_url": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/150/150/2/01/20160707145718_97803.jpg",
                    //产品的vue模式下的url
                    "url": "/catalog/product/57c7da4af656f273013bf56e", 
                    //产品页面需要选择的属性，譬如颜色尺码等
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