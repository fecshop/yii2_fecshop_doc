Fecshop-使用Xunsearch
==============

### Fecshop-使用Xunsearch

1.安装xunsearch

[XunSearch 安装教程](http://www.fancyecommerce.com/2016/09/24/xunsearch-%E5%AE%89%E8%A3%85%EF%BC%8C%E4%BD%BF%E7%94%A8/)

2.添加hosts

首先，先添加一下host vim /etc/hosts, 添加下面的host映射，:wq 保存退出即可

```
127.0.0.1    xunsearch
```


3.对于产品搜索，Xunsearch只支持中文， xunSearch安装教程 ,安装完成后，需要跑脚本同步到搜索工具中，命令行如下：

```
cd vendor/fancyecommerce/fecshop/shell/search
sh fullSearchSync.sh
```






