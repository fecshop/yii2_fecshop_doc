Fecmall项目迁移服务器
=============

> 本地开发完成后，配置到线上，或者线上换服务器，换域名等等，都是该文章讲述的范畴


### 本地和线上部署

1.对于本地和线上，您可以在本地和线上都部署一份，然后将`更新代码`的部分加入git进行代码更新，这种适合`全新`项目

2.如果您想在服务器安装`fecmall`，然后通过`迁移`的方式, 将安装好的fecmall打包下载到本地安装配置fecmall，或者在本地安装完成，
通过迁移的方式安装到线上，可以参看下面的`项目迁移-服务器之间项目迁移`(把本地看成服务器A即可)

### 项目迁移-服务器之间项目迁移

当我们在`服务器A`安装好fecmall后，我们想要将代码复制到另外的`服务器B`，并且用新的域名，我们需要做
如下的事情


1.将fecmall的`全部代码`打包，上传到`服务器B`

1.1将服务器A的fecmall的根目录打包，上传到服务器B，解压压缩包。

1.2在服务器B，进入解压后的根目录，执行`init`, 重新执行初始化（重新生成cookie key，设置文件权限）

脚本执行过程中，会询问是否覆盖`common/config/main-local.php`,您可以选择`No`（就是按`n`，然后`回车`即可）

```
[root@iZ942k2d5ezZ fecbo]# ./init
Yii Application Initialization Tool v1.0

Which environment do you want the application to be initialized in?

  [0] Development
  [1] Production

  Your choice 0
  Initialize the application under 'Development' environment? yes!
  Start initialization ...

  unchanged appbdmin/config/main-local.php
  unchanged appbdmin/config/params-local.php
  unchanged appbdmin/merge_config.php
  unchanged appbdmin/web/index-merge-config.php
  unchanged appbdmin/web/index.php
      exist common/config/main-local.php
            ...overwrite? [Yes|No|All|Quit] n
       skip common/config/main-local.php
  unchanged common/config/params-local.php
  unchanged appapi/config/main-local.php
  unchanged appapi/config/params-local.php
  unchanged appapi/merge_config.php
  unchanged appapi/web/index-merge-config.php
  unchanged appapi/web/index.php
  unchanged appapi/web/index-test.php
  unchanged apphtml5/config/main-local.php
  unchanged apphtml5/config/params-local.php
  unchanged apphtml5/merge_config.php
  unchanged apphtml5/web/sitemap.xml
  unchanged apphtml5/web/cn/sitemap.xml
  unchanged apphtml5/web/cn/robots.txt
  unchanged apphtml5/web/cn/index.php
  unchanged apphtml5/web/robots.txt
  unchanged apphtml5/web/fr/sitemap.xml
  unchanged apphtml5/web/fr/robots.txt
  unchanged apphtml5/web/fr/index.php
  unchanged apphtml5/web/index-merge-config.php
  unchanged apphtml5/web/index.php
  unchanged apphtml5/web/index-test.php
  unchanged apphtml5/web/sitemap_es.xml
  unchanged console/config/main-local.php
  unchanged console/config/params-local.php
  unchanged appfront/config/main-local.php
  unchanged appfront/config/params-local.php
  unchanged appfront/merge_config.php
  unchanged appfront/web/sitemap.xml
  unchanged appfront/web/cn/sitemap.xml
  unchanged appfront/web/cn/robots.txt
  unchanged appfront/web/cn/index.php
  unchanged appfront/web/robots.txt
  unchanged appfront/web/fr/sitemap.xml
  unchanged appfront/web/fr/robots.txt
  unchanged appfront/web/fr/index.php
  unchanged appfront/web/index-merge-config.php
  unchanged appfront/web/index.php
  unchanged appfront/web/index-test.php
  unchanged appfront/web/sitemap_es.xml
  unchanged appserver/config/main-local.php
  unchanged appserver/config/params-local.php
  unchanged appserver/merge_config.php
  unchanged appserver/web/index-merge-config.php
  unchanged appserver/web/index.php
  unchanged appserver/web/index-test.php
  unchanged appadmin/config/main-local.php
  unchanged appadmin/config/params-local.php
  unchanged appadmin/merge_config.php
  unchanged appadmin/web/index-merge-config.php
  unchanged appadmin/web/index.php
  unchanged appadmin/web/index-test.php
  unchanged tests/codeception/config/config-local.php
  unchanged yii
   generate cookie validation key in appadmin/config/main-local.php
   generate cookie validation key in appbdmin/config/main-local.php
   generate cookie validation key in appapi/config/main-local.php
   generate cookie validation key in appfront/config/main-local.php
   generate cookie validation key in apphtml5/config/main-local.php
   generate cookie validation key in appserver/config/main-local.php
      chmod 0777 appadmin/runtime
      chmod 0777 appadmin/runtime/cache
      chmod 0777 appadmin/runtime/upload
      chmod 0777 appadmin/web/assets
      chmod 0777 appbdmin/runtime
      chmod 0777 appbdmin/runtime/cache
      chmod 0777 appbdmin/web/assets
      chmod 0777 appapi/runtime
      chmod 0777 appapi/runtime/cache
      chmod 0777 appapi/web/assets
      chmod 0777 appfront/runtime
      chmod 0777 appfront/runtime/cache
      chmod 0777 appfront/web/assets
      chmod 0777 appfront/web/install/assets
      chmod 0777 appfront/web/cn/assets
      chmod 0777 appfront/web/fr/assets
      chmod 0777 appfront/web/sitemap.xml
      chmod 0777 appfront/web/sitemap_es.xml
      chmod 0777 appfront/web/fr/sitemap.xml
      chmod 0777 appfront/web/cn/sitemap.xml
      chmod 0777 apphtml5/runtime
      chmod 0777 apphtml5/runtime/cache
      chmod 0777 apphtml5/web/assets
      chmod 0777 apphtml5/web/sitemap.xml
      chmod 0777 apphtml5/web/sitemap_es.xml
      chmod 0777 apphtml5/web/fr/sitemap.xml
      chmod 0777 apphtml5/web/cn/sitemap.xml
      chmod 0777 appserver/runtime
      chmod 0777 appserver/runtime/cache
      chmod 0777 appserver/web/assets
      chmod 0777 appimage/common/media/catalog/product
      chmod 0777 appimage/common/media/catalog/category
      chmod 0777 appimage/common/addons
      chmod 0777 appimage/common/media/upload
      chmod 0777 appimage/common/media/wxmicroqrcode
      chmod 0777 addons
      chmod 0777 common/config/main-local.php
      chmod 0755 yii
      chmod 0755 tests/codeception/bin/yii

  ... initialization completed.

[root@iZ942k2d5ezZ fecbo]# 

```

