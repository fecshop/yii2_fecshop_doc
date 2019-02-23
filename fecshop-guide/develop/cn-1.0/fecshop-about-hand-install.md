Fecshop 安装
==================

> 注意：fecshop的安装，是不能从github clone下载安装的，需要按照下面的文档进行安装
> ，下面有三种安装方式，推荐使用docker compose方式快速部署，如果您对Yii2部署比较熟悉，
> 可以采用第3种标准部署方式安装fecshop，下面的操作过程中，请严格按照文档步骤操作


### Docker Compose 方式安装Fecshop

> 由于fecshop安装，需要的软件比较多，
强烈建议新手时候docker部署fecshop，
简单快捷，多学习新知识，这些都是日后调薪换工作的资本。

**强烈建议使用docker部署fecshop，方便快捷！**

**强烈建议使用docker部署fecshop，方便快捷！**


新手安装fecshop，建议使用docker安装，
非常的简单快捷，地址为：
https://github.com/fecshop/yii2_fecshop_docker
，推荐使用这种方式快速部署Fecshop。

### Vagrant Box 方式安装Fecshop

vagrant box的方式（不建议）：2017.6月做的box，以后**不再维护vagrant box**，
推荐使用docker compose安装，如果您想使用vagrant box可以参看：
[Fecshop vagrant安装](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-about-vagrantinstall.html)



### 标准安装方式：Linux 环境安装Fecshop

> 建议使用docker的方式快速安装部署，
标准安装是从裸机centos一步一步的搭建起来的，
过程繁琐，建议新手用docker搭建，docker安装fecshop的
文档非常的详细。

参考资料：

