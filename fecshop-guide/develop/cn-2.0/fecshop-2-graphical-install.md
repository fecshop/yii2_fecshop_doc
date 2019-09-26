Fecmall-2.x 安装
============

> Fecmall-2版本，致力于用户体验和应用市场，之前的版本都是脚本配置，现在
可以界面安装fecshop了, Fecmall-2.3.0以上的版本才支持界面安装, 如果是2.3以前的版本，请参看：
[Fecmall-2.x 安装](fecshop-2-about-hand-install.md)
 和 [Fecmall-2.x WAMP环境安装](fecshop-2-about-wamp-install.md)

多种针对性安装方式
-------
 
1.对于熟悉docker的，想要使用docker安装fecmall安装，参看：https://github.com/fecshop/yii2_fecshop_docker

2.对于**纯小白用户**本地window安装，第一次使用wamp安装fecmall，可以参看：
[Fecmall WAMP环境安装](fecshop-2-3-about-wamp-install.md)
,该教程为手把手系列

3.如果是**宝塔用户**，可以参看教程：http://www.fecmall.com/topic/2156

4.下面是标准通用安装教程。
 
 
 **下面是通用教程（标准）：**

下载Fecmall
-----------------

1.通过`composer`安装（**建议下载方式，方便升级**）

1.1安装composer

```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
composer self-update
```

1.2下载fecmall

> 如果是国外的服务器直接安装即可
，如果是国内的服务器，建议切换阿里云的composer源，参看：http://www.fecmall.com/topic/2037



> 请将2.3.0 改成最近的fecmall版本，这里查看最新的版本号： https://github.com/fecshop/yii2_fecshop/releases

**请将2.3.0 改成最近的fecmall版本 **

```
composer create-project fancyecommerce/fecshop-app-advanced  fecmall 2.3.0
cd fecshop
```

2.通过百度网盘下载完整包（QQ群文件也可以下载）

> 不推荐，无法通过composer进行升级, 建议composer下载失败的使用。

下载地址，https://pan.baidu.com/s/1hs1iC2C ， 下载`fecshop-2.x.x.zip` （请下载最高的版本）


Nginx/Apache 域名配置
----------------------

1.准备域名

> Fecmall是一个多入口的电商系统，各个入口独立访问，对应独立的子域名如下：


Pc端：`appfront.fecshoptest.com`

后台：`appadmin.fecshoptest.com`

图片：`img.fecshoptest.com`

H5端: `apphtml5.fecshoptest.com`(如果不安装h5，vue等入口，可以不准备)

移动Api端：`appserver.fecshoptest.com`  (如果不安装微信小程序，vue等入口，可以不准备)
 
第三方数据对接Api端：`appapi.fecshoptest.com` (如果不和第三方系统进行数据对接，可以不准备)

将上面的域名（替换成您自己的域名）解析到您的服务器，
如果您是在本地windows，可以在host文件中做虚拟域名指向127.0.0.1即可（打开文件：C:\Windows\System32\drivers\etc\hosts ，
不熟悉的参看：http://www.fecshop.com/topic/1037 ）




2.Nginx/Apache 做路径指向



> 您可以使用nginx或者apache做服务器，下面将nginx和apache都进行了说明，
下面的`$root`代表fecshop的安装路径，将其缓存您安装的相应的路径即可

`appfront.fecshoptest.com`   >  `$root/appfront/web/`

`appadmin.fecshoptest.com`   >  `$root/appadmin/web/`

`img.fecshoptest.com`   >  `$root/appimage/common/`

`apphtml5.fecshoptest.com`   >  `$root/apphtml5/web/`

`appserver.fecshoptest.com`   >  `$root/appserver/web/`

`appapi.fecshoptest.com`   >  `$root/appapi/web/`

对于Apache和Nginx的配置文件，您可以参看一下下面的例子：

2.1 nginx配置文件


