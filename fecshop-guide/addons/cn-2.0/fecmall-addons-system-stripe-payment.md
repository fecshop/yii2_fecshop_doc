Fecmall-Stripe支付方式
=============

> Stripe支付方式，当今非常流行的支付方式，Fecmall和stripe支付方式进行了对接




### Fecmall-Stripe扩展安装

应用市场地址：http://addons.fecmall.com/57236781

购买后，直接应用管理部分，在线安装即可

刷新后台界面即可



### Fecmall-Stripe扩展配置


1.注册stripe账户：https://dashboard.stripe.com/ ，注册成功后登陆即可

> stripe是没有沙盒和证书环境之分（譬如不同的登陆地址和账户），而是通过`public key` 和 `private key`的前缀来区分的，
因此，只需要将test key，替换为 正式环境的key就可以了

得到测试环境的：`public key` 和 `private key`

![](images/stripe1.png)


正式环境需要身份验证后，才可以获取


2.添加webhooks，获取`Endpoint Secret`

添加webhooks网址：https://dashboard.stripe.com/test/webhooks

![](images/stripe2.png)

![](images/stripe3.png)


`Endpoint Secret`就是上图的`密码签名`



3.后台配置

进入后台配置界面

![](images/stripe4.png)

将上面获取的`public key` ， `private key`
，`Endpoint Secret`填写进去
，保存即可


4.appfront apphtml5开启stripe支付

4.1appfront开启支付

![](images/stripe5.png)


4.2apphtml5开启支付

![](images/stripe6.png)


### Fecmall-Stripe商城下单测试


1.产品加入购物车后，进行下单，支付方式选择stripe，点击下单后，
就会跳转到支付页面


![](images/stripe7.png)


测试卡stripe test card：https://stripe.com/docs/testing#cards


![](images/stripe8.png)

`卡号`填写上面`测试卡`的卡号，日期`大于`当前的日期即可，其他的随便填,然后点击支付即可，
支付成功后，将会跳转回商城，完成支付。







































