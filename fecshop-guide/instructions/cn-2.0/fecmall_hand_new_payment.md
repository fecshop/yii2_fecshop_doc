Fecmall 如何开发一个新支付
==========================


> fecmall开发新的支付的讲解


fecmall开发一个新的支付，是完全可以开发成独立扩展的方式

您需要先了解一下，帮助文件，[Fecmall 支付](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_payment_method.html)

这个文档是对现有的一些支付方式的配置讲解

在这个文档的中间部分，写了`开发新支付` 相应的步骤，
然后是`开发新支付` 的功能实现，该功能是以paypal支付方式作为讲解步骤

最后，您可以以支付宝的开发详细步骤做参考，下面是详细：




### 1.前序

对于支付，如果我想要开发一个支付，我想可以很方便的通过配置的方式无缝的嵌入一个支付，而不需要改动原来的文件，只需要在配置中添加即可，譬如支付宝支付：

![](https://i.loli.net/2017/07/20/59701e1c81e1f.png)

### 2.我想添加支付宝支付，我做的事情：

1.在配置文件`@common/config/fecshop_local_services/Payment.php` 中 在 `paymentConfig.standard` 中添加了下面的配置：

```
'alipay_standard' => [
	'label'=> '支付宝支付',
	// 跳转开始URL
	'start_url'             => '@homeUrl/payment/alipay/standard/start',
	// 支付完成后，跳转的地址。
	'return_url'            => '@homeUrl/payment/alipay/standard/review',
	// 支付宝发送消息，接收的地址。
	'ipn_url'               => '@homeUrl/payment/alipay/standard/ipn',
	'success_redirect_url'  => '@homeUrl/payment/success',
],
```

**配置中的参数讲解:**

`label` ：就是在上面图片中支付部分显示的内容。

`start_url` ： 就是生成订单完成后跳转的url

![](https://i.loli.net/2017/07/20/59702305b78b9.png)

如图点击支付按钮后，fecshop会生成订单，生成订单成功后会跳转到 `start_url` 对应的url，`@homeUrl`代表的首页地址。如果是pc端，也就是appfront，这个url对应的就是文件：`@fecshop\app\appfront\modules\Payment\controllers\alipay\StandardController.php` 的 `actionStart()` 方法。

`return_url` ： 这个是支付宝支付成功后，返回网站的地址，这个地址会调用支付宝接口查询订单支付状态，然后查看本地订单是否是支付成功状态，如果不是则更新订单状态（可能消息发送更改了支付状态）

`ipn_url` ： 这个是支付宝支付notify消息接收的url，如果用户支付完成后，直接关掉了页面，没有回调到自营网站，这样情况下，只能靠IPN更改订单支付状态，这个步骤一定要做好安全验证，支付宝用的是私钥和公钥加密的方式，paypal是把产品重新发送给paypal，问一下paypal是否是合法的方式，这样做的原因是：消息可能被伪造。

`success_redirect_url`： 在`return_url`处理完所有的事情后，自营网站就跳转到站内的支付成功页面，告诉用户支付成功，这个值是固定的，所有的订单的`success_redirect_url`，目前都是一样的，微信也搞成一样即可。

这样嵌入支付宝的支付就完成了。

对于微信支付可以这样添加：

'weixin_standard' => [
	'label'=> '微信支付',
	// 跳转开始URL
	'start_url'             => '@homeUrl/payment/weixin/standard/start',
	// 微信完成后，跳转的地址。
	'return_url'            => '@homeUrl/payment/weixin/standard/review',
	// 微信发送消息，接收的地址。
	'ipn_url'               => '@homeUrl/payment/weixin/standard/ipn',
	'success_redirect_url'  => '@homeUrl/payment/success',
],

然后新建文件：
`@fecshop\app\appfront\modules\Payment\controllers\weixin\StandardController.php`

### 3.实现上面对应的各个controller

打开：`@fecshop\app\appfront\modules\Payment\controllers\alipay\StandardController.php` , 可以看到代码：

```
public $enableCsrfValidation = false;
    /**
     * 在网站下单页面，选择支付宝支付方式后，
     * 跳转到支付宝支付页面前准备的部分。
     */
    public function actionStart()
    {
        //$AopSdkFile = Yii::getAlias('@fecshop/lib/alipay/AopSdk.php');
        //require($AopSdkFile);
        echo '支付宝支付跳转中...';
        return Yii::$service->payment->alipay->start();
    }
    /**
     * 从支付宝支付成功后，跳转返回 fec-shop 的部分
     */
    public function actionReview()
    {
        $reviewStatus = Yii::$service->payment->alipay->review();
        if($reviewStatus){
            $successRedirectUrl = Yii::$service->payment->getStandardSuccessRedirectUrl();
            return Yii::$service->url->redirect($successRedirectUrl);
        }else{
            echo Yii::$service->helper->errors->get('<br/>');
            return;
        }
    }
    /**
     * IPN，支付宝消息接收部分
     */
    public function actionIpn()
    {
        \Yii::info('alipay ipn begin', 'fecshop_debug');
       
        $post = Yii::$app->request->post();
        if (is_array($post) && !empty($post)) {
            \Yii::info('', 'fecshop_debug');
            $post = \Yii::$service->helper->htmlEncode($post);
            ob_start();
            ob_implicit_flush(false);
            var_dump($post);
            $post_log = ob_get_clean();
            \Yii::info($post_log, 'fecshop_debug');
            $ipnStatus = Yii::$service->payment->alipay->receiveIpn($post);
            if($ipnStatus){
                echo 'success';
                return;
            }
        }
    }
```

可以看到上面使用了 `Yii::$service->payment->alipay` 服务，也就是payment alipay services，下面说一下步骤：

### 4. alipay payment service

4.1 新建alipay  services 文件：

新建service文件:`@fecshop\services\payment\Alipay.php` , 由于支付宝的sdk不支持namespace，因此，需要通过require的方式引入,支付宝的sdk，我放到了`@fecshop/lib/alipay`下面，下面是在alipay payment中引入（init()方法会在构造方法中调用，一次init方法，在实例化alipay对象的时候就会执行）

```
public function init()
    {
        parent::init();
        $AopSdkFile = Yii::getAlias('@fecshop/lib/alipay/AopSdk.php');
        require($AopSdkFile);
    }

```

Alipay.php 里面其他的函数暂不一一说明。

4.2 在配置中引入alipay services

打开配置文件：@fecshop/config/services/Payment.php 文件可以看到配置

```
'alipay' => [
                'class'         => 'fecshop\services\payment\Alipay',
                // 商家appId
                //'appId'       => '2016080500172713',
                // 应用私钥，可以在这里通过工具生成：https://docs.open.alipay.com/291/105971/
                //'rsaPrivateKey' => 'MIIEpAIBAAKCAQEApIw+Hsk65Z+mieDsEiTkhtf7ZNBgks83DLUDb1yh2d/HDB0s9zHFzsgQGny0kUTM0fJ43h7WydyUG9Kuv4fxD5iVfM2xkUYW5bvfTXVaj5LLj8rTKL+nnFybzzM5rewqh2u1Gzd7BbpOnhMn4Y+7JyyaWXsnRFBxIrmRAqQJVlVUG4RclLHfplFkMVcEMzoRda2UV54oQDMg8ZxignCqxgIKr7bpwpgdpdqZArHtmyEjhQfIblCLDjVk0rKxGsaz+ATYVt3eQozdyNEuKFRhy0VGmwmdQYhQFbge7SS6bVqXZHsq2fNZ6hMJ2XNOZajFm5jXMksnaX85PzdJ58HFewIDAQABAoIBAAn/c27Pb0Kwdp/+CJn5n+EJkn7HonaJHKErBnBnwnXIgQGdbDQA1DICOehCF36UHZXME8f7O7W8L0uZe4Crs9vsu3h/zwAysAV5atH8BWqf0rqD6lyZeIepoNXwGNsWdGcSBkkHD/SDI2+7Xjr4TrjMnvw83V/rO1SOzd7JNMAICj6NZ2tteIqQCn+BriEEawRDimSAWvVaCbwnbCDF8y40MxZ4K6picBQ0gsbC6eQuXRqzB6CoFBkQsXGtK0VXvlJXVmKRzRqPxjD6Cer21tF1CDryVedSWKsdwEXvOdO8LdPZpnmQMvwyTuhM0V9L3rif4spIK9ML3lZLzM47rpECgYEA2XzyRUEni4jKmWcE3oSZjCvp5BJwi6DSRkAphGTwoW/8oTCJhx1B43Qusxv0bUwGzN/KlRHwgNRerQ9xqWMYnIIfBJLOqASunB8eHMBDN+zC6TnUKOu43CpZ+fGVVm2VUbWLHr5h93AOBSQhtvvegbEk9hbNRCCbcY6jbZZmgkUCgYEAwa9v5Bk8q0obGonDUd5LZkHBt7mfT12cUPkfBClz8/tpv7rirCg5I4XaQHerEo+iCOpn3iIl37ix6V7LcspjJuJwpTn0OzugO7MzEyRi0zAqkNAB1voeJL/hl08rHVkA9fZ2AVuOhUvG2A1pqB8BjY9AW1/2W/EXH16qCKzfhL8CgYEAjK/QoJAHHrH8LMOBWNf547y8bfanqwr7OspikOwi5Ktmhna5YBfC+Xm8g8w/jzww4fKaP1f9dbjrDZQB+IrL7uIVYoX8/J8avI88kWilktWrN+daoKXrTTBwR8jIy8HTZ6nCNr787G0mBJlc3duMEeUffbk+SyW0p/6XJVq3MOkCgYEAhXqPJOZTjkRS63YXels1ITKd+yzcYojDynX07xxWQcV4+l4kCrrprdZ4M8eEyRTdeUF59XcZHNYfHhJrKR/bNxgEw4luDEgqRBpaT43a4WonW4dOTUYv8eme4XT45I/K/rcsWgEr9ibj0U9lCizcGB+qHY7DrFc5NTA7BCGHJOcCgYAN82UigyX4qyqpQDofP/fQOybE2QJuG4pG3x3k/nMxCYm6DAcDS9WyRIAlNwOLXDFLICPa3SlaFjC4A0hLh1CU0465Bau+/q8Avs2/Hz1SMoeqyKf8Sq3RyCFFSb0Zsq26Tr8BtyRjHfFRDiZe5O9H7lOCGqiQEgUuAE9aCgCYVA==',
                // 支付宝公钥，注意，这里不是应用私钥，需要把应用公钥提交后获取的支付宝公钥
                // 对于沙盒账户的步骤可以参看：http://blog.csdn.net/terry_water/article/details/75258175
                //'alipayrsaPublicKey' => 'MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAt5egD1BQCK5fCQXKsgWh+VFj9zanV9cdwVmM/MOQ/zrwMBHMIRO0IdJMft351iXtyACKVX+noK1qzkiVOdg3MxLjbGoMDKR+/1PDxoxtWSVUJBywoYHH/Dh7TCi5GWGasOlXV4qWi0e5Yfa2x/Wi0cxqx76aY5izXEyabHAvWgTWNv121ZRNhl4qcuoWZYiMIQpTst6hEhRn/isUMgdtLRQ1a06q+qOkLmJ99vq8cqbfduAdOuhzbZNWqLV76CSc0meurlVtDoIn5kVAZdzjNTA2rlqSCgs/OZxaL8s/qrIynhLoB6U6i0fj4RsIsbrvoSnrPWo98rsM0RrlU8fpdwIDAQAB',  //'MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEApIw+Hsk65Z+mieDsEiTkhtf7ZNBgks83DLUDb1yh2d/HDB0s9zHFzsgQGny0kUTM0fJ43h7WydyUG9Kuv4fxD5iVfM2xkUYW5bvfTXVaj5LLj8rTKL+nnFybzzM5rewqh2u1Gzd7BbpOnhMn4Y+7JyyaWXsnRFBxIrmRAqQJVlVUG4RclLHfplFkMVcEMzoRda2UV54oQDMg8ZxignCqxgIKr7bpwpgdpdqZArHtmyEjhQfIblCLDjVk0rKxGsaz+ATYVt3eQozdyNEuKFRhy0VGmwmdQYhQFbge7SS6bVqXZHsq2fNZ6hMJ2XNOZajFm5jXMksnaX85PzdJ58HFewIDAQAB',
                'format'        => 'json',
                'charset'       => 'utf-8',
                'signType'      => 'RSA2',
                //'devide'        => 'pc' ,  // 填写pc或者wap，pc代表pc机浏览器支付类型，wap代表手机浏览器支付类型 
                // 下面是沙盒地址， 正式环境请改为：https://openapi.alipay.com/gateway.do
                //'gatewayUrl'    => 'https://openapi.alipaydev.com/gateway.do', 
            ],
```

也就是payment 服务的子服务 alipay。

在alipay service类文件中你可以看到：

```
public $gatewayUrl;
    // 商家 appid
    public $appId;
    // 商家uid
    public $sellerId;
    // 应用私钥
    public $rsaPrivateKey;
    // 支付宝公钥
    public $alipayrsaPublicKey;
    public $format;
    public $charset;
    public $signType;
    
    public $devide;
    public $apiVersion = '1.0'; //'1.0';
```

上面的配置，会在alipay service（`@fecshop\services\payment\Alipay.php`） 实例化的时候，通过注入的方式，把配置注入进去。

当然，上面的配置文件不是一个，是多个配置文件，是为了用户本地化的需要，打散放到了多个地方，最终还是要合并起来的，做微信支付的时候，放到一个配置文件中即可。后面我打散他。
其他的alipay payment支付的配置文件路径：

`@common\config\fecshop_local_services\Payment.php` 本地各个入口公用配置

`@appfront\config\fecshop_local_services\Payment.php` appfront入口本地配置

`@apphtml5\config\fecshop_local_services\Payment.php` apphtml5入口本地配置

初始化的时候这些配置文件会合并起来，在@app/web/index.php文件中可以看到通过array merge合并所有的配置文件成一个数组。

总之，上面的配置合并后，注入到类`@fecshop\services\payment\Alipay.php`实例化的对象，然后这个对象的属性就会被赋值。

最后，咋们看看这个alipay service：`@fecshop\services\payment\Alipay.php`

方法1：`initParam()` 是初始化类内部属性。

方法2：`public function start()` 这个是生成订单，跳转到paypal前的start controller调用的方法，也就是从订单中调取数据，里面有一个方法：`$this->getStartBizContentAndSetPaymentMethod()`  通过订单数据，生成传递给支付宝所需要的参数。其他的都是支付宝内部需要的东西

方法3：`getStartBizContentAndSetPaymentMethod()` ,这个函数在方法2中已经说明

方法4：`paymentSuccess($increment_id,$trade_no,$sendEmail = true)`  ， $increment_id是自营网站订单号，$trade_no是支付宝订单交易号，做微信支付，直接复制过去这个方法调用即可，在订单支付成功的时候调用

方法5：`receiveIpn()` 这个是ipn消息发送后执行的方法。这个方法要做安全验证，支付宝是公钥和私钥加密的方式，通过`$this->_AopClient->rsaCheckV1()`进行验证安全性

方法6：`Review()` 这个是跳转到支付宝付款成功后，跳转到网站的controller执行的方法，这个方法会查询支付宝订单状态，查询后，如果支付成功，通过调用方法`paymentSuccess()`来更改订单状态，发送邮件，然后清空购物车。

方法7：`validateReviewOrder()`: 这个方法是验证数据是否一致，因为有一些人可能在自营网站生成订单后，然后伪造消息发送给支付宝，更改订单金额，实际付了很少的钱，因此需要验证订单金额，商家appid 商家uid等一些列的信息。

alipay大致写完。参考这个文件接口，就可以开发自己的支付了。




QA:

问：有个疑问，微信支付的回调通知，官方不保证百分百回调成功，那是由框架主动发起查询后再调用ipn_url， 还是由业务层自己查询微信支付结果？

答：更改订单状态有2种：

1.在支付宝支付成功后，会跳转到网站，在return url中调用alipay的接口查询，如果支付成功更改网站订单状态，发送邮件，清空购物车等等一系列操作

2.异步消息，支付宝会至少6次消息发送，直到成功。 对于paypal 支付宝，如果网站没有问题，异步消息肯定可以更改订单状态。

最后，如果您不放心，可以把每天的所有pending订单，通过支付宝的接口查询当天的所有订单支付状态，并进行处理。

当然，订单最终都是要传递到erp中，可以在erp中通过接口确认核实一下。

一般不会存在问题，这种概率很小，即使存在问题漏单，用户会咨询客户找上门的。




































