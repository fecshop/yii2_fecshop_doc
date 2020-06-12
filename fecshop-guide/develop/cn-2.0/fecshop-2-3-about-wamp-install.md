Fecmall-2.x WAMP环境安装 - 手把手系列
================

> Windows下面，使用WAMP环境本地安装fecshop教程，相信有经验的程序员看一下linux
下安装fecmall，就可以在wamp下面，安装，下面的安装教程是给小白用的，
比较详细，配图比较多。


**有一些截图太大，如果看起来不够清晰，可以放大浏览器查看截图**

**手把手再WAMP上面配置fecmall，满足小白用户的win环境安装**

下载WAMP
--------------

### 1.下载

1.1官网下载
wamp官网：http://www.wampserver.com/en/#download-wrapper

下载地址：https://sourceforge.net/projects/wampserver/files/

1.2Fecmall Q群下载


Q群文件中可以看到：wampserver3.1.9_x64.exe
，这个是win64位使用的安装程序，安装即可

### 2.安装

我的安装路径是：`D:\wamp64`

安装完成后，启动`wamp`，启动成功后，`右下角`图标为`绿色`，不是绿色可以`重启`（restart all services）试试

![](images/qq0.png)

打开浏览器访问：http://127.0.0.1/ ， 出来wamp就代表安装，并启动wamp成功了

![](images/qq2.png)

配置域名指向
----------

### 1.打开win host文件

C:\Windows\System32\drivers\etc\hosts

将下面的添加到hosts文件中


```
127.0.0.1 appfront.fecshoptest.com
127.0.0.1 appadmin.fecshoptest.com
127.0.0.1 img.fecshoptest.com
127.0.0.1 apphtml5.fecshoptest.com
127.0.0.1 appserver.fecshoptest.com
127.0.0.1 appapi.fecshoptest.com
```

添加完成后截图

![](images/qq1.png)


下载fecmall文件
-----------------

### 一.推荐使用composer安装

1.下载composer： https://getcomposer.org/download/

![](images/qq4.png)

鼠标左键点击右下角的wamp图标，可以看到当前启动的php的版本`7.2.18`

![](images/qq60.png)

安装composer，需要选择相应的`php`(**注意，这个一定要和wamp默认启动的php版本一致，否则将会出现
web的php和命令行的php，不是同一个的问题，这个一定要注意**)

![](images/qq6.png)

剩下的都是一路next即可。

安装完成后， window + r ，cmd进入命令行模式

![](images/qq7.png)

2.进入web目录

我的目录是： D:\wamp64\www

![](images/qq8.png)


更改阿里云composer镜像源

```
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
```

执行下载：

> 请将2.1.6 改成最近的fecmall版本，这里查看最新的版本号： https://github.com/fecshop/yii2_fecshop/releases

```
composer create-project fancyecommerce/fecshop-app-advanced  fecshop 2.1.6
```
然后就可以看到文件下载：

![](images/qq9.png)

下载的log日志如下：

![](images/qq10.png)



![](images/qq11.png)


下载完成后，可以看到：D:\wamp64\www\fecshop
，打开这个文件夹，可以看到如下

![](images/qq12.png)

这就代表下载成功了

2.直接下载完整压缩包

2.1百度网盘 下载地址，https://pan.baidu.com/s/1hs1iC2C ， 下载fecshop-2.x.x.zip （请下载最高的版本）

2.2QQ群文件下载，官方Q群文件里面有相应的文件,Fecmall QQ群(新)：782387676，入群验证：fecmall

Fecmall初始化
---------------

### 1.执行fecmall  init

进入fecshop的目录，执行`init.bat`

![](images/qq14.png)


### 2.初始化mysql数据库

鼠标左键点击wamp的右下角图标，如图所示，点击mysql console

![](images/qq16.png)

点击后，弹框内容`root`即可，点击ok，然后出来mysql控制台，直接点回车

![](images/qq17.png)


```
use mysql

update mysql.user set authentication_string=password('123456') where user='root' ;

flush privileges;

```

