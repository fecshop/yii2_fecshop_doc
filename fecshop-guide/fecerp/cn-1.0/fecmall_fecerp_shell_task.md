Task任务脚本
=========

> 任务处理脚本

### Task任务脚本


对于一些耗时比较长的操作，譬如同步数据，不适合即时处理，适合通过任务的方式

管理员在后台操作数据同步，就下了一个任务，然后通过离线脚本来处理任务内容

1.Task任务脚本文件路径：

```
./addons/fecmall/fecerp/shell/task.sh
```

2.通过linux CRON定时任务执行Task.sh


执行`crontab -e`,进入cron编辑部分，进行脚本添加

```
* * * * * /usr/bin/flock -xn /www/web_logs/task.lock -c '/bin/bash /www/web/demo/fecerp/addons/fecmall/fecerp/shell/task.sh  >> /www/web_logs/fecerp/task.log 2>&1'
```

由于各个task的执行时间有偏差，有时候脚本执行时间比较长，有时间比较短，而我们希望每分钟循环执行一次（增强时效性），因此需要通过锁
机制，当task执行超过一分钟没有完成，那么下一分钟的task执行的时候将会取消，直至当前task执行完成，才会执行下一个task


`/usr/bin/flock -xn /www/web_logs/task.lock -c 'xxxxxxxxxx'`： linux锁机制

`/bin/bash /www/web/demo/fecerp/addons/fecmall/fecerp/shell/task.sh  >> /www/web_logs/fecerp/task.log 2>&1`：执行的task.sh文件
路径，以及将执行结果写入到`/www/web_logs/fecerp/task.log`



2.1文件创建以及权限设置：(例子)

```
mkdir /www/web_logs

touch /www/web_logs/task.lock
chmod 777 /www/web_logs/task.lock

touch /www/web_logs/fecerp/task.log
chmod 777 /www/web_logs/fecerp/task.log

chmod 755 /www/web/demo/fecerp/addons/fecmall/fecerp/shell/task.sh
```

2.2添加cron后，您可以添加一下产品同步，譬如将基础库产品同步到商城产品库，可以在后台查看task列表：

![](images/erp_14.jpg)








