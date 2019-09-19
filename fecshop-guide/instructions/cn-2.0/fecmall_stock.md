Fecmall 产品库存
==========

> 指的是Fecmall产品的库存


### 1.产品库存类型

产品的类型，详情可以参看
：[fecshop产品](fecshop_product.md)

#### JD模式

使用的是产品的qty字段，在后台编辑对应，如图：

![jd](images/a211.png)



### 2.库存存储

产品表是mongodb表，产品库存已经从mongodb中抽出来，放到mysql中
，因为产品库存操作具有多表事务性。
product_flat里面也会存储一个qty字段，但是这个存储的值无效，在
产品初始化的时候会使用mysql中的值覆盖掉。
库存在mysql中存储对应的表为：

jd模式库存表：`product_flat_qty`

### 3.库存扣除的流程和安全性

关于支付流程，订单支付库存扣除的流程，具体流程参看[fecmall 支付](fecmall_payment_method.md)


库存安全控制：a)高并发库存超卖控制， b)支付请求多次执行造成库存多次扣除的问题  c)未支付订单库存返还问题。

3.1 高并发库存超卖控制

为了防止超卖的控制，代码参看：`@fecshop/service/product/Stock.php`



3.2 未支付订单库存返还问题。

@fecshop/shell/order/returnPendingProductQtyStock.sh


###  各个位置的库存说明

1.由于产品表数据可能是mysql，也可能是`mongodb`，产品库存表数据在`mysql`，无法`join`，无法做
排序，范围查询等，
因此，将产品`库存`数据同步到`product_flat`表中，
这个脚本参看：[Fecshop 产品库存表库存数据同步到product_flat表的脚本](http://www.fecshop.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-console-product-qty-sync.html)

3.后台产品表，按照库存过滤和按照库存排序，都是使用的product_flat
表的库存，对于范围查询和排序，不需要`100%`的严格精确。

4.对于前台的按照库存的排序，也是使用的mongodb表的库存字段


5.前面第2步骤的脚本，您可以按照自己的需要，每天或者隔几个小时跑一次同步。（
这个看您个人的需要）

[Fecshop 产品库存表库存数据同步到product_flat表的脚本](http://www.fecshop.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-console-product-qty-sync.html)



论坛相关帖子（版本一的帖子）：

http://www.fecshop.com/topic/1460

http://www.fecshop.com/topic/1460


























