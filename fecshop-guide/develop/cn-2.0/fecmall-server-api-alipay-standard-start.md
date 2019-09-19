Api- Onepage Alipay Standard Start
================

> 标准支付，选择alipay支付方式支付，跳转的页面加载的api

URL: `/payment/alipay/standard/start`

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


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| return_url      | 必须        |   String     | 支付成功后，跳转回fecshop的url    |

**请求参数示例如下：**

```
{
    return_url: "http://demo.fancyecommerce.com/#/payment/alipay/standard/review"
}
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



#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "redirectUrl": "https://openapi.alipaydev.com/gateway.do?alipay_sdk=alipay-sdk-php-20161101&app_id=2016080500172713&biz_content=%7B%22out_trade_no%22%3A%221100000911%22%2C%22product_code%22%3A%22QUICK_WAP_WAY%22%2C%22total_amount%22%3A%22927.80%22%2C%22subject%22%3A%22Raglan+Sleeves+Letter+Printed+Crew+Neck+Sweatshirt+kahaki-xl%22%7D&charset=UTF-8&format=json&method=alipay.trade.wap.pay&notify_url=http%3A%2F%2Ffecshop.appserver.fancyecommerce.com%2Fpayment%2Falipay%2Fstandard%2Fipn&return_url=http%3A%2F%2Fdemo.fancyecommerce.com%2F%23%2Fpayment%2Falipay%2Fstandard%2Freview&sign=W3z2RHb%2BaC1NvaH8lg1Ug1G%2BRFQYW1yX%2FKaofsVopQp%2BAi84gFzL6%2FL85YnFJNy61X20o%2BObUqrQ5C5tbB5%2Bw%2F0IqXlJEkPAH%2FjVNZxyj2aqZBBPP2hY%2BQIyMVmbnQyEOXYlhYi2rhkVuPw%2BmFoJNFWkC5sSf8lQbOoKBFyljNkdnfelTxVliv7aCVuPsiKLMk6uKthwPv2KYJ9xMHM%2FH1panfC6ERHHwl8bUm6sxbD28vKmTLs5oB%2B%2BwCOreK8QdbE0VU9pK6mYpC6%2FwrTqZZEqUUou9WEOB1RVD%2B1L%2B3rroc0bL9Ru2SJbBhd3XE1B1B7MiR9N2qo3DlVjKr4Ifg%3D%3D&sign_type=RSA2&timestamp=2017-11-01+11%3A30%3A44&version=1.0"
    }
}
```