fecmall search:删除xunsearch所有数据的脚本
=========================

> 清空xunsearch所有数据的脚本


### 配置

无需配置，直接执行脚本即可，执行后，将
清空xunsearch里面所有的数据。


### 执行

```
cd vendor/fancyecommerce/fecshop/shell/search
sh deleteXunSearchAllData.sh
```


执行log

```
[root@iZ942k2d5ezZ search]# sh deleteXunSearchAllData.sh 
There are 1 pages to check if is delete in xunSearch
##############ALL BEGINING###############
begin delete Xun Search Date 
Page 1 done
[root@iZ942k2d5ezZ search]# 
```

xunsearch目前只设置了支持中文搜索，其他的外文用的是mongodb，
删除xunsearch后，您需要重新跑一下搜索数据同步脚本
[search:产品同步到搜索的脚本](fecshop-console-search-sync.md)


