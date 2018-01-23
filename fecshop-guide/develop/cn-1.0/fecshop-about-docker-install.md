Fecshop Docker(把docker当成虚拟机)安装
=================

> 通过docker镜像的方式快速部署fecshop，本部分是把docker当虚拟机用，也就是
> 在linux上面搞一个docker，然后所有的东西都在这个docker里面。
> 然后通过ssh直接连接docker虚拟机。

### 不建议提示

这种方式是不推荐的方式，违背了docker的哲学思想，**强烈建议**按照下面的文档安装：
https://github.com/fecshop/yii2_fecshop_docker

不过，下面这种方式，因为是虚拟机的方式，新手入手操作会比较简单一些。

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

> 镜像2G左右，阿里云地址：https://dev.aliyun.com/detail.html?spm=5176.1972343.2.2.usuXdL&repoId=110333

```
docker pull registry.cn-hangzhou.aliyuncs.com/fecshopsoft/fecshop:3.0.3.1
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
docker run -d -p 2222:22 -p 80:80 registry.cn-hangzhou.aliyuncs.com/fecshopsoft/fecshop:3.0.3.1 /usr/sbin/sshd -D
```

注意，创建启动容器命令使用一次后，不要重复使用，如果重复使用，将会创建多个容器


3.查看容器

```
docker ps         // 查看运行中的容器
docker ps -a      // 查看所有容器
```


4.通过宿主机，进入第2步启动的docker容器虚拟机

通过 `docker ps -a` 查看容器的id（CONTAINER ID），然后通过命令

```
docker exec -it 42d099e3fdca(这个替换成容器id) /bin/bash
```

执行后，就进入了docker容器里面的虚拟机.

`exit` 退出。


5.ssh 直接连接 docker容器虚拟机

