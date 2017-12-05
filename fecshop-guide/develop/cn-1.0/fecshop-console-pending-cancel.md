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

如果您网站是零库存模式，也就是有强大的采购可以很快发货，那么，您把产品库存
设置很大，不需要跑这个脚本。

### 配置


1.设置`特定支付方式`的订单，pending订单不可被取消

打开 `@common/config/fecshop_local_services/Payment.php` 可以看到

```
return [
    'payment' => [
        /**
         * 不需要释放库存的支付方式。譬如货到付款，在系统中
         * pending订单，如果一段时间未付款，会释放产品库存，但是货到付款类型的订单不会释放，
         * 如果需要释放产品库存，客服在后台取消订单即可释放产品库存。
         */
        'noRelasePaymentMethod' => ['check_money'], 
        ...
```

指的是，对于`check_money`这种货到付款（或线下交易）的订单pending订单
是不可以取消，只能客服手动取消或者将订单状态改成processing。

2.设置pending状态超过多长时间的订单，才允许脚本取消

配置文件：`@common/config/fecshop_local_services/Order.php`
，打开后，可以看到下面的配置，代表的含义是，pending状态超过600分钟（10小时）
的订单，才允许脚本取消掉，释放库存。

这个根据自己的情况来设置。

```
'minuteBeforeThatReturnPendingStock'    => 600,
```

3.设置脚本一次处理pending订单的最大个数

> cron周期执行，限制每次处理的pending订单的最大个数。

 

配置文件：`@common/config/fecshop_local_services/Order.php`
，打开后，可以看到下面的配置

```
// 脚本一次性处理多少个pending订单。
'orderCountThatReturnPendingStock'        => 30,
```



### 执行

```
cd vendor/fancyecommerce/fecshop/shell
sh returnPendingProductQtyStock.sh
```

执行log

```
[root@iZ942k2d5ezZ order]# sh returnPendingProductQtyStock.sh 
order_updated_at: 1512491096
order count: 7
cancel order[begin] increment_id: 1100001132
cancel order[end] increment_id: 1100001132
cancel order[begin] increment_id: 1100001133
cancel order[end] increment_id: 1100001133
cancel order[begin] increment_id: 1100001134
cancel order[end] increment_id: 1100001134
cancel order[begin] increment_id: 1100001135
cancel order[end] increment_id: 1100001135
cancel order[begin] increment_id: 1100001136
cancel order[end] increment_id: 1100001136
cancel order[begin] increment_id: 1100001137
cancel order[end] increment_id: 1100001137
cancel order[begin] increment_id: 1100001138
cancel order[end] increment_id: 1100001138
[root@iZ942k2d5ezZ order]# 
```


### 设置cron 

可以每隔5分钟执行一次

```
5/* * * * * /bin/bash /www/web/develop/fecshop/vendor/fancyecommerce/fecshop/shell/order/returnPendingProductQtyStock >> /www/web_logs/returnPendingProductQtyStock.log 2>&1
```




