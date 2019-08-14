Fecmall-2.x 安装
==============

> 由于Fecmall在1版本上面的改动比较大，因此建议重新安装Fecmall-2.x，不建议从Fecmall-1版本升级。


关于Fecmall-2.x 安装
--------------------

1.如果是windows安装，建议使用WAMP来安装，教程参看：[Fecmall-2.x WAMP环境安装 - 手把手系列](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecshop-2-about-wamp-install.html)

2.如果使用docker安装，参看文档：[Fecmall Docker 安装](https://github.com/fecshop/yii2_fecshop_docker)

3.如果想在linux上面直接安装，可以参看本章下面的教程

下载 Fecmall-2.x 
----------------

### 1.Fecmall源文件下载

1.1通过`composer`安装（**建议下载方式，方便升级**）

安装composer

```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
composer self-update
```

1.2安装Fecmall

如果是国外的服务器直接安装即可
，如果是国内的服务器，建议切换阿里云的composer源，参看：http://www.fecmall.com/topic/2037

> 请将2.1.6 改成最近的fecmall版本，这里查看最新的版本号： https://github.com/fecshop/yii2_fecshop/releases

```
composer create-project fancyecommerce/fecshop-app-advanced  fecshop 2.1.6
cd fecshop
```

### 2.通过百度网盘下载完整包（QQ群文件也可以下载）

>不推荐，无法通过composer进行升级, 建议composer下载失败的使用。

下载地址，https://pan.baidu.com/s/1hs1iC2C ， 下载`fecshop-2.x.x.zip` （请下载最高的版本）


准备域名，以及nginx配置
------------------

### 1.域名准备

> 如果是windows本地，可以在host文件中做域名指向127.0.0.1即可（打开文件：C:\Windows\System32\drivers\etc\hosts ，不熟悉的参看：http://www.fecshop.com/topic/1037 ）


Pc端：`appfront.fecshoptest.com`

后台：`appadmin.fecshoptest.com`

图片：`img.fecshoptest.com`

H5端: `apphtml5.fecshoptest.com`

移动Api端：`appserver.fecshoptest.com`  (如果不安装微信小程序，vue等入口，可以不准备)
 
第三方数据对接Api端：`appapi.fecshoptest.com` (如果不和第三方系统进行数据对接，可以不准备)



### 2.nginx做路径指向

>下面的`$root`代表fecshop的安装路径，将其缓存您安装的相应的路径即可

`appfront.fecshoptest.com`   >  `$root/appfront/web/`

`appadmin.fecshoptest.com`   >  `$root/appadmin/web/`

`img.fecshoptest.com`   >  `$root/appimage/common/`

`apphtml5.fecshoptest.com`   >  `$root/apphtml5/web/`

`appserver.fecshoptest.com`   >  `$root/appserver/web/`

`appapi.fecshoptest.com`   >  `$root/appapi/web/`



nginx需要做去掉`index.php`的配置，详细参考帖子：http://www.fecshop.com/topic/398  ，  http://www.fecshop.com/topic/392


配置完成后，重启nginx

安装 Fecmall-2.x 
--------

### 1.init 命令行初始化

> window：运行`init.bat`，linux:运行 `./init`

在fecshop根目录执行  `./init`,  然后命令提示符，填写 `0` （develop开发模式）， `yes` 即可完成初始化

log日志可以参看：http://www.fecshop.com/topic/2003

### 2.初始化数据库

2.1创建数据库`Fecmall`

2.2配置填写：

打开 `@common/config/main-local.php`，进行mysql配置

```
 'db' => [ 
    'class' => 'yii\db\Connection',
    'dsn' => 'mysql:host=127.0.0.1;dbname=fecmall',
    'username' => 'root',
    'password' => 'xxxxxx',
    'charset' => 'utf8',
]
```

2.3初始化Mysql数据库

```
./yii migrate --interactive=0 --migrationPath=@fecshop/migrations/mysqldb
```

2.4添加测试数据

产品测试数据图片百度网盘下载地址：https://pan.baidu.com/s/1hs1iC2C ，下载：fecshop-2.x测试数据.zip （QQ群文件也可以下载）
解压后，里面有`appimage`(测试产品图片) 和 `fecshop.sql`（测试sql文件） 

2.4.1将`appimage`文件夹复制到`fecshop根目录`

2.4.2将`fecshop.sql`导入到数据库`fecmall`中



### 3.访问后台

也就是上面配置的域名：`appadmin.fecshoptest.com`

初始账户密码：  `admin`  `admin123`

右上角切换成`中文语言`。

**首先配置图片域名** 

网站配置-->基础配置-->基础配置  找到图片域名，填写您的图片域名，譬如：`//img.fancyecommerce.com`
(前面不要加`http:`,这种方式http和https都可以调用图片url)

![](images/ff1.png)


3.1后台添加`appfront`(PC)配置，添加`store`

> 这里是对pc端的配置，对应的域名为：`appfront.fecshoptest.com`

`网站配置`-->`Appfront配置`-->`Store配置`

可以看到`store`列表，点击`id为1`的数据（激活状态），进行编辑，将域名更改成 `appfront.fecshoptest.com`，保存

然后就可以访问：appfront.fecshoptest.com ，查看pc端了

![](images/ff2.png)


3.2配置Apphtml5


> 这里是对`html5`端的配置，对应的域名为：`apphtml5.fecshoptest.com`

`网站配置`-->`Apphtml5配置`-->`Store配置`

可以看到store列表，点击`id为8`的数据（激活状态），进行编辑，将域名更改成 `apphtml5.fecshoptest.com`，保存

然后就可以访问：apphtml5.fecshoptest.com ，查看H5端了

![](images/ff3.png)


3.3配置Appserver


> 这里是对`Appserver`端的配置，对应的域名为：`appserver.fecshoptest.com` ,是对微信小程序，vue等客户端提供api的入口

`网站配置`-->`Appappserver配置`-->`Store配置`

将 `Store Key` 更改成 `appserver.fecshoptest.com` 即可。


![](images/ff5.png)

Appserver 就可以为vue和微信小程序提供api了。

### 4.其他的配置

> 配置完`appserver.fecshoptest.com`，您可以安装vue和微信小程序等客户端

`vue`: https://github.com/fecshop/vue_fecshop_appserver

`微信小程序`：https://github.com/fecshop/wx_micro_program

















