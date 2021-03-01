Fecbbb多商户安装
===========


### 安装


1.您需要先安装fecbbc多商户 [Fecbbc多商户安装](http://www.fecmall.com/doc/fecmall-guide/instructions/cn-1.0/guide-fecmall-install.html)

2.应用市场：http://addons.fecmall.com/81291754 ， 下单绑定

3.进行安装

1.Store配置

1.1网站配置-->Appfront配置--> Store配置

打开cn和us的store编辑，将第三方模板路径值设置为：`@fecbbb/app/appfront/theme,@fecbbc/app/appfront/theme/fecbbc`

1.2网站配置-->Apphtml5配置--> Store配置

打开cn和us的store编辑，将第三方模板路径值设置为：`@fecbbb/app/apphtml5/theme,@fecbbc/app/apphtml5/theme/fecbbc`


2.打开支付

进入后台

2.1支付配置   

支付宝配置：`网站配置` -->`支付参数配置` --> `支付宝支付配置` ,   
 
微信支付配置：`网站配置` -->`支付参数配置` --> `微信支付配置` 


2.2打开线下支付方式

`网站配置` -->`Appfront配置` --> `支付配置` ,   将 `线下付款支付方式`设置为Enable

`网站配置` -->`Apphtml5配置` --> `支付配置` ,   将 `线下付款支付方式`设置为Enable

`网站配置` -->`Appserver配置` --> `支付配置` ,   将 `线下付款支付方式`设置为Enable









