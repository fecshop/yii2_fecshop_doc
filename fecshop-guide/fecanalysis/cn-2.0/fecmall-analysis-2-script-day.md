FA-2.0 shell脚本
===========

> FA的离线shell脚本



### 每日统计脚本

1.脚本文件：`./addons/fecmall/fecfa/shell/dailyStatistics.sh`

您可以每日跑一次，建议凌晨1点跑



2.功能：将当日接收的数据，进行mapreduce分析，算出来统计结果，然后将其复制到最终表中。


3.cron

您可以使用cron定时任务，cron语法参看：http://www.fecmall.com/topic/4444

Linux下执行：`crontab -e`

填写内容：

```

1 1 1 * * /bin/bash /www/web/fecshop/addons/fecmall/fecfa/shell/dailyStatistics.sh  >> /www/web_logs/fecshop/dailyStatistics.log 2>&1


```

`1 1 1 * *`: 每天的 01:01:01，执行该统计脚本


`/www/web/fecshop/addons/fecmall/fecfa/shell/dailyStatistics.sh`: 文件路径，请替换成您自己的文件路径

` /www/web_logs/fecshop/dailyStatistics.log`: 脚本执行的log日志输出，您可以替换成您自己的log文件路径，
另外，一定要设置成777文件权限，否则无法写入log


4.手动执行该脚本

```
cd /www/web/fecshop/addons/fecmall/fecfa/shell
sh dailyStatistics.sh 
```

执行`sh dailyStatistics.sh`,即执行前1天的数据统计


执行`sh dailyStatistics.sh 7`,即执行前`1-7`天的数据统计，也就是将7天前的每一天，都执行一遍。


### 手动删除历史数据


FA 在mongodb中，每天都新建一个表，如果您的空间不足，想要批量删除历史的库，那么可以手动执行该脚本


1.进入文件：@fecfa\app\console\modules\Fa\controllers\DbController.php


修改类变量

```
// 保留的月数。譬如只保留最近3个月的trace数据
public $retainTraceDbMonth = 3;
// 删除的月数，设置为1，代表将`三个月之前`和 `四个月之前` 之间的数据，进行删除
public $retainRemoveMonth = 1;
```

2.执行脚本

```
`cd /www/web/fecshop/addons/fecmall/fecfa/shell`
sh dropHistoryTrace.sh
```

执行后，将会将1步骤设置mongodb历史数据库删除掉


