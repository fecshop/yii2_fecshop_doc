Fecmall-使用Mongodb
============


### Fecmall数据库发展简介

1.目前Fecmall是2版本，默认全部使用mysql

2.如果您玩过fecmall-1版本，您肯定了解，对于一版本，必须使用双数据库，对于涉及到事务操作的表，譬如cart，order表，
放到了mysql中，而非事务的表，譬如product，category，review，cms等放到了mongdob中，
好处是最大化的利用各个数据库的优势，增强并发，但是，带来了配置繁琐，对小白以及初级程序员使用不友好，
因此，fecmall对mongodb实现的services，使用mysql进行了实现，默认只需要mysql即可

3.如果您公司或者您个人有一定的开发能力，网站有一定的并发要求，那么您可以使用mongodb来替代一部分的mysql存储，
在使用前，您需要进行如下的配置



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


5.mongodb数据库初始化(导入mongodb的表，数据，索引):


```
./yii mongodb-migrate  --interactive=0 --migrationPath=@fecshop/migrations/mongodb
```

如果Mongodb migrate报错：PHP Compile Error 'yii\base\ErrorException' with message 'require_once(): Failed opening required 'Array/m170228_072455_fecshop_tables.php' (include_path='.:')' 可以参看这里解决：http://www.fecshop.com/topic/45


6.如果使用mongodb搜索

需要同步数据到mongodb的搜索引擎


```
cd vendor/fancyecommerce/fecshop/shell/search
sh fullSearchSync.sh
```



### 使用mongodb 

配置mongodb作为存储引擎，产品分类数据进行数据同步，可以参看：[Fecshop-Service数据库配置](fecshop-2-service-database.md)
























