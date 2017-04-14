上线前的配置
============


当您配置好线上环境，网站可以访问，
产品，分类等都已经上传，那么就可以开始上线了，
上线前需要进行一系列的线上配置。

### 1.邮箱配置

1.1smtp配置

您需要设置您的邮箱smtp信息，比较牛的就是sendgrid了，当然
也有一些其他的邮件商，如果订单量少，可以用
google等免费邮箱的smtp服务，不过发送量有限制

1.2邮件模板的配置

如果您想个性化您的邮件模板，那么您需要修改您的模板内容

邮件配置的详细参看 [fecshop 邮件设置](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_email.html)


### 2.facebook google登录

首先需要申请相应的key ：
[facebook login 申请 app_id 和 app_secret](http://blog.csdn.net/terry_water/article/details/55095721)
，
[google login api 申请 CLIENT_SECRET 和 CLIENT_SECRET ](http://blog.csdn.net/terry_water/article/details/55095209)

申请到了就是配置，
您可以在`@appfront/config/fecshop_local_services/Store.php`中配置
 
### 3.货运信息

配置各个货运方式，以及相应的运费，详细参看：
[Fecshop 货运方式](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_shipping_method.html)

#### 4.支付信息

配置paypal的信息，详细参看：[Fecshop 支付方式](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_payment_method.html)

需要注意的是：paypal的地址和账号一定需要是线上的账户，而不是沙盒url和沙盒账户，
这个一定要看好。


### 5.设置cron 

具体参看[fecshop cron](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_cron_script.html)

### 6.是否开启注册登录等验证码

具体参看[Fecshop 验证码](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_yzm.html)

### 7.设置语言和货币 以及相应的文件翻译

一般是一个域名一个语言，[Fecshop 多语言](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_mutil_lang.html)

[Fecshop 货币](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_currency.html)



### 8.编辑各个page页和static block

[Fecshop page页](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_page.html)

[Fecshop 静态块](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_static_block.html)

### 9.缓存开启

[Fecshop 缓存](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_cache.html)

### 10. https  vls加密方式

google 对https的网站会有加分，建议网站使用https的方式
，nginx配置加密证书的配置可以参考：
[centos 下安装 Let’s Encrypt 永久免费 SSL 证书](http://www.fancyecommerce.com/2017/04/07/centos-%e4%b8%8b%e5%ae%89%e8%a3%85-lets-encrypt-%e6%b0%b8%e4%b9%85%e5%85%8d%e8%b4%b9-ssl-%e8%af%81%e4%b9%a6/)

### 11. 配置加速

这个非必须，网站流量如果比较大，才建议使用
，如果想开启，可以参考：[fecshop 配置加速](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_config_speed.html)


### 12. 设置

将logo图片换成您自己的logo，在



### 13.最后

最后多测试，多看，多观察哪里有问题，新站上线经常会出问题




















