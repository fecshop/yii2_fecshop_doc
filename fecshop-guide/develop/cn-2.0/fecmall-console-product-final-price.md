product:计算最终价格的脚本
=========================

> 按照分页遍历产品，计算出来产品的最终价格进行保存到产品字段的脚本，
> 计算出来的价格，仅仅作为分类和搜索页排序和过滤用，并
> 不用于产品的价格显示。


### 脚本介绍

对于产品，有几种价格属性，然后根据规则计算出来最终的价格，譬如，

1.产品的最终价格是由product的price属性存储的，最终价格 = price

2.如果设置了special_price,那么，最终价格 = special_price

3.如果special_price 特价时间过期，最终价格 = price

4.如果存在批发价，也就是tier_price,那么多个产品价格购物车就会更便宜

根据上面的规则，我们最终得到了产品的final_price，但是这个值是动态计算的，
因此，我们无法在分类搜索页面，按照价格排序，过滤，
因此我们需要使用脚本计算出来，在脚本执行时间产品的价格，
然后把值保存到产品的属性final_price中。然后通过这个字段来做分类页面，
产品价格的过滤和排序

**注意**：在产品详细页面，产品的价格还是动态生成，没有使用产品属性final_price，
这个属性仅仅用来在分类页面排序和过滤。

### 脚本执行：

```
cd vendor/fancyecommerce/fecshop/shell
sh computeProductFinalPrice.sh
```

执行log:

```
[root@iZ942k2d5ezZ shell]# sh computeProductFinalPrice.sh
There are 40 products to process
There are 1 pages to process
##############ALL BEGINING###############
Page 1 done
##############ALL COMPLETE###############
[root@iZ942k2d5ezZ shell]# 
```
























