Fecmall-2.x 安装
============

> Fecmall-2版本，致力于用户体验和应用市场，之前的版本都是脚本配置，现在
可以界面安装fecmall了, Fecmall-2.3.0以上的版本才支持界面安装, 如果是2.3以前的版本，请参看：
[Fecmall-2.x 安装](fecshop-2-about-hand-install.md)
 和 [Fecmall-2.x WAMP环境安装](fecshop-2-about-wamp-install.md)

多种针对性安装方式（具体环境）
-------
 
1.对于熟悉docker的，想要使用docker安装fecmall安装，参看：https://github.com/fecshop/yii2_fecshop_docker

2.对于**纯小白用户**本地window安装，第一次使用wamp安装fecmall，可以参看：
[Fecmall WAMP环境安装](fecshop-2-3-about-wamp-install.md)
,该教程为手把手系列

3.对于**纯小白用户**线上linux安装，fecmall以宝塔插件的方式做了一键部署：

【fecmall宝塔控制面板安装文档：**一键部署，最新**】：[Fecmall-2.x 宝塔一键部署安装](fecshop-2-graphical-bt-install.md)

[Fecmall宝塔面板部署视频](http://www.fecmall.com/topic/4262)

4.下面是标准通用安装教程 - 标准通用。
 

下载Fecmall
-----------------

**下载方式一**：通过`composer`在线安装下载（**建议下载方式，方便升级**）

1.1安装composer

```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
composer self-update
```

1.2下载fecmall

> 如果是国外的服务器直接安装即可
，如果是国内的服务器，建议切换阿里云的composer源，参看：http://www.fecmall.com/topic/2037



> 请将2.12.1 改成最近的fecmall版本，这里查看最新的版本号： https://github.com/fecshop/yii2_fecshop/releases

**请将2.12.1 改成最近的fecmall版本 **

```
composer create-project fancyecommerce/fecshop-app-advanced  fecmall 2.12.1
cd fecshop
```

**下载方式二**：直接下载完整`Zip压缩包`

> 如果您网络不好，那么可以下载zip完整包，但是升级还是需要使用composer


阿里OSS下载地址【阿里云付费OSS，速度比较块，这个地址是目前最高的版本】：https://fecmall-download.oss-cn-shenzhen.aliyuncs.com/download/fecmall-lasted.zip



Nginx/Apache 域名配置
----------------------

1.准备域名

> Fecmall是一个多入口的电商系统，各个入口独立访问，对应独立的子域名如下：


Pc端【必须】：`www.fecshoptest.com`

后台【必须】：`appadmin.fecshoptest.com`

图片【必须】：`img.fecshoptest.com`

H5端【选填】: `m.fecshoptest.com`(如果不安装h5，vue等入口，可以不准备)

移动Api端【选填】：`appserver.fecshoptest.com`  (如果不安装微信小程序，vue等入口，可以不准备)
 
第三方数据对接Api端【选填】：`appapi.fecshoptest.com` (如果不和第三方系统进行数据对接，可以不准备)

多商户经销商后台【选填】：`appbdmin.fecshoptest.com` (如果不安装fecbbc多商户扩展，可以不准备)

将上面的域名（替换成您自己的域名）解析到您的服务器，
如果您是在本地windows，可以在host文件中做虚拟域名指向127.0.0.1即可（打开文件：C:\Windows\System32\drivers\etc\hosts ，
不熟悉的参看：http://www.fecmall.com/topic/4203 ）




2.Nginx/Apache 做路径指向



> 您可以使用nginx或者apache做服务器，下面将nginx和apache都进行了说明，
下面的`$root`代表fecshop的安装路径，将其缓存您安装的相应的路径即可

`www.fecshoptest.com`   >  `$root/appfront/web/`

`appadmin.fecshoptest.com`   >  `$root/appadmin/web/`

`img.fecshoptest.com`   >  `$root/appimage/common/`

`m.fecshoptest.com`   >  `$root/apphtml5/web/`

`appserver.fecshoptest.com`   >  `$root/appserver/web/`

`appapi.fecshoptest.com`   >  `$root/appapi/web/`

`appbdmin.fecshoptest.com`   >  `$root/appbdmin/web/`

对于Apache和Nginx的配置文件，您可以参看一下下面的例子：

2.1 nginx配置文件，您可以参考下面的config例子


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


准备好这些后，就可以通过web浏览器界面安装fecmall了，详细参看：[Fecmall-2.x 界面安装](fecshop-2-graphical-web-install.md)












