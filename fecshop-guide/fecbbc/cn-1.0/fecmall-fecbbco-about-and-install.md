Fecbbco 跨境多商户介绍和安装
==================

> Fecbbco是基于fecbbc的基础上开发的扩展，用于跨境多商户

### Fecbbco 跨境多商户介绍

Fecbbc多商户是针对国内的多商户系统，对于国内的多商户系统，和跨境有所不同

1.账户体系不同，国内用`手机号`，国外用`email`作为账户体系，因此，账户的`注册`，`登陆`，`密码找回`等功能都有所不同。

2.`语言`和`货币`的不同，跨境为`多语言多货币`

3.`货运地址`不同，跨境需要加入`国家`字段，并且地址的顺序也不同，譬如国内是xx省xx市xx区xxx街道xxx，
而国外的地址顺序为：  `xxx街道xxx市xx省xxx国家`

4.`支付`不同，国内一般用支付宝微信，国外一般用paypal，stripe，等一些支付渠道

5.页面`布局`不同


### Fecbbco扩展安装


1.应用市场地址：http://addons.fecmall.com/92374754

如果安装fecmall应用扩展，详细参看: [Fecmall应用市场安装扩展文档](http://www.fecmall.com/doc/fecshop-guide/addons/cn-2.0/guide-fecmall-addons-install.html)

2.安装完成后，进入后台，`刷新缓存`（后台： `控制面板` -> `缓存管理`）

3.设置store第三方模板路径

进入平台后台，设置模板路径，fecbbco的模板路径写到最左边

3.1`网站配置` -> `appfront配置` ->  `store配置`

将`@fecbbco/app/appfront/theme/fecbbco` 加入到`第三方模板路径`中，譬如：
`@fecbbco/app/appfront/theme/fecbbco,@fecbbc/app/appfront/theme/fecbbc`


3.2`网站配置` -> `apphtml5配置` ->  `store配置`

将`@fecbbco/app/apphtml5/theme/fecbbco` 加入到`第三方模板路径`中，譬如：
`@fecbbco/app/apphtml5/theme/fecbbco,@fecbbc/app/apphtml5/theme/fecbbc`


4.设置扩展优先级

平台后台：`应用中心` -> `应用管理` -> `已安装应用`

将fecbbco的扩展的`优先级`设置最高（数字越大，优先级越高）

保存即可。


补充：该扩展还在进一步开发中。
















