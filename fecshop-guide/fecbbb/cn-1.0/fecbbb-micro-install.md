Fecbbb微信小程序安装
============


> 小程序部分的安装


### 微信小程序安装

1.下载微信小程序zip包

fecbbb扩展安装后，进入文件夹 `./addons/fecmall/fecbbb/`即可看到微信小程序的zip压缩包
:`fecbbb_wx_micro_program.zip`

下载下来解压，就是微信小程序部分的完整文件


2.解压zip文件，通过微信开发者工具打开目录

2.1打开config.js,将 'url': 'https://fecbbcserver.fecshop.com', 改成您自己的域名，这个就是fecmall appserver入口对应的域名， 注意，这里必须是https

2.2project.config.json 将 "appid": "wxedc77529191bc54f", 改成您自己的微信小程序的appid

3.fecmall后台配置，以及微信小程序的设置，详细参看文档：http://www.fecmall.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_wx_micro.html

3.搭建完，您就可以参看您的微信小程序了























