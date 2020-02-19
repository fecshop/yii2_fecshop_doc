FecMallFecbdc 多商户分销安装
================





> 安装Fecmall fecbdc多商户分销系统的教程


### 安装

1.安装fecmall开源商城

fecmall多商户系统，是在fecmall开源商城系统进行的扩展系统，
是独立包的形式开发，因此，需要先安装fecmall


fecmall安装教程：[Fecmall-2.x安装教程](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecshop-2-graphical-install.html)

2.应用市场注册账户，购买fecmall多商户分销系统

2.1Fecbbc多商户系统购买地址：http://addons.fecmall.com/42575492

2.2Fecbdc多商户分销系统购买地址：http://addons.fecmall.com/33239568



因为fecbdc多商户分销系统，是在多商户系统fecbbc基础上扩展的，因此，这两个系统都需要购买

3.安装fecmall fecbbc多商户系统

您可以参看文档：[fecmall fecbbc多商户系统安装文档](http://www.fecmall.com/doc/fecmall-guide/instructions/cn-1.0/guide-fecmall-install.html)

您需要细致看文档，完成多商户部分的安装，安装完成后，需要仔细看一下多商户的各个流程，进行熟悉


4.安装Fecmall Fecbdc多商户分销系统

购买完成后，登陆fecmall后台， 应用中心--> 应用管理 --> 应用市场

点击在线安装`fecbdc 多商户电商系统`


4.1 Appfront设置store，为store添加模板路径

后台Appfront store：`网站配置`--> `appfront配置` --> `store配置`

> 注意：激活的store都需要设置，点击编辑，在编辑框 `第三方模板路径`中填写下面的内容

```
@fecbdc/app/appfront/theme/fecbdc,@fecbbc/app/appfront/theme/fecbbc
```



4.1 Apphtml设置store，为store添加模板路径

后台Apphtml5 store：`网站配置`--> `apphtml5配置` --> `store配置`

> 注意：激活的store都需要设置，点击编辑，在编辑框 `第三方模板路径`中填写下面的内容

```
@fecbdc/app/apphtml5/theme/fecbdc,@fecbbc/app/apphtml5/theme/fecbbc
```





5.设置应用优先级`priority`

登陆平台后台：`应用中心` --> `应用管理` --> `已安装应用`

fecbbc: `priority`  设置为 `1`

fecbdc: `priority` 设置为 `2`




















