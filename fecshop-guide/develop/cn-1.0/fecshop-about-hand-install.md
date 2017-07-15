Fecshop 全手动安装
==================

> 本文是在linux下面部署开发环境， 
> 是纯净linux一步一步的配置fecshop的整个环境，
> 整个过程比较繁琐，如果您想快速部署，可以使用vagrant进行快速部署，我已经打包好
> vagrant box,您直接加载过来就可以.
>
> 详细参看[Fecshop vagrant安装](fecshop-about-vagrantinstall.md)


linux作为开发环境
-----------------

在linux下面做开发环境，你可能很不习惯，你可以用编辑器的ftp的远程功能
加载linux的文件，开发起来和本地win没有太多的不同（会有一些文件权限和svn提交代码
需要使用命令行的不同），这是我整理的一篇详细博文：
[Linux 作为开发环境的方法分享](http://www.fancyecommerce.com/2016/08/30/linux-%E4%BD%9C%E4%B8%BA%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E7%9A%84%E6%96%B9%E6%B3%95%E5%88%86%E4%BA%AB/)
Linux作为开发环境，线上线下同样的配置，会省略去很多线下程序运行正常，线上出问题的烦恼。
用vagrant在win下面虚拟linux环境的博文：[vagrant 下载部署linux环境](http://www.fancyecommerce.com/2016/09/22/vagrant-%E4%B8%8B%E8%BD%BD%E9%83%A8%E7%BD%B2linux%E7%8E%AF%E5%A2%83/)

当然最省劲的安装， 还是您加载我打包好的vagrant box，直接加载过来即可，详情参看：
[Fecshop vagrant安装](fecshop-about-vagrantinstall.md)，下面是最原始的安装方式，全手动
，如果您是一个喜欢琢磨研究，可以按照下面的步骤尝试一遍。

环境配置部分：
-----------

**一定要按照下面的步骤按照**

**一定要按照下面的步骤按照**

**一定要按照下面的步骤按照**

**重要的事情说三遍**

**如果不按照下面的步骤安装出现问题，请不要
去论坛发帖求助，浪费大家时间。**

如果您对linux不熟悉，感觉障碍很大，可以参看**录制好的视频：**
[Fecshop 安装视频](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_video_install.html)
，里面讲解是的搭建Linux虚拟机，配置linux环境，已经安装配置fecshop等内容。

下面是文档讲述如何搭配环境以及安装fecshop：

1、Linux环境配置：

需要安装mongodb php mysq等等，详情参看文章：
[Fecshop 环境部署 以及 安装步骤](http://www.fancyecommerce.com/2017/03/06/%E7%8E%AF%E5%A2%83%E9%83%A8%E7%BD%B2/)

**注意**：redis版本一定要高，2.2.7一下的版本是不行的，不支持php-redis，建议安装2.8+的版本。


2、安装 

2.1 通过composer的方式安装，如果因为墙无法使用composer，可以按照2.2方式安装

** 可能浏览器存在缓存，导致内容不是最新内容，因此，可以频繁多次刷新下页面，让其不读取浏览器缓存，而是读取最新的内容**

安装这个扩展的首选方式是通过 [composer](http://getcomposer.org/download/).

安装composer

```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
composer self-update
```


安装fecshop app advanced

```
composer global require "fxp/composer-asset-plugin:^1.3.1"
composer create-project fancyecommerce/fecshop-app-advanced  fecshop 1.0.3.5
cd fecshop
composer update    
./init
```

如果报错：jquery.inputmask包找不到，可以参看这里的解决：http://www.fecshop.com/topic/58

注意：一定要执行`composer update` ，不少朋友没有执行，导致版本太低，报错。

如果上面安装很慢，那么您可以使用[composer 中国镜像](https://pkg.phpcomposer.com/)

具体的使用方法可以参看我整理的文档：[composer 默认地址改为中国镜像地址，以及中国镜像地址还原成默认地址](http://www.fancyecommerce.com/2017/04/19/composer-%E9%BB%98%E8%AE%A4%E5%9C%B0%E5%9D%80%E6%94%B9%E4%B8%BA%E4%B8%AD%E5%9B%BD%E9%95%9C%E5%83%8F%E5%9C%B0%E5%9D%80%EF%BC%8C%E4%BB%A5%E5%8F%8A%E4%B8%AD%E5%9B%BD%E9%95%9C%E5%83%8F%E5%9C%B0%E5%9D%80/)

2.2 百度云盘下载完整包

由于composer网速实在不友好，因此，我打包了一份放到了百度云盘，
点击这里进入下载地址为：[fecshop.1.0.3.3.zip](http://pan.baidu.com/s/1b63eXo#list/path=%2Ftools)
需要注意的是，上面的环境中需要的php的扩展都要安装。
这里仅供测试安装使用，如果想升级，还是得使用前面第一部的
composer安装，阿里云主机是可以composer安装的。



执行完上面，就安装完成了。你可以点击这里进行下一步，
[Fecshop 初始配置](fecshop-about-config.md)