脚本执行Log分析：

`unchanged`: 代表没有进行改变，保持原装的文件(因为此处是迁移，不是全新安装fecmall，因此是正常的)

`generate cookie`: 代表重新生成了`cookie key`，唯一性保证`cookie`的安全

`chmod`: 设置`文件权限`


总结：`init`这个步骤是`必须要执行`的，这里会初始化`文件权限`，重新生成`cookie key`，保证安全性，一定不要省略。


2.导出mysql代码，在`服务器B`导入数据库

您可以使用mysql命令行，或者使用phpmyadmin等工具进行sql文件的导出和导入


3.在`服务器B`配置nginx，将新域名指向fecmall的相应的web目录，这个在fecmall安装部分都有介绍，
各个域名指向那个`文件路径`，这里不做介绍,需要将`appadmin`，`appfront`, `apphtml5`,` appimage`等等，域名都要配置，
然后`重启nginx`

4.配置数据库，打开`@common/config/main-local.php`, 配置db组件的数据库配置

```
'db' => [ 
    'class' => 'yii\db\Connection',
    'dsn' => 'mysql:host=127.0.0.1;dbname=fecmall',
    'username' => 'root',
    'password' => '123456',
    'charset' => 'utf8',
],
```

将`ip`，`数据库名称`，数据库`用户名`，`密码`（如果数据库的`端口`不是默认，需要设置port），改成`服务器B`的数据库信息



5.后台store域名设置

如果您不做域名更换，那么不需要操作该步骤，只需将域名解析到新的服务器ip即可，
如果您要做域名更换，那么需要执行下面的步骤

访问后台域名，进入后台`配置store`

5.1`appfront`配置：后台菜单，`网站配置` -->  `appfront配置` --> `Store配置`

将域名改成您当前的域名

5.2`apphtml5`配置：后台菜单，`网站配置` -->  `apphtml5配置` --> `Store配置`

将域名改成您当前的域名

5.3`appserver`配置：后台菜单，`网站配置` -->  `appserver配置` --> `Store配置`

将域名改成您当前的域名

5.4`图片域名`配置：
后台菜单，`网站配置` -->  `基础配置` --> `基础配置`

将图片域名改成您目前的域名。

6.对于本地和线上，还要注意安全性，进行: [Fecmall开发环境切换成生产环境](fecmall_env_change.md)

对于网站正式运营，已经要切换成prod生产环境。

7.您可以访问您的前端商城了，查看是否有问题，如果有问题，可以在论坛发帖







































