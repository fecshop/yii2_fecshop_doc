Fecmall扩展-ElasticSearch搜索插件
=================

> 通过elasticSearch进行搜索

### ElasticSearch搜索扩展介绍

elasticSearch是非常强大的搜索引擎，对于并发高的搜索可以提供强有力的支撑，但是，
es非常耗费资源，对内存要求高，因此不适合小站，一般8G内存以上，并且搭建集群的方式玩，
对于小站，中文搜索用xunsearch即可。


### 插件安装

1.首先，需要安装yii2-elasticsearch扩展

```
composer require --prefer-dist yiisoft/yii2-elasticsearch:"2.1.x-dev"
```

下载log

```
[root@iZ942k2d5ezZ fecbvc]# composer require --prefer-dist yiisoft/yii2-elasticsearch:"2.1.x-dev"
Do not run Composer as root/super user! See https://getcomposer.org/root for details
./composer.json has been updated
Loading composer repositories with package information
Updating dependencies (including require-dev)
Package operations: 1 install, 0 updates, 0 removals
  - Installing yiisoft/yii2-elasticsearch (2.1.x-dev c9ef932): Downloading (100%)         
Package codeception/base is abandoned, you should avoid using it. No replacement was suggested.
Package phpoffice/phpexcel is abandoned, you should avoid using it. Use phpoffice/phpspreadsheet instead.
Writing lock file
Generating autoload files
```


安装成功后，可以在vendor/yiisoft/看到文件夹 `yii2-elasticsearch`


2.应用市场：http://addons.fecmall.com/44669378

购买后，即可进入fecmall后台应用中心，在线安装扩展


### 环境搭建


1.安装elasticSearch并启动

安装elasticSearch-6版本，详细参看文档：http://www.fecmall.com/topic/672

安装完成后一定要启动es

2.配置


2.1Enable `ElasticSearch Engine`
`网站配置` --> `基础配置` -->    `搜索引擎配置`

将 `ElasticSearch Engine` 设置为： `Enable`

2.2中文搜索设置为`elasticSearch`

`网站配置` --> `基础配置` -->    `多语言配置`


将语言`zh-CN`对应的搜索引擎设置为`elasticSearch`


2.3配置文件 `@common/config/main-local.php`

在组件`components`配置数组中添加elasticSearch的配置

```
'elasticsearch' => [
    'class' => 'yii\elasticsearch\Connection',
    'nodes' => [
        ['http_address' => '127.0.0.1:9200'],
        // configure more hosts if you have a cluster
    ],
],
``` 


### 数据同步


1.新建mapping

进入网站根目录执行

```
./yii elasticsearch/updatemapping
```


2.执行数据同步

```
cd  ./vendor/fancyecommerce/fecshop/shell/search
sh fullSearchSync.sh

```

3.可以进入网站中文store查看搜索结果了




补充：清空elasticSearch数据

进入网站根目录执行

```
./yii elasticsearch/clean
```


到这里就完成了，中文分词默认使用的是`cjk analysis`,结果也还行




4.如果您想要使用elasticSearch 安装中文分词器 IK Analysis

> 不清楚是内存太小还是其他原因，我安装了这个中文分词插件，elasticSearch很卡，因此这个我暂时没验证结果，您可以自行验证

可以参看这个帖子：http://www.fecmall.com/topic/2489










