Fecmall Cron 脚本
===============

> 需要在线上设置的定时脚本。脚本地址在@fecshop/shell路径下面


### Fecmall开源版本的脚本

Fecmall的脚本文件地址：`./vendor/fancyecommerce/fecshop/shell`

1.每天一次脚本：

`./computeProductFinalPrice.sh`: 计算商品的最终价格的脚本，用于分类侧栏产品价格排序和过滤

`./order/productSellerCount.sh`：通过订单信息，计算产品销量，然后将销量数据写入产品表的脚本

2.时间间隔：将pending订单（创建时间）未支付超过30分钟的订单取消，并归还产品库存。

`./order/returnPendingProductQtyStock.sh`: 未支付订单进行取消的脚本。

3.使用工具脚本

`urlRewrite.sh`： url重写的脚本，这个脚本在url 重写不准确或者其他情况下需要
手动跑一次，用来纠正url 重写的数据问题

`fullSearchSync.sh`：这个脚本是产品搜索生成mongodb产品相应语言的full Text Search表
的脚本。

`sitemapGeneral.sh`：生成sitemap的脚本

`syncMysqlProductQtyToMongo.sh`: 进行`product mysql services` 切换成`mongodb services`，进行库存同步的脚本

`initDb.sh`: 当你你的fecmall进行升级后，需要执行数据库migrate进行数据库升级，可以执行该脚本

`./search/deleteXunSearchAllData.sh`: 清空xunsearch搜索引擎数据的脚本

`./search/fullSearchSync.sh`: 将数据库的产品数据，同步到搜索引擎

`./product/syncProductMongoDataToMysql.sh`: 进行`product mongodb services` 切换成` mysql services`，进行产品数据同步执行的的脚本


`./product/syncCategoryAndProducMysqlDataToMongo.sh`: 进行`category mysql services` 切换成` mongodb services`，进行分类数据同步，执行脚本

`./product/syncCategoryAndProductMongoDataToMysql.sh`: 进行`category mongodb services` 切换成` mysql services`，进行分类数据同步，执行的脚本



### 如何设置CRON

cron格式例子：

```
* * * * * /bin/bash /www/web/demo/fecmall/vendor/fancyecommerce/fecshop/shell/order/returnPendingProductQtyStock.sh  >> /www/web_logs/fecerp/task.log 2>&1
```

1.将`/www/web/demo/fecmall`改为您自己的存放fecmall的文件路径

2.您需要创建文件`/www/web_logs/fecerp/task.log`,然后设置log文件可写，cron的执行结果将输出到这个log文件中。

将`returnPendingProductQtyStock.sh`设置为`755`，可以执行权限。

3.将`* * * * * `改为您自己的频率周期，cron周期具体语法说明



从左到右，五个cron字段有不同的意义：

```
分钟：0-59
小时：0-23
日期：1-31
月份：1-12
周几：0-6（0表示周日）
```

*代表为基本单位，譬如`* * * * * `代表每分钟执行一次， `*/5 * * * * `代表每5分钟执行一次，
`10 * * * * `代表每个小时的第10分钟执行，譬如1:10:00,3:10:00,
`1 2 * * * `代表每天的2点1分执行。

更多的语法资料请自行搜索


4.linux执行`crontab -e`，写入计划任务，隔一段时间后，查看log文件，查看是否执行（当然，首先你你的脚本需要有输出内容，
您可以手动执行这个脚本，看到是否有输出内容）

如果log文件中有成功的输出信息，则说明你的cron配置成功


### cron高级使用


我们通过cron周期执行某个脚本，譬如每分钟执行一次，但是会存在某些脚本执行时间过长，一分钟不能
执行完成，如果我们开始下一个脚本，可能会出现脏数据。

我们需要加锁，当上一分钟没有执行完，下一分钟不执行脚本，直至脚本执行完成后，
下一个周期才能执行

如果您的脚本多次执行也没有关系，或者您的间隔很长（譬如一天执行一次），则不需要加锁，下面是关于加锁的cron配置例子

通过linux CRON定时任务执行Task.sh（这个是一个erp里面的例子）

执行crontab -e,进入cron编辑部分，进行脚本添加

```
* * * * * /usr/bin/flock -xn /www/web_logs/task.lock -c '/bin/bash /www/web/demo/fecerp/addons/fecmall/fecerp/shell/task.sh  >> /www/web_logs/fecerp/task.log 2>&1'
```

由于各个task的执行时间有偏差，有时候脚本执行时间比较长，有时间比较短，而我们希望每分钟循环执行一次（增强时效性），因此需要通过锁 机制，当task执行超过一分钟没有完成，那么下一分钟的task执行的时候将会取消，直至当前task执行完成，才会执行下一个task

`/usr/bin/flock -xn /www/web_logs/task.lock -c 'xxxxxxxxxx'`： linux锁机制

`/bin/bash /www/web/demo/fecerp/addons/fecmall/fecerp/shell/task.sh >> /www/web_logs/fecerp/task.log 2>&1`：执行的task.sh文件 路径，以及将执行结果写入到`/www/web_logs/fecerp/task.log`














