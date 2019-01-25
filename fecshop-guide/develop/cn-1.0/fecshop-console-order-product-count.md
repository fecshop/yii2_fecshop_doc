order: 计算产品销量的脚本
======================

> 通过脚本，根据时间取x月之内的订单（也可以是全部订单），将产品的销量个数累加，然后将
最终个数值添加到产品表的score字段，作为产品的销量的功能脚本

### 脚本介绍

很多时候，我们需要通过销量对产品进行排序，或者通过销量过滤产品，譬如取出来销量最好的10个产品，
因此我们需要通过订单（fecshop计算的默认是已经支付的订单）进行计算产品的销量个数，然后将最终计算值
同步到product的score字段，然后，您就可以通过这个字段对产品进行排序和过滤了


### 配置

设置订单的范围，也就是计算xx月之内的订单

您可以在 @common/config/fecshop_local_services/Order.php 在order config中添加下面的配置

```
/**
         * 计算销量的订单时间范围（将最近几个月内的订单中的产品销售个数累加，作为产品的销量值,譬如3代表计算最近3个月的订单产品）
         * 0：代表计算订单表中所有的订单。
         * 这个值用于console入口（脚本端），通过shell脚本执行，计算产品的销量，将订单中产品个数累加作为产品的销量，然后将这个值更新到产品表字段中，用于产品按照销量排序或者过滤
         */
        'orderProductSaleInMonths' => 3,
```

上面的设置代表取最近3个月的订单，进行计算，将订单的产品销量个数总值作为最终销量，更新到
product表的score字段

### 执行脚本

```
cd vendor/fancyecommerce/fecshop/shell/order
sh productSellerCount.sh
```




### 获取产品


1.获取销量前十的产品代码

```
$filter = [
    'orderBy'	=> ['score' => SORT_DESC],
    'numPerPage' 	=> 10,
    'pageNum'		=> 1,
];
$productData = Yii::$service->product->coll($filter);

if (is_array($productData['coll']) && !empty($productData['coll'])) {
    foreach ($productData['coll'] as $product) {
        echo $product->sku;
    }

}

```


















