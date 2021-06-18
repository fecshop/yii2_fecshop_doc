Fecmall Shell 脚本
==========

> Fecmall离线处理数据的脚本

### Fecmall 脚本

对于商城而言，我们需要处理一些数据，大致分为这么几种：

1.`初始化脚本`

根据自己需要，进行一些数据的处理，一般`手动执行`，譬如将`mysql数据库`的数据更新到`mogodb数据库`中。


2.`周期性脚本`

每隔xx时间段就需要执行的脚本，譬如：将`未支付订单取消`处理，释放库存，优惠券等等


对于这些脚本，我们都需要在console入口,编码我们相应`controller`进行执行。

然后通过   `./yii    xxx/xxx/xxx` 进行执行（在根目录）

### Shell脚本

为什么不直接`运行php脚本`，而是通过shell进行`外层控制`执行呢？

1.对于数据量大的数据处理，我们需要进行`分页`，如果使用`单个php`进行进行处理，那么势必会造成`php内存`不足，
因此我们通过shell进行`外层循环`控制，每个分页开启一个php的进程，执行完当前页的数据，php进程完成结束`释放内存`，
然后shell控制执行下一个循环，开启一个新的`php进程`，这样就不会造成内存不足,譬如：

`productSellerCount.sh`:

```
#!/bin/sh
Cur_Dir=$(cd `dirname $0`; pwd)
# get product all count.
count=`$Cur_Dir/../../../../../yii order/item/count`
pagenum=`$Cur_Dir/../../../../../yii order/item/pagenum`

echo "There are $count order products to process"
echo "There are $pagenum pages to process"
echo "##############ALL BEGINING###############";
for i in `seq $pagenum`
do
   $Cur_Dir/../../../../../yii order/item/computesellercount $i
   echo "Page $i done"
done

echo "##############ALL COMPLETE###############";
```

2.当我们写了多个php的脚本，但这几个脚本之间是有条件判断的，根据`脚本a`的脚本，来决定执行`脚本b`还是`脚本c`，
以及传递不同的参数，通过`shell`进行控制，代码的层次性会好很多


3.操作方便，我们写了一个根据时间来处理数据的脚本，通过传递不同的时间，
我们可以新建多个`shell`文件，里面默认传递不同的参数，直接执行即可，当我们几个月后回去直接脚本，直接无脑执行脚本文件即可，
方便实用


4.shell文件本身也就是一个执行入口，比较直观


### Shell文件执行

我们可以通过cron进行执行，详细可以参看：[Fecmall console 介绍和配置](https://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-console-about.html)

### Shell周期执行上锁的问题

对于周期执行的shell文件，譬如`每一分钟`执行一次的脚本，
我们通过linux的`cron`进行添加`计划任务`，每分钟执行一次，但是，可能存在有的时候数据过多，
或者远程获取数据的时间过长，导致执行的时间超过一分钟，导致同时有两个该脚本同时执行，
进而导致产生`脏数据`。

对于这种情况，我们需要`加锁`，如果上一个周期脚本`没有执行`完成，下一个周期脚本`将不允许`执行

例子：

```
* * * * * /usr/bin/flock -xn /www/web_logs/task.lock -c '/bin/bash /www/web/demo/fecerp/addons/fecmall/fecerp/shell/task.sh  >> /www/web_logs/fecerp/task.log 2>&1'
```


`/usr/bin/flock -xn /www/web_logs/task.lock -c 'xxxxxxxxxx'`： linux锁机制

`/bin/bash /www/web/demo/fecerp/addons/fecmall/fecerp/shell/task.sh >> /www/web_logs/fecerp/task.log 2>&1`：
执行的`task.sh`文件 路径，以及将执行结果写入到`/www/web_logs/fecerp/task.log`




















