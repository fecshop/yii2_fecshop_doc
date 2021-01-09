电商网站对接
===========

> 对于其他的电商系统的对接


> 和其他的电商系统对接，理论上肯定是可以的，但是FA没有去做和其他的电商系统的对接，
下面只是记录一下对接的方式，因为没有测试，因此不保证可行，这里只是记录一下。

### 数据对接


1.追踪系统，添加网站

基础信息 --> 网站管理

具体操作参看:fecshop_relate.md 基础信息部分

2.js打点代码

查看js代码可以看到各个js代码

2.1通用js

```
 // 将该js代码添加的所有网站页面，您可以添加到网站的底部
<script type="text/javascript">
	var _maq = _maq || [];
	_maq.push(['website_id', '9b17f5b4-b96f-46fd-abe6-a579837ccdd9']);
    _maq.push(['fec_store', store_name]);
    _maq.push(['fec_lang', store_language]);
    _maq.push(['fec_app', store_app_name]);
    _maq.push(['fec_currency', store_currency]);
    
	(function() {
		var ma = document.createElement('script'); ma.type = 'text/javascript'; ma.async = true;
		ma.src = ('https:' == document.location.protocol ? 'https://' : 'http://') + 'trace.fecshop.com/fec_trace.js';
		var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ma, s);
	})();
</script>
```

将这个js添加到您的所有页面，而且需要您的电商系统定义js变量的值

`store_name`:如果您的电商分为多个store，譬如英文一个store，法文一个store，那么这里填写您的store的名字，自己定义即可，
如果没有store的概念，那么您可以填写一个字符串，定死即可

`store_language`:当前的语言，填写二位语言简码，譬如`zh`  `en`  `fr`  `es`  `de`等

`store_app_name`:您的电商系统的入口，譬如pc端入口填写`appfront`， html5端填写`apphtml5`，vue点填写`appserver`

`store_currency`:您的当前的货币。


2.2分类 Js

将该js放到分类页面

```
 // 将该js代码添加到分类页面
<script type="text/javascript">
	var _maq = _maq || [];
	_maq.push(['category', category]);  // category：填写分类的name，如果是多语言网站，那么这里填写默认语言的分类name
</script>
```

`category`: js变量，string类型，如果您的网站是多语言，那么这里填写您的网站默认语言
对应的分类name，否则分类的统计将会以分类语言，分开统计。

2.3产品js

将该js放到产品页面

```
 // 将该js添加到产品页面
<script type="text/javascript">
	var _maq = _maq || [];
	_maq.push(['sku', sku]); // sku：当前产品页面的sku编码
</script>
```

`sku`: js变量，string类型

2.4购物车页面

将该js放到产品页面

```
 // 将该js添加到购物车页面，
<script type="text/javascript">
	var _maq = _maq || [];
	_maq.push(['cart', cart]); // cart：购物车页面的购物车数据，该值的示例数据请看下面
</script>
```

`cart`: js变量，对象数组类型，示例如下：

```
[
    {
        "sku":"grxjy56002622",  
        "qty":1,
        "price":35.52
    },
    {
        "sku":"grxjy5606622",
        "qty":4,
        "price":75.11
    }
]
```

内置变量说明

`sku`: string类型，产品的sku

`qty`: int类型，购物车中该产品的个数

`price`: float类型，产品的价格，注意，这里的价格是网站**默认货币**对应的价格，而**不是当前货币**。



2.5搜索界面

将该js放到搜索产品页面

```
// 将该js添加到搜索页面
<script type="text/javascript">
	var _maq = _maq || [];
	_maq.push(['search', search_text]);
</script>
```

search_text 变量的示例数据:

```
//上面 
{
    "text": "fashion handbag", // 搜索词
    "result_qty":5  // 搜索的产品个数
}
```

内置变量说明

`text`: string类型，搜索的关键词

`result_qty`: int类型，搜索该关键词，搜索结果的个数（产品数）


3.服务端通过api传递数据

