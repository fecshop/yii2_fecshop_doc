Fecmall-2.x 安装微信小程序
=============



> 安装微信小程序部分的教程


### 建议

fecmall对应的微信小程序是偏框架的，功能也比较基础，做国内的微信小程序，建议使用
fecyo扩展对应的微信小程序，[Fecyo微信小程序](http://www.fecmall.com/doc/fecmall-guide/fecyo/cn-1.0/guide-fecmall-fecyo-micro-program-about.html)
，您可以安装fecyo扩展，然后安装对应的小程序，参看上面的文档即可。

### 介绍

1.微信小程序Demo查看，可以微信小程序搜索`fecmall`，或者扫描下面的小程序码进入：

![wx_xiaochengxu_fecmall](images/wx_xiaochengxu_fecmall.png)

2.github地址：https://github.com/fecshop/wx_micro_program


### 微信设置


1.微信帐号开通

需要开通`微信小程序`

需要开通微信商户平台，而微信商户平台需要开通`微信服务号`

顺序：先开通`微信服务号`，需要花300块做认证，然后开通`小程序帐号`，就不需要花300块的认证了

`微信服务号`和`微信小程序`，需要企业资质认证，需要有公司`公章`，以及公司`银行账户`（打款认证）

2.微信商户平台设置

这一块属于`微信支付`的范畴，您可以参看文档：[Fecshop微信支付](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_payment_wx_method.html)

微信小程序支付对应的`JsApi`支付方式

3.微信小程序设置

3.1`服务器域名`设置: 登陆小程序后台： `开发`-->`开发设置`-->`服务器域名`, 设置`request合法域名`，譬如：
https://fecshop.appserver.fancyecommerce.com
线上小程序必须`https`才行，因此需要nginx配置`https`

3.2`appId`和`AppSecret`(小程序密钥)设置：  开发-->开发设置-->开发者ID ，在fecshop：
@common/config/payment/wxpay/lib/WxPay.Micro.Config.php中设置

```
const APPID = 'wxedc77579191bc54f';
const APPSECRET = '3b97c3fb4edeb1ca25e8386d753347a9';
```

3.3设置商户支付收款

@common/config/payment/wxpay/lib/WxPay.Micro.Config.php中设置

```
const MCHID = '1517420921';
const KEY = '8934e7d15483e97501ef794cf7b0519e';
```

该信息参看上面的`微信商户平台设置`，在微信商户平台获取

3.4微信小程序的其他的一些设置，可以参看：
[Fecshop 微信小程序帮助文档](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_wx_micro.html)


### 微信小程序下载

1.github地址：https://github.com/fecshop/wx_micro_program

2.下载

```
git clone git@github.com:fecshop/wx_micro_program.git
```

3.配置

文件下载后，通过`微信开发者工具`加载，微信开发者工具下载地址：https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html

加载的时候需要填写`appid`，请填写您的`appid`

加载完成后，在`config.js`中进行设置

```
'url': 'https://fecshop.appserver.fancyecommerce.com',

// 默认语言
'lang_code': 'zh',

// 默认货币
'currency_code': 'CNY',

```

`url`:指的是fecshop appserver端的域名，开发环境可以是`http`，线上环境必须是`https`，
也就是通过这个域名对应的api获取数据，
因此，您需要先把fecshop的appserver端设置好，然后将域名填写到这里。
 

 
### 其他


`微信小程序`的知识这里就不涉及了，不明白的自行学习吧，微信官方文档：https://developers.weixin.qq.com/miniprogram/dev/framework/

遇到其他的问题，可以论坛发帖:[Fecshop论坛](http://www.fecshop.com/topic)
































