Fecshop Docker安装
=================

> 通过docker镜像的方式快速部署fecshop

### 镜像信息

```
操作系统：centos6.9
php：7.1.13
nginx：nginx-1.11.13
mysql: 5.6.14
redis: redis-3.2.9
mongodb: 3.6
xunsearch: laest
nodejs v5.12.0
npm  3.8.6
cnpm laest
```

### 安装docker

1.操作系统版本要求,Linux 操作系统，linux内核需要大于3.10，查看的方法：

> 在window下面也可以安装docker，但我不熟悉，因此不做陈述，这里说的是在centos7下面部署的过程

```
[root@42d099e3fdca ~]# uname -r
3.10.0-229.el7.x86_64
[root@42d099e3fdca ~]#
```

`centos7` 默认就支持，centos6需要升级linux内核，对于阿里云等云主机，是无法升级内核的，独立主机是可以的， 依次建议直接用centos7

2.docker 安装

```
sudo curl -sSL https://get.daocloud.io/docker | sh
```

3.docker 启动

```
// 启动docker
service docker start

// 开机启动
chkconfig docker on
```

经过了这些步骤，我们就把docker部署好了

### 安装Fecshop 镜像

1.下载镜像，并载入

在百度云盘中下载fecshop docker 镜像，载入docker仓库

```
docker	load	--input	fecshop_3.03.tar
```

其他：您也可以把仓库中的镜像保存成本地文件（这个不需要操作）

```
docker	save	-o	fecshop_3.03.tar	fecshop:3.03

```


2.查看镜像，创建启动容器