js打点接收的都是有界面的数据，也就是在页面刷新后执行js的内容，
但是有一些数据是没有界面的，而是纯服务端执行的数据处理，对于这部分数据，
我们可以通过服务端接收这部分数据

对于服务端，在追踪系统：
基础信息 --> 网站管理，在列表中点击 `编辑`,
可以查看到 `验证 Token` 信息。


目前有四部分数据是通过api传送接收的

`账号登录`: 登录账户成功后，发送给trace系统数据

`账号注册`: 注册账户成功后，发送给trace系统数据

`生成订单`: 下单页面生成订单成功后，发送给trace系统数据

`订单支付状态更改`: 订单支付确认后，发送给trace系统数据
，定于订单支付确认，有主动接口查询的，也有IPN消息接收的，
无论哪种方式更改您的电商系统，您都需要将这个状态传递给trace系统。


下面是详细解说,curl发送的数据

3.1、首先，curl 需要在request header加上带上 `access_token`，譬如php的代码：

```
curl_setopt($ch, 
    CURLOPT_HTTPHEADER, 
    [
    'Accept: application/json',
    'Content-Type: application/json',
    'Access-Token: '.$access_token,
    'Content-Length: ' . strlen($data)
    ]
);
```

`$access_token` 就是上面，在trace获取的token。

`Accept` 和 `Content-Type`: 都是json格式，也就是说，发送和接收的格式都是`application/json`

3.2 

3.2.1、api 发送数据的url，在trace中获取，php curl使用的示例代码：

```
curl_setopt($ch, CURLOPT_URL, $this->trace_api_url);
```

3.2.2、

下面就是curl发送的$data 数据：

3.3、$data - 基础参数：

`website_id`: 站点唯一标示，在追踪系统中获取【必须存在】

3.4、$data - 站内的当前参数：

`fec_store`：您的站点的store名称，如果没有store的概念，那么这种随便填写一个短字符串即可

`fec_app`：您的电商系统的当前入口，譬如pc端入口填写`appfront`， html5端填写`apphtml5`，vue点填写`appserver`

`fec_currency`：当前的`货币code`，譬如  `USD`, `EUR`, `CNY` 等。

3.5、$data - 前端传递的cookie参数 - 获取通用数据参数

当您加入trace.js后，该js会在您的网站留下cookie。

`uuid`: 从cookie中获取 `_fta`的值，也就是 $_COOKIE['_fta'] (PHP语法)

`cl_activity`: 从cookie中获取 `_ftactivity`的值，也就是 $_COOKIE['_ftactivity'] (PHP语法)

`cl_activity_child`:从cookie中获取 `_ftactivity_child`的值，也就是 $_COOKIE['_ftactivity_child'] (PHP语法)

`first_page`: 直接赋值`'0'`即可。

`first_referrer_domain`: 从cookie中获取 `_ftreferdomain`的值，也就是 $_COOKIE['_ftreferdomain'] (PHP语法)


`first_referrer_url`: 从cookie中获取 `_ftreferurl`的值，也就是 $_COOKIE['_ftreferurl'] (PHP语法)


`is_return`: 从cookie中获取 `_ftreturn`的值，也就是 $_COOKIE['_ftreturn'] (PHP语法)


3.6、$data - 前端传递的cookie参数 - 获取广告数据参数

`fid`: 从cookie中获取 `_fid`的值，也就是 $_COOKIE['_fid'] (PHP语法)

`fec_medium`: 从cookie中获取 `fec_medium`的值，也就是 $_COOKIE['fec_medium'] (PHP语法)

`fec_source`: 从cookie中获取 `fec_source`的值，也就是 $_COOKIE['fec_source'] (PHP语法)

`fec_campaign`: 从cookie中获取 `fec_campaign`的值，也就是 $_COOKIE['fec_campaign'] (PHP语法)

`fec_content`: 从cookie中获取 `fec_content`的值，也就是 $_COOKIE['fec_content'] (PHP语法)

`fec_design`: 从cookie中获取 `fec_design`的值，也就是 $_COOKIE['fec_design'] (PHP语法)




