Fecrot扩展-console脚本
============

> 三级分销，需要离线处理数据的脚本

### Fecrot扩展-console脚本

打开文件路径：@fecrot/shell  (@fecrot指的是文件路径 ./addons/fecmall/fecrot),
可以看到有一些shell脚本文件。


1.脚本文件:`computeCustomerGroupByOrderAmount.sh`

计算用户的用户组，当用户的累计订单销售额达到一定的额度后，就会更改用户组。


2.脚本文件:`customerOrderGiftPoint.sh`

根据用户的已支付订单销售额，计算赠送用户积分的脚本

3.脚本文件:`customerOrderGiftWalletAmount.sh`

根据用户的已支付订单销售额，计算赠送用户站内钱包余额的脚本

4.脚本文件:`distributeComputeGroup.sh`

计算分销商的用户组，当分销商带来的订单的累计销售额达到一定的额度后，就会更改用户组

5.脚本文件:`distributeComputeProfit.sh`

当分销商带来订单销售额，通过该脚本，计算分销商的分销分成

6.脚本文件:`distributeProfitRecharge.sh`

当分销商带来的订单，经过x天后，订单完成，那么将分销分成充值到分销商钱包。

















