fecmall product: 产品库存表库存数据同步到产品flat表的脚本
=========================

> 将 产品库存表，产品库存数据，同步到产品flat表的脚本

### 为什么要同步？

fecmall的产品和库存是分开表的，为了操作方便，进行库存排序等，进行了数据冗余，
在产品表有一个库存字段，由于fecmall是多数据库支持的系统，因此不能使用join（mysql和
mongodb都支持），因此需要将产品库存表的库存字段的值，同步到产品flat表中

需要注意的是，产品flat表中的库存字段，仅仅是为了排序等一些需要，并不是严格的
的库存值，真正正确的是产品库存表中的库存值


因此，我们需要一个脚本，隔一段时间跑一次，将产品库存表的库存数据同步到产品flat表中,
这个有点类似前面的计算产品最终价格的脚本，计算出来的数据只是为了`范围的查询过滤`，而**不用于
最终的严格数据计算**。

### 同步那些数据？

将表 `product_flat_qty` 的库存数据，同步到 `product_flat`表的qty字段


对于产品库存，更详细的参看帮助文档：
[fecshop 产品库存](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_stock.html)


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
























