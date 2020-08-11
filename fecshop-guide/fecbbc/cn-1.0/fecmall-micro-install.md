FecMall Fecbbc多商户微信小程序安装
===========

> 微信小程序入口

### Fecbbc多商户微信小程序

1.您需要应用市场付费购买

http://addons.fecmall.com/24135818

在线安装，安装完成后，下载zip文件  `./addons/fecmall/fecbbcmicro/fecbbc_wx_micro_program.zip`
，这个就是fecyo的微信小程序完整文件，通过ftp下载下来即可


2.解压zip文件，通过微信开发者工具打开目录

2.1打开`config.js`,将 `'url': 'https://fecbbcserver.fecshop.com',` 改成您自己的域名，这个就是fecmall appserver入口对应的域名，
注意，这里必须是https

2.2project.config.json 将 `"appid": "wxedc77529191bc54f",` 改成您自己的微信小程序的appid


3.fecmall后台配置，以及微信小程序的设置，详细参看文档：http://www.fecmall.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_wx_micro.html


3.搭建完，您就可以参看您的微信小程序了






























