分销商囤货库存收益统计
==========




分销商虚拟仓，囤货库存售出后获得的收益，进行月结统计，结算给分销商。

分销商通过`支付囤货订单`，获得`分销商虚拟仓囤货库存`，当用户下单使用`囤货库存`后，
分销商就会获得收益，也就是将订单的 `经销商成本价`进行累加, 得到
`分销商囤货收益月结`




```
cd ./addons/fecmall/fecbdct/shell
sh statisticsDistributeStockProfitMonth.sh

```


