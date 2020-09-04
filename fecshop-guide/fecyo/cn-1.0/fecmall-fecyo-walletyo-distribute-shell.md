Walletyo-分销系统-Console脚本
================

>  分销部分的脚本


### cron计划任务定时执行脚本

关于cron计划任务表达式语法，详细参看文档：http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-console-about.html


### 后台脚本


@addons/fecmall/walletyo/shell

1.分销用户组计算脚本

```
distributeComputeGroup.sh
```

建议一天执行一次，譬如：

```
0 0 1 * * /bin/bash /www/web/fecshop/addons/fecmall/walletyo/shell/distributeComputeGroup.sh  >> /www/web_logs/fecshop/distributeComputeGroup.log 2>&1
```

含义解读：

每天凌晨`1:00:00`执行脚本，

脚本文件为：`/www/web/fecshop/addons/fecmall/fecyo/shell/distributeComputeGroup.sh` ， 设置成文件权限`755`

执行的结果写到日志文件： `/www/web_logs/fecshop/distributeComputeGroup.log` , 设置文件权限`可写`

`2>&1`：新日志文件为新增


2.分销订单计算收益的脚本

```
distributeComputeProfit.sh
```

建议一天执行一次，详细参考上面的脚本（时间可以错开，譬如：`1:20:00`）

3.分销订单收益，充值分销商钱包的脚本


```
distributeProfitRecharge.sh
```

建议一天执行一次，详细参考上面的脚本（时间可以错开，譬如：`1:40:00`）
















