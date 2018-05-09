fecshop 升级
=============

> 当fecshop代码更新后可以通过composer更新


### 1.原理

入口包部分，github地址为：
https://github.com/fancyecommerce/yii2_fecshop_app_advanced
也就是安装fecshop后，除了vendor以外的所有文件，都是入口包文件，
打开根目录下面的composer.json文件可以看到如下内容：

```
"require": {
	"php": ">=5.4.0",
	"yiisoft/yii2": ">=2.0.6",
	"yiisoft/yii2-bootstrap": "*",
	"yiisoft/yii2-swiftmailer": "*",
	"yiisoft/yii2-apidoc": "~2.0.0",
	"fancyecommerce/fecshop": ">=1.1.2.9"
   
},
```

通过上面可以看到 fecshop 和 yii2 都是一个composer包，通过包依赖的方式
加载过来。

### 2.升级

#### 2.1 yii2_fecshop_app_advanced包：

通过上面，我们了解了原理，yii2_fecshop_app_advanced 入口包是无法升级的，
因为很多的本地化配置都在里面，升级将导致全体被覆盖。
幸运的是，这个包作为入口部分，很少改动，可以在
https://github.com/fancyecommerce/yii2_fecshop_app_advanced/commits/master
查看各次提交对应的修改，然后手动复制到相应文件即可。

#### 2.2 核心包以及第三方包升级：

打开根目录下面的composer.json配置文件，
找到下面的代码

```
"require": {
	"php": ">=5.4.0",
	"yiisoft/yii2": ">=2.0.6",
	"yiisoft/yii2-bootstrap": "*",
	"yiisoft/yii2-swiftmailer": "*",
	"yiisoft/yii2-apidoc": "~2.0.0",
	"fancyecommerce/fecshop": ">=1.1.2.9"
   
},
```

更改相应的版本号，然后在根目录下面执行`composer update` 即可。

譬如我想升级fecshop，我访问
https://github.com/fancyecommerce/yii2_fecshop/releases，
查看最新的版本号，和当前文件的版本号是否一致，如果不一致，
将`"fancyecommerce/fecshop": ">=1.1.2.9"` 这行中的`1.1.2.9`
改成最新的
，当然，yii2框架也是这个原理，修改下版本号。

然后在根目录下面执行`composer update`即可完成升级。

**开发注意：** vendor下面的文件不要做改动，如果修改功能，需要按照文档的说明
在二开路径进行覆盖重写，如果您修改了vendor下面的内容，那么，下次升级的时候，
将会把您改动的内容全部覆盖掉，您写的代码将全部清空。这个需要切记！

#### 2.3 通过Migrate升级数据库部分

如果您有重要数据，切记先备份数据库

每次版本更新，虽然不一定有数据库的更新，但是您都需要执行一下下面的更新语句（在
fecshop根目录下面执行）。

mysql 升级：

```
./yii migrate --interactive=0 --migrationPath=@fecshop/migrations/mysqldb
```

mongodb 升级

```
./yii mongodb-migrate  --interactive=0 --migrationPath=@fecshop/migrations/mongodb
```
