执行log如图：

![](images/qq18.png)

这样初始化完成了  mysql账户密码为：`root  123456`

打开phpmyadmin

![](images/qq19.png)


浏览器打开后，用创建好的mysql用户名密码登陆，创建数据库 `fecmall`


![](images/qq20.png)

点击创建，成功可以看到fecmall数据库


### 3.配置apache
 
 上面再win hosts中我们添加了指向本地的域名
 

```
127.0.0.1 appfront.fecshoptest.com
127.0.0.1 appadmin.fecshoptest.com
127.0.0.1 img.fecshoptest.com
127.0.0.1 apphtml5.fecshoptest.com
127.0.0.1 appserver.fecshoptest.com
127.0.0.1 appapi.fecshoptest.com
```

下面我们在apache中做配置，打开apache配置文件

![](images/qq31.png)

在这个配置文件后面追加如下的内容

> 新版本2.1.6以后的fecmall版本，@app/web/`.htaccess`默认已经添加，用于处理`url中去掉index.php`的问题, 您不需要自己手动添加了


```

<VirtualHost *:80>
  ServerName appadmin.fecshoptest.com
  ServerAlias fecshoptest
  DocumentRoot "${INSTALL_DIR}/www/fecshop/appadmin/web"
  <Directory "${INSTALL_DIR}/www/fecshop/appadmin/web">
    Options +Includes +FollowSymLinks +MultiViews
    AllowOverride All
    Require local
  </Directory>
</VirtualHost>


<VirtualHost *:80>
  ServerName appfront.fecshoptest.com
  ServerAlias fecshoptest
  DocumentRoot "${INSTALL_DIR}/www/fecshop/appfront/web"
  <Directory "${INSTALL_DIR}/www/fecshop/appfront/web">
    Options +Includes +FollowSymLinks +MultiViews
    AllowOverride All
    Require local
  </Directory>
</VirtualHost>


<VirtualHost *:80>
  ServerName apphtml5.fecshoptest.com
  ServerAlias fecshoptest
  DocumentRoot "${INSTALL_DIR}/www/fecshop/apphtml5/web"
  <Directory "${INSTALL_DIR}/www/fecshop/apphtml5/web">
    Options +Includes +FollowSymLinks +MultiViews
    AllowOverride All
    Require local
  </Directory>
</VirtualHost>

<VirtualHost *:80>
  ServerName img.fecshoptest.com
  ServerAlias fecshoptest
  DocumentRoot "${INSTALL_DIR}/www/fecshop/appimage/common"
  <Directory "${INSTALL_DIR}/www/fecshop/appimage/common">
    Options +Includes +FollowSymLinks +MultiViews
    AllowOverride All
    Require local
  </Directory>
</VirtualHost>

<VirtualHost *:80>
  ServerName appserver.fecshoptest.com
  ServerAlias fecshoptest
  DocumentRoot "${INSTALL_DIR}/www/fecshop/appserver/web"
  <Directory "${INSTALL_DIR}/www/fecshop/appserver/web">
    Options +Includes +FollowSymLinks +MultiViews
    AllowOverride All
    Require local
  </Directory>
</VirtualHost>


<VirtualHost *:80>
  ServerName appapi.fecshoptest.com
  ServerAlias fecshoptest
  DocumentRoot "${INSTALL_DIR}/www/fecshop/appapi/web"
  <Directory "${INSTALL_DIR}/www/fecshop/appapi/web">
    Options +Includes +FollowSymLinks +MultiViews
    AllowOverride All
    Require local
  </Directory>
</VirtualHost>
```

保存apche配置文件，然后重启apache

![](images/qq32.png)








### Fecmall界面安装


准备好这些后，就可以通过web浏览器界面安装fecmall了，http://bt.appfront.fecshop.com/install` （换成您自己的域名）

界面安装配置详细参看：[Fecmall-2.x 界面安装](fecshop-2-graphical-web-install.md)

 
 