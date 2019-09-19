Fecmall 添加新的订单状态
===============

> Fecmall 已经默认添加了标准的订单状态，如果你想添加新的订单状态，可以参看下面描述


### order services

Fecmall的订单状态文件在：https://github.com/fecshop/yii2_fecshop/blob/master/services/Order.php#L27

类变量部分可以看到，有很多 Fecmall 已经订单好的订单状态

```
// 下面是订单支付状态
    // 等待付款状态
    public $payment_status_pending          = 'payment_pending';
    // 付款处理中，(支付处理中，因为信用卡有预售，因此需要等IPN消息来确认是否支付成功)
    public $payment_status_processing       = 'payment_processing';
    // 收款成功（支付状态已确认，代表已经收到钱了）
    public $payment_status_confirmed        = 'payment_confirmed';
    // 欺诈【当paypal的返回金额和网站金额不一致【以及货币类型】的情况，就会判定该状态】
    public $payment_status_suspected_fraud  = 'payment_suspected_fraud';
    // 订单支付已取消【用户进入paypal点击取消订单返回网站，或者payment_pending订单超过xx时间未支付被脚本取消，或者客服后台取消】
    public $payment_status_canceled         = 'payment_canceled';
    // 订单审核中（订单收款成功后，进入erp，需要客服审核，才能开始发货流程，或者可能存在某些问题，被客服暂时挂起）
    public $status_holded                   = 'holded';
    // 订单备货处理中，从成功收款进入erp并客服审核成功后，进入备货流程 到 发货前的状态
    public $status_processing                   = 'processing';
    // 订单已发货【订单包裹被物流公司收取后】
    public $status_dispatched                   = 'dispatched';
    // 订单已退款【已收款订单因为某些原因进行退款，譬如：仓库无货，用户收到货后发现破损退款等】
    public $status_refunded                     = 'refunded';
    // 订单已完成，【用户收到货物xx时间后，未发起纠纷争端，订单状态标记为已完成】
    public $status_completed                 = 'completed';
    // 订单已取消，【用户付款后，因为纠纷进行取消订单后的状态】
    public $status_canceled                 = 'canceled';
    
```

如果你想增加订单状态，重写order service，然后添加相应的订单状态变量（类变量）即可


在下面可以看到三个方法


```
 public function getOrderPaymentedStatusArr()
 protected function actionGetStatusArr()
 protected function actionGetSelectStatusArr()
```

根据你的需求，将你的新的订单状态加到这里面的数组中即可。















