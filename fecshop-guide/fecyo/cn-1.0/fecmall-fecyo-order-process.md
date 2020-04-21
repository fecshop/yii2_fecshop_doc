Fecmall Fecyo订单处理流程
===========

> 用户下单后，商户进行订单处理的过程


### 订单流程处理

1.`生成订单`，进行`库存`的扣除，`优惠券`被使用，`购物车`清空，订单表生成数据

2.用户进入支付页面，进行`订单支付`，支付完成后，即进入`订单处理`部分


3.用户未支付订单，可以继续在账户中心，订单管理部分，找到订单，`继续支付`

4.用户可以手动`取消未支付`订单，取消订单后，使用的优惠券返还，订单产品`库存返还`

5.超过一定时间未支付的订单，系统`CRON计划任务`，将会自动取消订单，进行优惠券返还，订单产品库存返还等

6.订单支付完成后，将会进入`订单审核`阶段，客服进行订单审核，可以进行订单审核通过和拒绝操作，审核通过的订单，即进入备货阶段

7.管理员可以通过excel将`备货订单导出`

8.订单发货后，管理员可以在后台填写`物流公司`以及`追踪号`，进行`订单发货`操作

9.订单发货后，用户收货后可以进行`订单收货`操作

10.如果用户`超过x天`后，仍未操作订单收货，将由系统CRON计划任务，进行订单收货操作

### 订单状态

1.订单service为：Yii::$service->order,  订单状态为`sale_flat_order`表的`order_status`字段，详细如下：

```
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

// 订单已收货
public $status_received                 = 'received';

// 订单已退款【已收款订单因为某些原因进行退款，譬如：仓库无货，用户收到货后发现破损退款等】
public $status_refunded                     = 'refunded';

// 订单已完成，【用户收到货物xx时间后，未发起纠纷争端，订单状态标记为已完成】
public $status_completed                 = 'completed';

// 订单已取消，【用户付款后，因为纠纷进行取消订单后的状态】
public $status_canceled                 = 'canceled';
```


2.订单的状态改变，是基于流水线的流程化操作，不可逆，每一步的updateAll操作，都要判断状态是否允许


您可以在下面的文档，详细参看订单处理的各个详细细节




















