Fecmall-administer插件安装，升级，卸载部分
==============

> 扩展插件，在安装，升级，卸载等操作，进行sql安装，图片文件复制等初始化操作


### Fecmall-administer文件部分

当您通过gii工具初始化生成扩展插件，进入到 `./addons/您的package包名/您的插件名/administer/` 就可以看到三个文件

 - Install.php   （安装部分）
 
 - Uninstall.php （卸载部分）
 
 - Upgrade.php （升级部分）
 
 相关资料： [Fecmall-应用安装和加载原理](fecmall-addons-developer.md)
 
 
### Install.php 


扩展插件的安装部分，插件第一次安装的时候，会执行该文件里面的run()方法, 进行插件初始化

1.Install.php 例子

```
<?php
/**
 * Fecmall Addons
 */
namespace fectestst\administer;
use Yii;
/**
 * 应用安装类
 * 您可以在这里添加类变量，在配置中的值可以注入进来。
 */
class Install implements \fecshop\services\extension\InstallInterface
{
    // 安装初始版本号，不需要改动，不能为空
    public $version = '1.0.0';
    // 类变量，在config.php中可以通过配置注入值
    public $test;
    
    /**
     * @return mixed|void
     */
    public function run()
    {
        if (!$this->installDbSql()) {
            return false;
        }
        if (!$this->copyImageFile()) {
            return false;
        }
        
        return true;
    }
    
    /**
     * 进行数据库的初始化
     * sql语句执行，多个sql用分号  `;`隔开
     */
    public function installDbSql()
    {
        
        $db = Yii::$app->getDb();
        // 修改表sql
        $sql =  "ALTER TABLE  `customer` ADD  `bdmin_user_id` INT( 11 ) NOT NULL COMMENT  '该用户所属的供应商的id', ADD INDEX (  `bdmin_user_id` )";
        $db->createCommand($sql)->execute();
        
        // 新建表sql
        $sql =  "
            CREATE TABLE IF NOT EXISTS `statistical_bdmin_month` (
                `id` INT( 11 ) NOT NULL AUTO_INCREMENT PRIMARY KEY ,
                `bdmin_user_id` INT( 11 ) NOT NULL COMMENT  '供应商ID',
                `complete_order_total` DECIMAL( 12, 2 ) NULL COMMENT  '完成的订单金额',
                `refund_return_total` DECIMAL( 12, 2 ) NULL COMMENT  '退货-退款总额',
                `month` INT( 5 ) NULL COMMENT  '月份',
                `updated_at` INT( 11 ) NULL COMMENT  '更新时间',
                `created_at` INT( 11 ) NULL COMMENT  '创建时间'
                ) ENGINE = INNODB;
        ";
        $db->createCommand($sql)->execute();
        
        // 后台添加url资源，以及添加admin用户的权限。
        $db->createCommand("INSERT INTO `admin_url_key` (`name`, `tag`, `tag_sort_order`, `url_key`, `created_at`, `updated_at`, `can_delete`) VALUES ('Home Page Config Save', 'config-homepage', 2, '/cms/homepage/managereditsave', 1554107065, 1554117214, 1)")->execute();
        $lastInsertId = $db->getLastInsertID() ;
        $db->createCommand("INSERT INTO `admin_role_url_key` (`role_id`, `url_key_id`, `created_at`, `updated_at`) VALUES (4, " . $lastInsertId . ", 1541129239, 1541129239)")->execute();
        
        
        return true;
    }
    
    /**
     * 复制图片文件到appimage/common/addons/{namespace}，如果存在，则会被强制覆盖
     */
    public function copyImageFile()
    {
        /*
        $sourcePath = Yii::getAlias('@fectestst/app/appimage/common/addons/fectestst');
        
        Yii::$service->extension->administer->copyThemeFile($sourcePath);
        */
        return true;
    }
    
}
```


插件安装的时候，会执行`run()`方法，因此插件初始化需要执行的内容，您都写到run方法里面

```
public function run()
    {
        if (!$this->installDbSql()) {
            return false;
        }
        if (!$this->copyImageFile()) {
            return false;
        }
        
        return true;
    }
```


`installDbSql()`函数是安装数据库sql的函数，`copyImageFile()`函数是复制图片文件到图片文件`appimage/common`下的函数（图片域名对应的文件路径）

2.扩展安装sql部分`installDbSql()`函数

2.1执行安装sql语句

`$db = Yii::$app->getDb();`：是yii2框架的函数，获取db组件

`$db->createCommand($sql)->execute();`: 执行sql语句