> 关于镜像和容器的更多操作命令参看：
[docker 常用命令](http://www.fecshop.com/topic/591)

查看镜像

```
docker images
```


创建启动容器

```
docker run -d -p 2222:22 -p 80:80 fecshop:3.03 /www/start.sh
```

注意，创建启动容器命令使用一次后，不要重复使用，如果重复使用，将会创建多个容器


3.查看容器

```
docker ps         // 查看运行中的容器
docker ps -a      // 查看所有容器
```


4.进入第2步启动的容器

通过 `docker ps -a` 查看容器的id，然后通过命令

```
docker exec -it 42d099e3fdca(这个替换成容器id) /bin/bash
```

执行后，就进入了docker容器里面的虚拟机。


5.ssh 直接连接 docker容器虚拟机

```
IP：宿主机的ip
端口：2222
root
fecshop123
```

您可以直接用notepad的远程加载文件功能，通过sftp连接，
加载文件结构树，详细参看：
[Linux 作为开发环境的方法分享](http://www.fancyecommerce.com/2016/08/30/linux-%E4%BD%9C%E4%B8%BA%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E7%9A%84%E6%96%B9%E6%B3%95%E5%88%86%E4%BA%AB/)


当然，您可以可以直接用vim编辑，或者您有更好的办法，编辑docker容器虚拟机
的文件。

6.镜像里面安装的软件以及fecshop的资料


```
mysql
root
drdf32SDFDAsse33r33F2sfdsa3Y
```


```
phpMyAdmin
访问： my.fecshoptest.com
账户密码为上面mysql的账户密码
```


```
RockMongo
访问：rock.fecshoptest.com
admin
fecshop123
```

7.设置，访问,以及文件架构

7.1设置host映射
打开C:\Windows\System32\drivers\etc\hosts，添加如下代码（将 127.0.0.1 替换成宿主主机的IP（注意这里不是docker容器虚拟机的IP）。）：


127.0.0.1       my.fecshoptest.com       # mysql的phpmyadmin的域名指向
127.0.0.1       appadmin.fecshoptest.com # 后台域名指向
127.0.0.1       appfront.fecshoptest.com # 前台pc端域名指向
127.0.0.1       appfront.fecshoptest.es  # 前台pc端 es 语言的域名指向
127.0.0.1       apphtml5.fecshoptest.com # 前台html端的域名指向
127.0.0.1       apphtml5.fecshoptest.es # 前台html端的域名指向
127.0.0.1       appapi.fecshoptest.com   # api端的域名指向
127.0.0.1       appserver.fecshoptest.com # server端的域名指向
127.0.0.1       img.fecshoptest.com        #appimage/common   图片的域名指向
127.0.0.1       img2.fecshoptest.com    #appimage/appadmin 图片的域名指向
127.0.0.1       img3.fecshoptest.com    #appimage/appfront 图片的域名指向
127.0.0.1       img4.fecshoptest.com    #appimage/apphtml5 图片的域名指向
127.0.0.1       img5.fecshoptest.com    #appimage/appserver图片的域名指向
127.0.0.1       vue.fecshoptest.com     #VUE端的地址


7.3fecshop的根目录为：`/www/web/online/fecshop-1.3.0.3`

7.4phpmyadmin的根目录：`/www/web/online/phpmyadmin`

7.5php的安装目录 `/usr/local/php` , 配置文件：`/etc/php.ini`

7.6mysql的安装目录:`/usr/local/mysql`, 配置文件：`/usr/local/mysql/my.cnf`

7.7nginx的安装目录 /usr/local/nginx`, 配置文件为：`/usr/local/nginx/conf`

7.8mongodb是通过yum安装的方式，参看：[mongodb安装](http://www.fancyecommerce.com/2016/05/03/yii2-mongodb%E7%9A%84%E5%AE%89%E8%A3%85%E5%92%8C%E9%85%8D%E7%BD%AE-mongo/),
 配置文件：`/etc/mongod.conf`

7.9vue部分的路径

vue的线上发布路径：`/www/web/online/vue_fecshop_appserver/dist` ,nginx域名指向的是该路径

vue的开发文件路径为：`/www/web/online/vue_fecshop_appserver`


7.10访问即可,访问上面的域名




8.自定义

> 默认的账户都不安全，您需要设置成自己的账户信息

8.1更改docker容器虚拟机的root密码

通过上面第五步进入docker主机，然后执行 `password root`, 更改密码即可

8.2更改mysql的密码

进入mysql修改密码，修改完成后，在 `@common/config/main-local.php` 处修改mysql的配置密码


8.3更改rockmongo的密码【废弃，请使用robomongo连接】

打开文件 /www/web/online/rockmongo/config.php
，将`fecshop123` 更改成您自己的密码。（rockmongodb是一个类似于phpmyadmin的的web在线访问界面）

```
$MONGO["servers"][$i]["control_users"]["admin"] = "fecshop123"
```


8.4redis

> 镜像中的redis是安全的，因为进行了ip绑定，只允许127.0.0.1访问，如果您进行其他的改动
> 请注意下面几点

8.4.1设置默认绑定的ip，其他ip不予许访问redis，增强安全

8.4.2端口是6379，这个端口不要开放（如果只有本机访问redis）

8.4.3设置redis访问密码

如果您进行了redis的修改，那么，您需要去`common/config/main-local.php`中进行配置
更多redis的信息参看：[yii2 – redis 配置](http://www.fancyecommerce.com/2016/05/03/yii2-redis-%E9%85%8D%E7%BD%AE/)


8.5mongodb

镜像中mongodb默认也是安全的配置允许访问的ip为127.0.0.1，其他ip不允许,因此不需要改动

你可以使用 `RoboMongo` GUI工具连接mongodb，[下载地址](https://robomongo.org/download)
, 因为mongodb默认设置无密码，只允许127.0.0.1登录，
因此，可以使用`RoboMongo`的ssh方式登录，填写您的主机的ssh信息即可登录。


8.6更改域名

您需要更改为您自己的域名，那么，您需要进行几处的更改：

8.6.1更改 appfront/config/fecshop_local_services/Store.php 更改域名，文档参考（第7部分）：
[配置文档](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-about-config.html)

8.6.2更改 apphtml5/config/fecshop_local_services/Store.php 更改域名，文档参考（第7部分）：
[配置文档](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-about-config.html)

8.6.3更改 appserver/config/fecshop_local_services/Store.php 更改域名，文档参考（第7部分）：
[配置文档](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-about-config.html)


8.6.4更改 common/config/fecshop_local_services/Image.php 更改图片域名，文档参考（第8部分）：
[配置文档](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-about-config.html)



8.6.5更改vue端，后端支持的api配置

进入文件夹：/www/web/online/vue_fecshop_appserver/

`config/dev.env.js`: 开发环境设置，将 API_ROOT 改成您的appserver端对应的域名，
WEBSITE_ROOT 改成您的vue端访问的域名。

`config/prod.env.js`:线上环境设置，将 API_ROOT 改成您的appserver端对应的域名，
WEBSITE_ROOT 改成您的vue端访问的域名。

`src/config/store.js`:这里设置vue端的多语言store，
将`domain`改成您的vue端访问的域名，并设置相应的语言，
您还可以在这里添加其他的域名，设置默认访问的语言


vue设置完成后，您需要重新编译一下：`npm run build`














