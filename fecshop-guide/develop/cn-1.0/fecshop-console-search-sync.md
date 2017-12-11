search:产品同步到搜索的脚本
=========================

> 将产品信息同步到搜索工具的脚本

### 介绍

执行该脚本，会将产品表的数据同步到搜索工具中，
同步的过程中会更新updated_at字段，
在同步完成后，会将同步时间小于脚本开始时间的数据删除掉，因为没有
被同步的数据说明在产品表中已经不存在了。

另外，对于产品编辑保存，在save方法中，会同步产品的信息到搜索工具中，
不过，不排除异常情况和有时候初始化数据，因此，
当前的脚本还是很有必要的

### 配置

无

### 执行

```
cd vendor/fancyecommerce/fecshop/shell/search
sh fullSearchSync.sh
```


执行log

```
[root@iZ942k2d5ezZ search]# sh fullSearchSync.sh 
There are 40 products to process
There are 1 pages to process
##############ALL BEGINING###############
Page 1 done
begin delete Mongodb Search Date 
##############ALL COMPLETE###############
[root@iZ942k2d5ezZ search]#
```