2.2添加后台权限资源


```
// 后台添加url资源，以及添加admin用户的权限。
$db->createCommand("INSERT INTO `admin_url_key` (`name`, `tag`, `tag_sort_order`, `url_key`, `created_at`, `updated_at`, `can_delete`) VALUES ('Home Page Config Save', 'config-homepage', 2, '/cms/homepage/managereditsave', 1554107065, 1554117214, 1)")->execute();
$lastInsertId = $db->getLastInsertID() ;
$db->createCommand("INSERT INTO `admin_role_url_key` (`role_id`, `url_key_id`, `created_at`, `updated_at`) VALUES (4, " . $lastInsertId . ", 1541129239, 1541129239)")->execute();
```

第一个sql是在`admin_url_key`表中新建url资源

第二个sql是将`admin_url_key` 的id ， 和 用户权限组id进行关联，数据写入到`admin_role_url_key`。

2.2.1开发新功能，后台新建url资源

当您进行开发扩展插件，在fecmall后台开发了新的菜单功能，新建了新的`controller`，就意味着新的url 资源建立，
fecmall后台部分是RBAC权限控制，因此您可以在fecmall后台新建url资源，并将其添加到相应的用户权限组

`控制面板` --> `后台用户` -->  `资源管理` 进行操作，关于菜单资源权限管理，详细资料：
[Fecmall 后台菜单RBAC](http://www.fecmall.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_admin_rbac.html)




2.2.1将后台新建的url资源，搞成sql，写入到`installDbSql()`函数，扩展插件安装过程中自动执行sql


fecmall的url资源以及权限对应关系，是存储到mysql里面的，因此在插件初始化的时候，需要用sql安装，
您打开数据表：`admin_url_key`，您可以看到新建的资源，你可以以上面的例子，将数据搞成sql，进行安装

通过phpmysql导出sql

```

INSERT INTO `admin_url_key` (`id`, `name`, `tag`, `tag_sort_order`, `url_key`, `created_at`, `updated_at`, `can_delete`) VALUES
(1, 'Account List', 'dashboard_user_account_manager', 2, '/fecadmin/account/manager', 1511948105, 1540730009, 1),
```

转换：

```
$db->createCommand("INSERT INTO `admin_url_key` (`name`, `tag`, `tag_sort_order`, `url_key`, `created_at`, `updated_at`, `can_delete`) VALUES ( 'Account List', 'dashboard_user_account_manager', 2, '/fecadmin/account/manager', 1511948105, 1540730009, 1)")->execute();
$lastInsertId = $db->getLastInsertID() ;
$db->createCommand("INSERT INTO `admin_role_url_key` (`role_id`, `url_key_id`, `created_at`, `updated_at`) VALUES (4, " . $lastInsertId . ", 1541129239, 1541129239)")->execute();

```

2.2.3转换工具

当您写了很多的url资源，手动转换非常费劲，您可以使用fecmall的工具生成，

譬如：您建立100多个url资源，可以通过phpmysql获得导出语句，然后通过该工具一次得到转换后的语句，复制上去就可

详细参看：[Fecmall-后台菜单Admin Url Key Gii工具](fecmall-addons-developer-admin-url-key-tools.md)



### Uninstall.php

卸载插件扩展执行的函数

按照逻辑，在install.php部分安装的sql，应该在卸载的时候执行sql删除，
但是这个是一个比较危险的操作，如果运营一段时间的站点误操作，将会导致出问题，
因此卸载部分，terry开发的扩展一般不会写sql删除的操作

但是，terry开发的扩展虽然没有实现sql删除，但是，如果您有sql删除的需求，可以在
`uninstallDbSql`函数里面写上删除的sql语句


Uninstall.php文件例子：

```
<?php
/**
 * Fecmall Addons
 */
namespace fectestst\administer;
use Yii;
/**
 * 应用安装类
 * 您可以在这里添加类变量，在配置中的值可以注入进来。
 */
class Uninstall implements \fecshop\services\extension\UninstallInterface
{
    
    /**
     * 应用执行卸载的步骤执行的函数。
     */
    public function run()
    {
        if (!$this->uninstallDbSql()) {
            return false;
        }
        if (!$this->removeImageFile()) {
            return false;
        }
        return true;
    }
    
    public function uninstallDbSql()
    {
        /*
        $sql = "
        //    DROP TABLE IF EXISTS `fecmall_addon_test1`;
        //    DROP TABLE IF EXISTS `fecmall_addon_test2`;
        ";
        // 执行sql, 创建表结构的时候，这个函数会返回0，因此不能以返回值作为return
        Yii::$app->getDb()->createCommand($sql)->execute();
        */
        
        return true;
    }
    
    public function removeImageFile()
    {
        /*
        return Yii::$service->extension->administer->removeThemeFile();
        */
        
        return true;
    }
}
```




### Upgrade.php 升级文件

当扩展插件发布后，后续会继续迭代开发，进行升级，升级过程中，会有sql安装，图片复制等操作，
您可以把升级的部分，写到Upgrade.php中。

如果您当前的升级，`不需要进行sql安装`，那么就不需要在这里添加升级代码了

Upgrade.php文件例子：


```
<?php
/**
 * Fecmall Addons
 */
namespace fectestst\administer;
use Yii;
/**
 * 应用安装类
 * 您可以在这里添加类变量，在配置中的值可以注入进来。
 */
class Upgrade implements \fecshop\services\extension\UpgradeInterface
{
    /**
     * @var array
     * 必须按照版本号依次填写，否则升级会导致问题。
     * 如果安装的初始版本号为1.0.0，那么下面的升级版本号必须比初始版本号大才行
     */
    public $versions = [
        '1.0.1',
        '1.0.2',
        '1.0.3',
    ];
    
    /**
    * @param $version  最新版本号
    * @return boolean
    *  升级执行的函数，您可以在各个版本号需要执行的部分写入相应的操作。
    */
    public function run($version)
    {
        /**
         * 下面仅仅是一个sql例子，您可以将其换成您自己要升级的内容
         */
        switch ($version)
        {
            case '1.0.1' :
                $this->upgrade101();
                break;
            case '1.0.2' :
                $this->upgrade102();
                break;
            case '1.0.3' :
                $this->upgrade103();
                break;
        }
        
        return true;
    }
    // 1.1.0
    public function upgrade110()
    {
        // 增加测试 - 冗余的字段
        $db = Yii::$app->getDb();
        $sql = "ALTER TABLE fecmall_addon_test1 ADD COLUMN redundancy_field_5255 varchar(48);";
        $db->createCommand($sql)->execute();
    }
    
    // 1.2.0
    public function upgrade102()
    {
        // 删除测试 - 冗余的字段
        $db = Yii::$app->getDb();
        $sql = "ALTER TABLE fecmall_addon_test1 ADD COLUMN redundancy_field_566 varchar(48);";
        $db->->createCommand($sql)->execute();
    }
    
    
    
    /**
     * 复制图片文件到appimage/common/addons/{namespace}，如果存在，则会被强制覆盖
     */
    public function copyImageFile()
    {
        /*
        $sourcePath = Yii::getAlias('@fectestst/app/appimage/common/addons/fectestst');
        
        Yii::$service->extension->administer->copyThemeFile($sourcePath);
        */
        return true;
    }
    
    
}
```

1.关于升级版本号

`升级版本号命名`：初次发版的扩展插件，命名版本号为：`1.0.0`, 而对于升级的版本，您可以自由命名，譬如：`1.1.0` ， `1.0.1`，
只要保证升级的版本号大于当前的版本号即可

`版本号一致性`：您在Upgrade.php写的版本号，要和fecmall应用市场上传扩展zip压缩包的版本号一致

2.升级代码详细步骤

假设您现在的版本号是`1.0.0`，升级的版本号为`1.1.0`

2.1在类变量$versions数组中添加新的版本号。如下：（后续如果继续升级，在该类变量数组中继续添加子项即可）

```
public $versions = [
    '1.1.0',
    // '1.2.0',
];
```

2.2在run方法里面，通过 $version 参数，进行判断执行相应的函数

```
public function run($version)
{
    /**
     * 下面仅仅是一个sql例子，您可以将其换成您自己要升级的内容
     */
    switch ($version)
    {
        case '1.1.0' :
            $this->upgrade110();
            break;
        // case '1.2.0' :
        //     $this->upgrade120();
        //     break;
        // case '1.3.0' :
        //     $this->upgrade130();
        //     break;
    }
    
    return true;
}
```


2.3新建方法：upgrade110()


```
// 1.1.0
    public function upgrade110()
    {
        // 增加测试 - 冗余的字段
        $db = Yii::$app->getDb();
        $sql = "ALTER TABLE fecmall_addon_test1 ADD COLUMN redundancy_field_5255 varchar(48);";
        $db->createCommand($sql)->execute();
    }
```

执行相关操作即可，里面执行sql，复制图片等，和Install.php里面是一样的。




至此，插件安装，卸载，升级部分已介绍完毕。
































