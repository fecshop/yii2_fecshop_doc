Fecmall Fecbdc多商户分销-经销商月结脚本
========================

> 经销商月结的脚本

### 经销商月结计算逻辑

1.终端用户通过分销商入口下单后，会把对应的经销商id写入订单表中

2.console脚本端，会通过线下脚本，处理订单信息，计算出来经销商的供货成本，汇总起来，写入表

3.当订单取消，订单退货退款，就会写入退款退货必分

4.月结 = 全部订单产品的供货成本 - 退款退货总额


该脚本是fecbbc的脚本演化而来，二开修改为，将计算订单的销售额，改为计算经销商的成本价格。

[Fecmall Fecbbc多商户订单月结脚本](http://www.fecmall.com/doc/fecmall-guide/instructions/cn-1.0/guide-fecmall-order-auto-month-yj.html)

### 脚本计算

```
cd ./addons/fecmall/fecbdc/shell
statisticsBdminMonth.sh
```

您可以通过CRON计划任务，定时跑这个脚本