[fecmall nginx default.conf 配置实例](http://www.fecmall.com/topic/2101)


2.2 apache配置文件


[fecmall apache httpd-vhosts.conf 配置实例](http://www.fecmall.com/topic/2100)




配置完成后，重启Nginx/Apache

Fecmal-Init初始化
------------------

1.init 命令行初始化

在fecshop根目录执行init命令，进行初始化

window：运行`init.bat`

linux:运行 `./init`

此命令会进行一些文件复制，一些设置文件权限等，增强安全性。

2.创建Mysql数据库`fecmall`

Fecmall界面安装
----------------

1.在上面的步骤中，配置了nginx/apache, 您配置好域名后，appfront对应域名配置为：`appfront.fecshoptest.com`   >  `$root/appfront/web/`

安装入口文件为：`$root/appfront/web/install.php`
, 打开安装地址： http://appfront.fecshoptest.com/install.php （替换成您自己的域名）


![](images/da1.png)



2.填写mysql的配置，点击提交

![](images/da2.png)

提交后，如图：

![](images/da11.png)

mysql的配置写入了配置文件：`@common/config/main-local.php`

点击按钮： `进行数据表初始化`，需要一段时间执行（请耐心等待），执行完成后的界面如下：


![](images/da12.png)



点击`测试产品数据安装`，完成后界面（如果不想安装测试数据，可以点击`跳过`按钮）

![](images/da13.png)



点击`下一步`按钮，进入完成安装界面

![](images/da15.png)


您可以进入mysql查看一下数据表是否已经创建，然后查看一下`product_flat`表里面是否有数据，进行数据库初始化以及
测试数据安装成功确认。



3.您还需要进行如下的步骤：

3.1需要设置`安全权限`（根目录执行，win不需要执行）：`chmod 644 common/config/main-local.php`

3.2删除安装文件 install.php（**为了安全，一定要删除掉**）(文件路径为：`appfront/web/install.php`),


Fecmall访问后台，进行后台配置
-----------------------

也就是上面配置的域名：`appadmin.fecshoptest.com`

初始账户密码：  `admin`  `admin123`

右上角切换成`中文语言`。

**首先配置图片域名** 

`网站配置`-->`基础配置`-->`基础配置`  找到`图片域名`，填写您的图片域名，譬如：`//img.fecshoptest.com`
(前面不要加`http:`,这种方式http和https都可以调用图片url,将该域名替换成您自己的域名)

![](images/ff1.png)

3.1后台添加`appfront`(PC)配置，添加`store`


`网站配置`-->`Appfront配置`-->`Store配置`

可以看到`store`列表，点击`id为1`的数据（激活状态），进行编辑，将域名更改成 `appfront.fecshoptest.com`(替换成您自己的域名)，保存

然后就可以访问：appfront.fecshoptest.com ，查看pc端了

![](images/ff2.png)


3.2配置Apphtml5

`网站配置`-->`Apphtml5配置`-->`Store配置`

可以看到store列表，点击`id为8`的数据（激活状态），进行编辑，将域名更改成 `apphtml5.fecshoptest.com`(替换成您自己的域名)，保存

然后就可以访问：apphtml5.fecshoptest.com ，查看H5端了

![](images/ff3.png)


3.3配置Appserver


> 这里是对`Appserver`端的配置，对应的域名为：`appserver.fecshoptest.com`(替换成您自己的域名) ,是对微信小程序，vue等客户端提供api的入口

`网站配置`-->`Appappserver配置`-->`Store配置`

将 `Store Key` 更改成 `appserver.fecshoptest.com` (替换成您自己的域名)即可。

![](images/ff5.png)

Appserver 就可以为vue和微信小程序提供api了。

其他的配置
----------------

> 配置完`appserver.fecshoptest.com`，您可以安装vue和微信小程序等客户端

`vue`: https://github.com/fecshop/vue_fecshop_appserver

`微信小程序`：https://github.com/fecshop/wx_micro_program


