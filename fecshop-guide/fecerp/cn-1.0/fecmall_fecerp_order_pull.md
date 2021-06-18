ERP订单数据拖取
==========

> 脚本定时任务操作，通过api，将商城平台的订单拖取（Pull）到erp订单表中

### ERP订单数据拖取脚本

通过该脚本，进行订单数据拖取

1.脚本文件

文件路径：`./addons/fecmall/fecerp/shell/order.sh`

打开这个文件，你会发现2个部分，上面`ORDER PULL`部分就是订单拖取脚本

因为php的内存机制，php的脚本不易执行时间过长，因此，这里使用的是shell进行
的循环控制，详细您可以阅读里面的shell代码

执行订单pull的部分：`$Cur_Dir/../../../../yii base/order/pullorder $siteId $j`, 
对于`base/order/pullorder`对应的文件是`fecerp\app\console\modules\Base\controllers\OrderController`
,您可以查看里面的`actionPullorder($siteId, $pageNum)`方法，查看具体的实现。

2.脚本控制

订单数据拖取，是通过时间区间进行查询拖取的，当次执行完成后的endAt时间戳，就是下一次执行脚本的beginAt时间戳

当然，这个过程要考虑订单拖取的失败情况，时间区间的限制情况，等等，这个部分的控制是fecmall
的`Fecmall cron脚本时间区间控制`机制来完成的，原理详细参看：
[Fecmall cron脚本时间区间控制](https://www.fecmall.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_cron_script_date_control.html)


3.service文件介绍

3.1拖取订单数据的方法：Yii::$service->orderapi->getApiOrders()

3.2保存订单数据的方法：Yii::$service->orderapi->saveOrder($order, $siteId)

具体由初始化的`$_orderApiService`
来进行具体实现。

譬如fecmall部分，是由 @fecerp/services/orderapi/Fecmall.php来实现的，您可以打开这个文件查看这
两个函数。

关于该机制的具体原理，您可以参看：[ERP订单扩展其他平台](fecmall_fecerp_order_other_platform.md)








