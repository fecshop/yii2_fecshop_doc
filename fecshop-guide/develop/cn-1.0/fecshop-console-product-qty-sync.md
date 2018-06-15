product: Mysql产品库存同步到Mongo表的脚本
=========================

> 将 Mysql产品库存数据，同步到Mongo产品表的脚本

### 为什么要同步？

fecshop的产品数据放到`mongodb`中，而库存的操作，和订单一起是有事务性的，
因此，产品库存放到了`mysql`的表中，这是产品的真实库存数据。


而对于mongodb中，也有一个库存字段，这个字段是为了在分类页面排序，以及后台进行库存排序，过滤等等（mysql无法和mongodb的表进行join操作，另外join操作对内存的开销大，因此用mongodb中的库存字段进行这些查询排序操作）
另外，在订单生成的时候，mongodb的库存字段是不扣除的。
mongodb的`库存`只是用来一些范围查询搜索，而对于获取产品库存用于下单等操作，请使用mysql表的库存。

因此，我们需要一个脚本，隔一段时间跑一次，将mysql的库存数据同步到`mongodb`产品表中,
这个有点类似前面的计算产品最终价格的脚本，计算出来的数据只是为了`范围的查询过滤`，而**不用于
最终的严格数据计算**。

### 同步那些数据？

将mysql表 `product_flat_qty` 的库存数据，同步到 mongodb `product_flat`表的qty字段


对于产品库存，更详细的参看帮助文档：
[fecshop 产品库存](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_stock.html)


### 脚本执行：

```
cd vendor/fancyecommerce/fecshop/shell
sh syncMysqlProductQtyToMongo.sh
```

执行log:

```
[root@iZ942k2d5ezZ shell]# sh syncMysqlProductQtyToMongo.sh 
There are 43 products to process
There are 5 pages to process
##############ALL BEGINING###############
Page 1 done
Page 2 done
Page 3 done
Page 4 done
Page 5 done
##############ALL COMPLETE###############

```
