> 上面的数据完成后，就需要传递您具体执行的参数了，将上面的参数，
根据下面的各种api，加上相应的数据，传递给服务端

3.7

3.7.1账户登录

`login_email`: string 类型，传递登录的email账户

3.7.2账户注册

`register_email`: string 类型，传递注册的email账户

3.7.3生成的订单

`payment_pending_order`: 数组 类型，传递生成的订单信息

详细如下：

```
"order": {
    "invoice": "1100001840",                // 类型：string，订单号
    "order_type": "standard",               // 类型：string，订单支付类型：standard代表标准支付，express代表快捷支付，对于paypal在购物车页面直接点击paypal按钮进行的支付是express，其他的为标准支付standard
    "payment_status": "payment_pending",    // 类型：string，订单的支付状态， `payment_pending`代表未支付，该值为确定值，未支付订单请用该字符串
    "payment_type": "paypal_standard",      // 类型：string，支付方式，也就是您的支付方式的名称，如果某种支付渠道有多种，譬如paypal有standard和express，请在名字区分开，譬如 paypal_standard， paypal_express，其他没有的，直接用名字即可，譬如alipay  
    "amount": 124,                          // 类型：Float， 订单的总额，这里的总额是您的电商系统的基础货币。
    "shipping": 0,                          // 类型：Float， 订单的运费，同上，基础货币
    "discount_amount": 0,                   // 类型：Float， 订单的优惠券折扣，同上，基础货币
    "coupon": "",                           // 类型：string，订单的优惠券
    "email": "2358269014@qq.com",           // 类型：string，下单者的邮箱
    "first_name": "terry",                  // 类型：string，下单者的first_name
    "last_name": "water",                   // 类型：string，下单者的last_name
    "city": "qingdao",                      // 类型：string，订单的收货地址 - 城市
    "zip": "434343",                        // 类型：string，订单的收货地址 - 邮编
    "country_code": "CN",                   // 类型：string，订单的收货地址 - 国家简码
    "state_code": "SD",                     // 类型：string，订单的收货地址 - 省简码
    "country_name": "China",                // 类型：string，订单的收货地址 - 国家全称
    "state_name": "山东省",                 // 类型：string，订单的收货地址 - 省全称
    "address1": "xx市xx镇",                 // 类型：string，订单的收货地址 - 详细街道地址1
    "address2": "",                         // 类型：string，订单的收货地址 - 详细街道地址2
    "products": [                           // 类型：Array， 订单的产品数组
        {
            "sku": "kilw0001",                                          // 类型：string，订单的产品sku
            "name": "Off-the-Shoulder Long Sleeve High-Low Day Dress",  // 类型：string，订单的产品name
            "qty": 5,                                                   // 类型：int，   订单的产品数量
            "price": 124                                                // 类型：float， 订单的产品单价，注意，这个是一个产品的价格
        },
        {
            "sku": "kxxw0601",
            "name": "sex sex Day Dress",
            "qty": NumberLong(5),
            "price": 64 
        }
    ] 
  } 
```

类型说明 详细参看注释


3.7.4更改订单的支付状态

该api用于更改订单的支付状态，因此，调用该api前，请确保订单已经生成存在于trace系统

更改订单状态，如果是订单成功页面调用支付接口发起的，因为是浏览器请求，因此会有cookie存在
，如果是paypal ipn发起，则没有cookie，但是 `website_id`可以从配置中读取

`payment_success_order`: 数组 类型，传递生成的订单信息


详细如下：因为仅仅更新订单状态，因此很多的订单字段不需要填写，不过，您也可以填写

```
"order": {
    "invoice": "1100001840",                // 类型：string，订单号
    "payment_status": "payment_confirmed",    // 类型：string，订单的支付状态， `payment_confirmed`代表订单已支付，该字符串是写死的。
  } 
```


对于具体的实现，您可以参考Fecshop的实现：https://github.com/fecshop/yii2_fecshop/blob/master/services/page/Trace.php