> 注意，宿主机的2222和80端口要开放,对于阿里云的端口开放，可以参看：[阿里云 ECS主机开启端口](http://www.fecshop.com/topic/594)

使用xshell连接docker容器虚拟机

```
IP：宿主机的ip
端口：2222
root
fecshop123
```

连接成功后，启动里面的nginx php  mysql 等等

```
/www/start.sh
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
访问： my.fecshop.com
账户密码为上面mysql的账户密码
```



7.设置，访问,以及文件架构

7.1设置host映射（如果您有域名，并做接解析，那么这个步骤不需要做）
打开C:\Windows\System32\drivers\etc\hosts，添加如下代码（将 127.0.0.1 替换成宿主主机的IP（注意这里不是docker容器虚拟机的IP）。）：

```
127.0.0.1       my.fecshop.com       # mysql的phpmyadmin的域名指向
127.0.0.1       appadmin.fecshop.com # 后台域名指向
127.0.0.1       appfront.fecshop.com # 前台pc端域名指向
127.0.0.1       appfront.fecshop.es  # 前台pc端 es 语言的域名指向
127.0.0.1       apphtml5.fecshop.com # 前台html端的域名指向
127.0.0.1       apphtml5.fecshop.es # 前台html端的域名指向
127.0.0.1       appapi.fecshop.com   # api端的域名指向
127.0.0.1       appserver.fecshop.com # server端的域名指向
127.0.0.1       img.fecshop.com        #appimage/common   图片的域名指向
127.0.0.1       img2.fecshop.com    #appimage/appadmin 图片的域名指向
127.0.0.1       img3.fecshop.com    #appimage/appfront 图片的域名指向
127.0.0.1       img4.fecshop.com    #appimage/apphtml5 图片的域名指向
127.0.0.1       img5.fecshop.com    #appimage/appserver图片的域名指向
127.0.0.1       vue.fecshop.com     #VUE端的地址
```

7.3、fecshop的根目录为：`/www/web/online/fecshop-1.3.0.3`

7.4、phpmyadmin的根目录：`/www/web/online/phpmyadmin`

7.5、php的安装目录 `/usr/local/php` , 配置文件：`/etc/php.ini`

7.6、mysql的安装目录:`/usr/local/mysql`, 配置文件：`/usr/local/mysql/my.cnf`

7.7、nginx的安装目录 /usr/local/nginx`, 配置文件为：`/usr/local/nginx/conf`

7.8、mongodb是通过yum安装的方式，参看：[mongodb安装](http://www.fancyecommerce.com/2016/05/03/yii2-mongodb%E7%9A%84%E5%AE%89%E8%A3%85%E5%92%8C%E9%85%8D%E7%BD%AE-mongo/),
 配置文件：`/etc/mongod.conf`

7.9、vue部分的路径

vue的线上发布路径：`/www/web/online/vue_fecshop_appserver/dist` ,nginx域名指向的是该路径

vue的开发文件路径为：`/www/web/online/vue_fecshop_appserver/src`


7.10访问即可,访问上面的域名


8.自定义

> 默认的账户都不安全，您需要设置成自己的账户信息

8.1更改docker容器虚拟机的root密码

通过上面第五步进入docker主机，然后执行 `password root`, 更改密码即可

8.2更改mysql的密码

进入mysql修改密码，修改完成后，在 `@common/config/main-local.php` 处修改mysql的配置密码


8.5、redis

> 【不需要更改设置】镜像中的redis是安全的，不需要进行设置，因为进行了ip绑定，只允许127.0.0.1访问，

如果您进行其他的改动，请注意下面几点：

8.5.1、设置默认绑定的ip，其他ip不允许访问redis，增强安全

8.5.2、端口是6379，这个端口不要开放（如果只有本机访问redis）

8.5.3、设置redis访问密码

如果您进行了redis的修改，那么，您需要去`common/config/main-local.php`中进行配置
更多redis的信息参看：[yii2 – redis 配置](http://www.fancyecommerce.com/2016/05/03/yii2-redis-%E9%85%8D%E7%BD%AE/)


8.5、mongodb

> 【不需要更改设置】镜像中mongodb默认也是安全的配置，允许访问的ip为127.0.0.1，其他ip不允许,因此不需要改动

你可以使用 `RoboMongo` GUI工具连接mongodb，[下载地址](https://robomongo.org/download)
, 因为mongodb默认设置无密码，只允许127.0.0.1登录，
因此，可以使用`RoboMongo`的ssh方式登录，填写您的主机的ssh信息即可登录。


8.6、更改域名

> 您需要更改为您自己的域名，那么，您需要进行几处的更改：

8.6.1、更改 appfront/config/fecshop_local_services/Store.php 更改域名，文档参考（第7部分）：
[配置文档](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-about-config.html)

8.6.2、更改 apphtml5/config/fecshop_local_services/Store.php 更改域名，文档参考（第7部分）：
[配置文档](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-about-config.html)

8.6.3、更改 appserver/config/fecshop_local_services/Store.php 更改域名，文档参考（第7部分）：
[配置文档](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-about-config.html)


8.6.4、更改 common/config/fecshop_local_services/Image.php 更改图片域名，文档参考（第8部分）：
[配置文档](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-about-config.html)



8.6.5更改vue端，后端支持的api配置

> 进入文件夹：/www/web/online/vue_fecshop_appserver/

`config/dev.env.js`: 开发环境设置，将 API_ROOT 改成您的appserver端对应的域名，
WEBSITE_ROOT 改成您的vue端访问的域名。

`config/prod.env.js`:线上环境设置，将 API_ROOT 改成您的appserver端对应的域名，
WEBSITE_ROOT 改成您的vue端访问的域名。

`src/config/store.js`:这里设置vue端的多语言store，
将`domain`改成您的vue端访问的域名，并设置相应的语言，
您还可以在这里添加其他的域名，设置默认访问的语言


vue设置完成后，您需要重新编译一下：`npm run build`







### 其他：（不需要操作）

1.通过容器生成镜像
docker commit -m "fecshop docker" -a "terry" e33e7292f603  alifechop:3.0.3.1

2.将镜像 打包导出为 本地tar文件
docker save -o fecshop_3.03.tar fecshop:3.03

3.将本地tar文件 导入到docker仓库，成为一个镜像
docker load --input fecshop_3.03.tar

4.通过镜像生成容器
docker run -d -p 2222:22 -p 80:80 alifechop:3.0.3.1 /usr/sbin/sshd -D

5.停止启动容器
docker stop  容器id 

docker start 容器id


### 阿里云docker

阿里云docker地址：https://dev.aliyun.com/search.html登录阿里云docker registry:
docker login --username=hi35488735@aliyun.com registry.cn-hangzhou.aliyuncs.com

从registry中拉取镜像：
docker pull registry.cn-hangzhou.aliyuncs.com/fecshopsoft/fecshop

将镜像推送到registry：
docker tag [ImageId] registry.cn-hangzhou.aliyuncs.com/fecshopsoft/fecshop:[镜像版本号]
docker push  registry.cn-hangzhou.aliyuncs.com/fecshopsoft/fecshop

https://dev.aliyun.com/detail.html?spm=5176.1972343.2.2.usuXdL&repoId=110333

### docker  hub

docker login --username=xxxx

在DockerHub上创建账号：https://hub.docker.com/
这里我的账号是firewarm
本地下载镜像（这里拿alpine做示例）,并为镜像打tag

```
[root@host-30 ~]# docker pull alpine:3.4
[root@host-30 ~]# docker tag alpine:3.4 firewarm/alpine:3.4
```

登录到DockerHub上

```
[root@host-30 ~]# docker login
# 输入用户名和密码 
fecshop
```

push镜像到DockerHub上

```
[root@host-30 ~]# docker push firewarm/alpine:3.4
The push refers to a repository [docker.io/firewarm/alpine]
4fe15f8d0ae6: Pushed 
3.4: digest: sha256:dc89ce8401da81f24f7ba3f0ab2914ed9013608bdba0b7e7e5d964817067dc06 size: 528
```

https://hub.docker.com/r/fecshop/fecshop/tags/

