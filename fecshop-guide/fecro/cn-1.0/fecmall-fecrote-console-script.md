Fecrote团长达人分销扩展-Console脚本
=================


> 团长达人分销，需要离线处理数据的脚本

### Fecrot扩展-console脚本

打开文件路径：@fecrot/shell  (@fecrot指的是文件路径 ./addons/fecmall/fecrot),
可以看到有一些shell脚本文件。


1.脚本文件:`distributeComputeProfit.sh`

当分销商带来订单销售额，通过该脚本，计算分销商的分销分成

2.脚本文件:`distributeProfitRecharge.sh`

当分销商带来的订单，经过x天后，订单完成，那么将分销分成充值到分销商钱包。


3.对于该文件下的其他脚本，忽略即可。

对于第1和第2脚本，需要设置cron，如何设置cron，参看文档：[Fecmall Cron 脚本](https://www.fecmall.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_cron_script.html)































