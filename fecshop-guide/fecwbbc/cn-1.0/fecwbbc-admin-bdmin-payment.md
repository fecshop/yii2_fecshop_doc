Fecwbbc跨境多商户 -设置支付
=========

> 设置跨境多商户支付


目前支持paypal支付，PayGate支付（信用卡收款），线下支付 三种订单支付方式。

### paypal支付设置

![](images/wbbc_26.png)


如何设置paypal，参看：[paypal 正式线上收款账户设置](http://www.fecmall.com/topic/297)

### 线下支付设置

![](images/wbbc_27.png)

线下支付，这里设置您的线下收款账户，您最多可以设置4个账户

设置后，用户可以在订单详情部分看到收款账户信息。


![](images/wbbc_28.png)


如果用户订单支付选择的是线下支付，那么可以通过线下打款，然后上传支付凭证，管理员在后台进行审核


![](images/wbbc_30.png)

审核通过后，勾选，进行线下支付已结清操作即可。

![](images/wbbc_31.png)


### PayGate支付

用于信用卡收款，payGate是非洲的主要的收款方式，支持`兰特`货币收款

1.配置

`网站配置` --> `支付参数配置` -->  `PayGate配置`

![](images/7777.png)

2.测试

2.1测试收款账号以及测试支付卡号




2.2测试收款账号:

```
PayGate ID	10011072130
密码	secret
货币	ZAR，EUR，USD
```

将其填写到后台`PayGate配置`，保存即可


2.3测试支付卡号，可以这里查看：https://docs.paygate.co.za/#testing

```
卡牌	卡号	风险指标
签证	4000000000000002	已验证（AX）*
万事达	5200000000000015	已验证（AX）
美国运通	378282246310005	未认证（NX）
```

2.4进行下单，支付，跳转到paygate页面，填写测试支付信息

![](images/8888.png)

进行下单即可。


填写您的`PayGate Id` 和 `PayGate Password` 即可。

### 支付开启

Appfront和apphtml5的支付，都要在配置中进行开启







1.Appfront配置支付开启

![](images/wbbc_32.png)

1.Apphtml5配置支付开启

![](images/wbbc_33.png)




















