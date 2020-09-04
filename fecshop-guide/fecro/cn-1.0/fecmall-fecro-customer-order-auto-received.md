Fecmall Fecro 用户订单自动收货
=============

> 订单产品自动收货操作


### cron计划任务定时执行脚本

关于cron计划任务表达式语法，详细参看文档：http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-console-about.html

### 用户订单自动收货


用户订单发货，`用户收货`后，但用户没有进行订单收货操作，超过`x天`未进行订单`收货操作`的订单，
系统计划任务cron脚本，将会执行`订单收货`操作

1.脚本:

```
cd  ./addons/fecmall/fecro/shell
sh customerOrderReceive.sh

```

建议一天执行一次，譬如：

```
0 0 1 * * /bin/bash /www/web/fecshop/addons/fecmall/fecro/shell/customerOrderReceive.sh  >> /www/web_logs/fecshop/customerOrderReceive.log 2>&1
```

含义解读：

每天凌晨`1:00:00`执行脚本，

fecmall文件根目录：`/www/web/fecshop`

脚本文件为：`/www/web/fecshop/addons/fecmall/fecro/shell/customerOrderReceive.sh` ， 设置成文件权限`755`

执行的结果写到日志文件： `/www/web_logs/fecshop/customerOrderReceive.log`, 设置文件权限可写

`2>&1`：新日志文件为新增


您可以将其添加到计划任务中执行

2.可以在后台设置X天数：`订单发货后自动收货最大天数`


![](images/ww12.png)