1.[Linux 作为开发环境的方法分享](http://www.fancyecommerce.com/2016/08/30/linux-%E4%BD%9C%E4%B8%BA%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E7%9A%84%E6%96%B9%E6%B3%95%E5%88%86%E4%BA%AB/)

2.[vagrant 下载部署linux环境(虚拟机)](http://www.fancyecommerce.com/2016/09/22/vagrant-%E4%B8%8B%E8%BD%BD%E9%83%A8%E7%BD%B2linux%E7%8E%AF%E5%A2%83/)

3.[vagrant 设置文件映射，将windows文件夹映射到linux中](http://www.fancyecommerce.com/2017/06/06/vagrant-%E8%AE%BE%E7%BD%AE%E6%96%87%E4%BB%B6%E6%98%A0%E5%B0%84%EF%BC%8C%E5%B0%86windows%E6%96%87%E4%BB%B6%E5%A4%B9%E6%98%A0%E5%B0%84%E5%88%B0linux%E4%B8%AD/)


> Linux 下面安装Fecshop，非常的详细，是完全从裸机Linux操作系统
> 一步一步的搭建环境的过程，而且安装php mysql等都是采用的编译方式，在学习fecshop的同时，可以提升您的linux部署环境的能力，
> 如果您对linux不熟悉，感觉障碍很大，可以参看**录制好的视频：**
> [Fecshop 安装视频](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_video_install.html)
> ，里面讲解是的搭建Linux虚拟机，配置linux环境，已经安装配置fecshop等内容，


** 一定要按照下面的步骤按照，如果按照下面的步骤安装出现问题，请到[www.fecshop.com](http://www.fecshop.com)
发帖，形成积累，方便更多的后来人。（帖子100%回复，QQ群的问题不回复） **


如果有Yii2基础，安装起来还是比较容易，如果没有Yii2基础，会比较费劲一些，
建议参看视频安装，视频和下面的文档
内容是同步的，下面是文档讲述如何搭配环境以及安装fecshop：

### 1、Linux环境配置：

需要安装mongodb php mysq等等，详情参看文章：
[Fecshop 环境部署 以及 安装步骤](http://www.fancyecommerce.com/2017/03/06/%E7%8E%AF%E5%A2%83%E9%83%A8%E7%BD%B2/)

**注意**：

1.redis版本一定要高，2.2.7一下的版本是不行的，不支持php-redis，建议安装2.8+的版本。

2.mongodb建议3+

3.php 7+ (因为有部分扩展不支持php5，因此，直接上php7了，您直接安装php7吧，性能比php5快一倍)

4.mysql，建议5.6+

### 2、安装 

安装有2种方式，建议使用`2.2 通过composer的方式安装`，
如果网络不行，可以使用 `2.1通过百度网盘安装 `

2.1 通过百度网盘安装(**不建议**)，

如果因为墙无法使用composer，可以访问百度云盘，下载地址为：http://pan.baidu.com/s/1hs1iC2C
**下载日期最新**的压缩包即可，下载完成后，解压，然后进入fecshop，执行init命令，详细如下：

```
cd fecshop   
./init
```

> 百度云盘下载，不经过composer安装，不会检测环境，因此，上面的环境中需要的php的扩展都要安装。
> 如果想升级，还是得使用composer 来升级
> composer安装，阿里云主机是可以composer安装的。
> 因此，第一次图省劲可以用百度网盘的方式下载安装，熟练后，还是需要用composer安装，
> 这样以后升级方便。

2.2 通过composer的方式安装

安装这个扩展的首选方式是通过 [composer](http://getcomposer.org/download/).

安装composer

```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
composer self-update
```


composer 安装fecshop app advanced

```
composer global require "fxp/composer-asset-plugin:^1.4.4"
composer create-project fancyecommerce/fecshop-app-advanced  fecshop 1.7.0.0
cd fecshop
composer update    
./init
```


在上面composer安装过程中，会出现填写github的token

```
Token (hidden):
```

需要去github获取token，具体步骤参考：[Fecshop 安装，获取github授权码](http://www.fecshop.com/topic/412)

如果报错：jquery.inputmask包找不到，可以参看这里的解决：http://www.fecshop.com/topic/58

如果报错：`no valid bower.json was found in any branch or tag of https://github.com/jquery/jquery-dist.git, could not load a package from it`,
这个是您的网络不行，中国镜像对bower部分是不能代理的，您需要开启一下vpn。
对于阿里云主机，是没有问题的，在本地可能会出这个问题，群里面有几个朋友遇到过。

如果上面安装很慢，那么您可以使用[composer 中国镜像](https://pkg.phpcomposer.com/)

具体的使用方法可以参看我整理的文档：[composer 默认地址改为中国镜像地址，以及中国镜像地址还原成默认地址](http://www.fancyecommerce.com/2017/04/19/composer-%E9%BB%98%E8%AE%A4%E5%9C%B0%E5%9D%80%E6%94%B9%E4%B8%BA%E4%B8%AD%E5%9B%BD%E9%95%9C%E5%83%8F%E5%9C%B0%E5%9D%80%EF%BC%8C%E4%BB%A5%E5%8F%8A%E4%B8%AD%E5%9B%BD%E9%95%9C%E5%83%8F%E5%9C%B0%E5%9D%80/)



### 3. 配置

执行完上面，就安装完成了。你可以点击这里进行下一步，
[Fecshop 初始配置](fecshop-about-config.md)，
** 注意，配置过程一定要仔细的操作 **。



### 其他 - 对于windows 环境安装Fecshop

> fecshop是基于php Yii2框架开发，对于windows下面安装，是可以的，
> 但是Terry对windows下面部署不是很熟悉，
> 因此只有linux安装fecshop的教程，不过，幸运的是，有热心fecshoper整理了在windows
> 下面安装fecshop的帖子，您看参看帖子地址：（如果您要用window安装fecshop，您也需要查看下面Linux的步骤，只是某些软件和配置参考下面的帖子）
> 
> [windows - WAMP 下安装Fecshop](http://www.fecshop.com/topic/402)
> 
> [windows - PHPStudy下安装Fecshop](http://www.fecshop.com/topic/527)
> 
> 在安装过程中存在问题，您可以在帖子评论区留言咨询。


