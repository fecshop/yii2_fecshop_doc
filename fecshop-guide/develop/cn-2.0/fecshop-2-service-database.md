Fecmall-Service数据库配置
==============



### Service 数据库配置


网站配置--> 基础配置 --> Service数据库配置

这里可以进行数据库的切换

对于`产品分类`部分，当切换数据库后

> 默认全部为mysql，如果您更改成mongodb，您需要安装mongodb，php-mongodb扩展，以及配置mongodb数据库（配置文件：@common/config/main-local.php）

1.同步数据脚本

脚本路径：@fecshop/shell/product

1.1将`mysql产品数据库`同步到`mongodb数据库`

```
sh syncCategoryAndProducMysqlDataToMongo.sh

```

1.2将`mongodb产品数据库`同步到`mysql数据库`

```
sh syncCategoryAndProductMongoDataToMysql.sh

```

2.同步完数据后，您必须执行shell urlRewrite脚本

脚本路径：@fecshop/shell

```

sh urlRewrite.sh

```























