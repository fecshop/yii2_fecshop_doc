FAA shell脚本
=====

> 执行的脚本

### Shell脚本

1.在fecmall根目录执行：

```
cd ./addons/fecmall/fecfaa/shell
dailyStatistics.sh

```


注意，执行FAA的这个shell脚本，Fa的那个shell脚本就不需要执行，已经包含了


3.cron

您可以使用cron定时任务，cron语法参看：http://www.fecmall.com/topic/4444

Linux下执行：`crontab -e`

填写内容：

```
1 1 1 * *  /bin/bash /www/web/fecshop/addons/fecmall/fecfaa/shell/dailyStatistics.sh  >> /www/web_logs/fecshop/dailyStatistics.log 2>&1
```

`1 1 1 * * `: 每天的 `01:01:01`，执行该统计脚本

`/www/web/fecshop/addons/fecmall/fecfaa/shell/dailyStatistics.sh`: 文件路径，请替换成您自己的文件路径

`/www/web_logs/fecshop/dailyStatistics.log`: 脚本执行的log日志输出，您可以替换成您自己的log文件路径， 另外，一定要设置成777文件权限，否则无法写入log

4.手动执行该脚本

```
cd /www/web/fecshop/addons/fecmall/fecfa/shell
sh dailyStatistics.sh 
```

执行`sh dailyStatistics.sh`,即执行前`1`天的数据统计

执行`sh dailyStatistics.sh 7`,即执行前`1-7`天的数据统计，也就是将7天前的每一天，都执行一遍。






