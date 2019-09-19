Api- Onepage Alipay Standard Ipn
================

> 支付宝支付成功后，用于接收支付吧IPN消息的接口
> ,需要注意的是，这个接口不是VUE访问的，而是由支付宝发送IPN的。

URL: `/payment/alipay/standard/ipn`

格式：`html/text`

方式：`post`


一：请求部分
---------

#### 1.Request Header

无

#### 2.Request Body Form-Data：


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| total_amount    | 必须        |   String    | 订单的总金额    |
| trade_no        | 必须        |   String    | 支付宝的订单号     |
| seller_id       | 必须        |   String    | 商家id，用于身份验证  |
| app_id          | 必须        |   String    | appid  |
| out_trade_no    | 必须        |   String    | 详细看支付宝接口  |



**请求参数示例如下：**

```
{
    total_amount: "927.80",
    trade_no: "2017110121001004590200337793",
    seller_id: "2088102170055546",
    app_id: "2016080500172713",
    out_trade_no: "1100000914"
}
```

二：返回部分
----------

#### 1.Reponse Header

无

#### 2.Reponse Body Form-Data：

格式：`html/text`

返回为：字符串

返回数据举例：

```
success
```