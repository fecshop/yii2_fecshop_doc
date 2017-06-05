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


1、Linux环境配置：

需要安装mongodb php mysq等等，详情参看文章：
[Fecshop 环境部署 以及 安装步骤](http://www.fancyecommerce.com/2017/03/06/%E7%8E%AF%E5%A2%83%E9%83%A8%E7%BD%B2/)

**注意**：redis版本一定要高，2.2.7一下的版本是不行的，不支持php-redis，建议安装2.8+的版本。


2、安装 fecshop app advanced

安装这个扩展的首选方式是通过 [composer](http://getcomposer.org/download/).

安装composer

```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
composer self-update
```


安装fecshop app advanced

```
composer global require "fxp/composer-asset-plugin:^1.2.0"
composer create-project fancyecommerce/fecshop-app-advanced  fecshop 1.0.2.5
cd fecshop
composer update    
./init
```

注意：一定要执行`composer update` ，不少朋友没有执行，导致版本太低，报错。

如果上面安装很慢，那么您可以使用[composer 中国镜像](https://pkg.phpcomposer.com/)

具体的使用方法可以参看我整理的文档：[composer 默认地址改为中国镜像地址，以及中国镜像地址还原成默认地址](http://www.fancyecommerce.com/2017/04/19/composer-%E9%BB%98%E8%AE%A4%E5%9C%B0%E5%9D%80%E6%94%B9%E4%B8%BA%E4%B8%AD%E5%9B%BD%E9%95%9C%E5%83%8F%E5%9C%B0%E5%9D%80%EF%BC%8C%E4%BB%A5%E5%8F%8A%E4%B8%AD%E5%9B%BD%E9%95%9C%E5%83%8F%E5%9C%B0%E5%9D%80/)


执行完上面，就安装完成了。你可以点击这里进行下一步，
[Fecshop 初始配置](fecshop-about-config.md)


