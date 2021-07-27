Fecmall-Braintree支付方式
=============

> braintree支付方式，和paypal，支付宝之类的支付流程不同，
braintree是再商城内部填写支付信息，进行信用卡扣款的流程


### 工作原理

![](images/1x9kwrNQ4Dfed7R.png)


### Braintree支付扩展安装

**扩展支持**：fecmall开源系统，fecro跨境单商户，fecwbbc跨境多商户系统

1.应用市场地址：http://addons.fecmall.com/45263532

2.如何应用市场安装应用，请参看文档：[Fecmall安装应用](https://www.fecmall.com/doc/fecshop-guide/addons/cn-2.0/guide-fecmall-addons-install.html)

安装插件后，请设置支付插件的优先级，`fecbraintree扩展优先级需要高出`其他插件（譬如fecro，fecwbbc等），
如何设置扩展插件优先级，请参看：[Fecmall-应用扩展优先级设置](https://www.fecmall.com/doc/fecshop-guide/addons/cn-2.0/guide-fecmall-addons-score.html)


3.如果你使用的`fecro跨境单商户`，必须更改: (做兼容性处理)

打开文件 `./addons/fecmall/fecbraintree/config.php `, 

3.1大约109行,将代码

```
'view'	=> '@fecbraintree/app/appfront/theme/fecbraintree/checkout/onepage/index/payment.php'  
```

改为：

```
'view'	=> '@fecbraintree/app/appfront/theme/fecbraintree/checkout/onepage/index/fecro_payment.php'  
```

3.2大约152行,将代码

```
 'view'	=> '@fecbraintree/app/apphtml5/theme/fecbraintree/checkout/onepage/index/payment.php'
```

改为：

```
 'view'	=> '@fecbraintree/app/apphtml5/theme/fecbraintree/checkout/onepage/index/fecro_payment.php'  
```


4.如果您是fecwbbc多商户，必须更改: (做兼容性处理)

打开文件 `./addons/fecmall/fecpaygate/config.php` , 

4.1您需要操作上面的`第3`步骤,操作上面的`3.1`和`3.2`，进行配置文件更改

4.2大约40行,将代码

```
 'class'    => 'fecbraintree\services\payment\Braintree',
```

改为：

```
 'class'    => 'fecbraintree\services\payment\BraintreeFecwbbc',
```

操作完成后，配置更改完成。


### Braintree支付扩展配置

> 目前是以沙盒环境配置

1.注册沙盒账户

注册沙盒账户参看: http://www.fecmall.com/topic/2283

2.2开启CVV验证：

默认不显示CVV验证部分，需要去官网后台开启(https://sandbox.braintreegateway.com/merchants/jjcy2pxvfgx4j5h6/processing/cvv/edit)

go to `Settings` -> `Processing` -> `CVV`, enable CVV verification rules, and renew the client token.

详细操作参看帖子：http://www.fecmall.com/topic/2287


2.后台填写配置信息

将资料填写下面（正式生产环境，请填写相关信息）

![](images/braintree1.png)

appfront开启braintree支付

![](images/braintree2.png)


### Fecro使用braintree的兼容性处理


由于braintree是站内输入信用卡，很容易冲突，因此做了兼容性处理


如果您在fecro上面安装braintree，那么需要进行如下配置更改


打开配置文件：`./addons/fecmall/fecbraintree/config.php`


```
1.代码文件107行左右，将

'view'	=> '@fecbraintree/app/appfront/theme/fecbraintree/checkout/onepage/index/payment.php'

改为：

'view'	=> '@fecbraintree/app/appfront/theme/fecbraintree/checkout/onepage/index/fecro_payment.php'

2.代码文件150行左右，将

'view'	=> '@fecbraintree/app/apphtml5/theme/fecbraintree/checkout/onepage/index/payment.php'

改为：

'view'	=> '@fecbraintree/app/apphtml5/theme/fecbraintree/checkout/onepage/index/fecro_payment.php'

```

### 支付测试

apphtml5也需要开启braintree支付

配置完成后，就可以去前端商城进行下单支付测试了

官方沙盒测试卡：https://developers.braintreepayments.com/guides/credit-cards/testing-go-live/php

譬如：


卡号：`4111 1111 1111 1111`

过期日期：`11/2020`

CVV: `111`


![](images/braintree3.png)



支付完成后，可以看到订单的状态改为：`payment_confirmed`

然后，可以去Braintree官网登陆账户，查看是否收到款项

![](images/braintree6.png)

### Fecro使用braintree的兼容性处理


由于braintree是站内输入信用卡，很容易冲突，因此做了兼容性处理


如果您在fecro上面安装braintree，那么需要进行如下配置更改


打开配置文件：`./addons/fecmall/fecbraintree/config.php`


```
1.代码文件107行左右，将

'view'	=> '@fecbraintree/app/appfront/theme/fecbraintree/checkout/onepage/index/payment.php'

改为：

'view'	=> '@fecbraintree/app/appfront/theme/fecbraintree/checkout/onepage/index/fecro_payment.php'

2.代码文件150行左右，将

'view'	=> '@fecbraintree/app/apphtml5/theme/fecbraintree/checkout/onepage/index/payment.php'

改为：

'view'	=> '@fecbraintree/app/apphtml5/theme/fecbraintree/checkout/onepage/index/fecro_payment.php'

```

### 注意：

Braintree一个收款账户，只能一个`货币`，默认是`美元`，
Fecmall请将默认货币设置为`美元`，fecmall在支付的时候，使用的是`基础货币`进行计算，`而非当前货币`，
因此fecmall的`基础货币`，`必须`和Braintree的`账户货币`保持一致。


### 参考资料：


http://www.fecmall.com/topic/2283


http://www.fecmall.com/topic/2285

http://www.fecmall.com/topic/2284


http://www.fecmall.com/topic/2287






