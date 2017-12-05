order:pending订单取消脚本
=========================

> 将pending order，取消订单的脚本


### 脚本介绍

对于用户下的订单，在支付前，订单状态为pending状态，
订单会扣除产品的库存，当用户没有支付该订单，该订单会一直占用产品的库存，
因此，我们需要一个脚本，把pending状态的订单，取消掉，将订单状态改成cancel，
然后释放库存。

为了避免误伤正在下单的用户，您可以根据自己的情况，将N段时间内没有支付的
pending订单过滤出来，然后依次取消

该脚本为周期执行脚本，需要在cron中设置，关于cron的设置参看：
[Fecshop console 介绍和配置](fecshop-console-about.md)

### 配置


### 执行

```
cd vendor/fancyecommerce/fecshop/shell
sh returnPendingProductQtyStock.sh
```









