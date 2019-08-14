Fecmall-使用Mongodb
============


### Fecmall-使用Mongodb

1.安装Mongodb

2.安装php扩展 `php-mongodb`,   ！！！！注意，不是`php-mongo`，一定要看清楚

3.安装Yii2 Mongodb扩展包: https://github.com/yiisoft/yii2-mongodb

打开composer.json 添加：

```
"yiisoft/yii2-mongodb": "~2.1.7",
```

然后执行 `composer update`


4.Fecmall配置mongodb

打开文件：`@common/config/main-local.php`


```
'mongodb' => [
    'class' => 'yii\mongodb\Connection',
    # 有账户的配置
    //'dsn' => 'mongodb://username:password@localhost:27017/datebase',
    # 无账户的配置
    'dsn' => 'mongodb://127.0.0.1:27017/fecshop_test_2017_04_19',
    # 复制集
    //'dsn' => 'mongodb://10.10.10.252:10001/erp,mongodb://10.10.10.252:10002/erp,mongodb://10.10.10.252:10004/erp?replicaSet=terry&readPreference=primaryPreferred',
],

```

配置即可。

5.如果使用mongodb搜索

需要同步数据到mongodb的搜索引擎


```
cd vendor/fancyecommerce/fecshop/shell/search
sh fullSearchSync.sh
```



### 使用mongodb 

配置mongodb作为存储引擎，产品分类数据进行数据同步，可以参看：[Fecshop-Service数据库配置](fecshop-2-service-database.md)
























