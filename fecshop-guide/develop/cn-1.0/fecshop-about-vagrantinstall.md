Fecshop vagrant安装
====================

> Vagrant是一个基于Ruby的工具，用于创建和部署虚拟化开发环境。
>它 使用Oracle的开源VirtualBox虚拟化系统，使用 Chef创建自动化虚拟环境。

1. vagrant 教程

你可能没有使用vagrant，这个没有关系，我整理了一份vagrant使用的教程，地址如下：
[vagrant 下载部署linux环境](http://www.fancyecommerce.com/2016/09/22/vagrant-%E4%B8%8B%E8%BD%BD%E9%83%A8%E7%BD%B2linux%E7%8E%AF%E5%A2%83/)


2. 添加Fecshop 环境的box

配置环境比较复杂，我本地已经配置好了fecshop的环境，并打包成一个box，
地址在百度云盘，下载地址为：https://pan.baidu.com/s/1kVwRD2Z， 
进入后打开文件夹，下载 package.box，根据上面的教程加载进来box即可。

安装完成后，各个入口的域名和对应的文件路径为：

```
pc端地址：appfront.fecshoptest.com appfront.fecshoptest.es 指向 /www/web/develop/fecshop/appfront/web 

后台端地址：appadmin.fecshoptest.com 指向/www/web/develop/fecshop/appadmin/web

html5端地址（未开发）：apphtml5.fecshoptest.com 指向/www/web/develop/fecshop/apphtml5/web

api端地址（未开发）：appapi.fecshoptest.com     指向/www/web/develop/fecshop/appapi/web

手机app端地址（未开发）：appserver.fecshoptest.com 指向/www/web/develop/fecshop/appserver/web

common图片端地址：img.fecshoptest.com     指向/www/web/develop/fecshop/appimage/common

appadmin图片端地址：img2.fecshoptest.com  指向/www/web/develop/fecshop/appimage/appadmin

appfront图片端地址：img3.fecshoptest.com  指向/www/web/develop/fecshop/appimage/appfront

apphtml5图片端地址：img4.fecshoptest.com  指向/www/web/develop/fecshop/appimage/apphtml5

appserver图片端地址：img5.fecshoptest.com     指向/www/web/develop/fecshop/appimage/appserver

rock mongo访问地址：rock.fecshoptest.com    账号：admin  密码：123456

phpmyadmin访问地址: my.fecshoptest.com      账号：root   密码：123456

后台端地址：appadmin.fecshoptest.com访问后，后台的用户名和密码为admin  123456
```

上面的域名需要本地windows添加hosts

打开C:\Windows\System32\drivers\etc\hosts，添加如下代码（如果是其他IP，将
127.0.0.1 替换成其他IP即可。）：

```
127.0.0.1       rock.fecshoptest.com
127.0.0.1       my.fecshoptest.com
127.0.0.1       appadmin.fecshoptest.com
127.0.0.1       appfront.fecshoptest.com
127.0.0.1       appfront.fecshoptest.es
127.0.0.1       apphtml5.fecshoptest.com
127.0.0.1       appapi.fecshoptest.com
127.0.0.1       appserver.fecshoptest.com
127.0.0.1       img.fecshoptest.com		#appimage/common
127.0.0.1       img2.fecshoptest.com	#appimage/appadmin
127.0.0.1       img3.fecshoptest.com	#appimage/appfront
127.0.0.1       img4.fecshoptest.com	#appimage/apphtml5
127.0.0.1       img5.fecshoptest.com	#appimage/appserver
```


这样就可以访问了，譬如：appfront.fecshoptest.com 访问前端pc web，
appadmin.fecshoptest.com 访问后台web






























