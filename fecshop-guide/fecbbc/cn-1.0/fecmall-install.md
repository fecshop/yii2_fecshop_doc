FecMall 多商户安装教程
========

> 安装Fecmall多商户系统的教程


### 安装

1.安装fecmall开源商城

fecmall多商户系统，是在fecmall开源商城系统进行的扩展系统，
是独立包的形式开发，因此，需要先安装fecmall


fecmall安装教程：[Fecmall-2.x安装教程](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecshop-2-graphical-install.html)

2.应用市场注册账户，购买fecmall多商户系统

购买地址：http://addons.fecmall.com/42575492

3.购买完成后，登陆fecmall后台， 应用中心--> 应用管理 --> 应用市场

点击在线安装`fecbbc 多商户电商系统`

4.安装完成后，需要nginx 添加一下经销商后台的访问域名

也将域名对应文件路径`@appbdmin/web`（@appadmin/web是平台后台地址）

`nginx`或`apache`的配置，和`appadmin`入口类似的配置，这里不做阐述

经销商后台默认登陆账户：  `fecshop`   `fecshop123`

登陆后，您会发现没有产品，您需要登陆平台商后台，进入产品管理，给产品添加经销商，添加后，就会
看到产品。

您可以登陆平台后台，添加新的经销商，添加后，在经销商后台即可登陆该账户，并发布产品等。


### 配置

1.Store配置


1.1网站配置-->Appfront配置--> Store配置

打开cn和us的store编辑，将`第三方模板路径`值设置为：`@fecbbc/app/appfront/theme/fecbbc`

1.2网站配置-->Apphtml5配置--> Store配置

打开cn和us的store编辑，将`第三方模板路径`值设置为：`@fecbbc/app/apphtml5/theme/fecbbc`

2.参数配置


在这里配置页面顶部的搜索词，以及首页各个板块的sku（在下面截图的右侧有注释）

![](images/bb1.png)

您可以按照下面的内容先填写上去,安装完成后，根据自己的需要更改

`Hot Search`: `卫衣,牛仔裤,运动鞋,椰子,nike,欧文`

`Hot Product Skus`：`testest,p10001-kahaki-xxl-t4,222212,22221,p10001-kahaki-xxl,p10001-black-m,op0002-33,men0003,men0001,sk0002,sk0003,sk0008`

`Chaoliu Top Sku1`：`sk10004-001,sk10003-001,sk10002-002,sk10002,sk1000-blue,sk2001-blue-zo`

`Chaoliu Top Sku2`：`men0003,men0001,sk0002,sk0003,sk0008`

`Chaoliu Bottom Skus1`：`sk10004-001,sk10003-001,sk10002-002,sk10002,sk1000-blue,sk2001-blue-zo`

`Chaoliu Bottom Skus2`：`men0003,men0001,sk0002,sk0003,sk0008`

`New Product Skus`：`testest,p10001-kahaki-xxl-t4,222212,22221,p10001-kahaki-xxl,p10001-black-m,op0002-33,men0003,men0001,sk0002,sk0003,sk0008,sk0002,sk0003,sk0008,sk1000-blue,sk0004,sk1000-khak`

`KuaiDiNiaoBusinessId`: 用于物流查询的api，可以去快递鸟官方注册，免费的查询有限制，官网地址：http://www.kdniao.com/

`KuaiDiNiaoAppKey`：用于物流查询的快递鸟api信息

`OrderAutoReveiveMaxDay`：订单发货后，X天后，脚本自动改成已收货


2.首页的板块配置

fecbbc-1.9.3版本+, 在安装fecyo的时候，直接进行初始化。

您可以在后台`cms`-->`static block(静态块)` 里面查看这些`静态块`





3.产品配置（测试产品）

3.1 添加经销商账户

因为测试数据是fecmall开源商城的，产品部分并没有供销商数据（产品从属于那个经销商），
因此需要您在后台设置一下经销商（可以添加经销商）

安装fecmall多商户，经销商默认只有fecshop一个账户，您可以在后台继续添加经销商账户

后台：供应商管理  -> 供应商管理

添加经销商账户，成功后，就可以去经销商后台登陆了



3.2淘宝模式产品数据初始化

fecmall安装后，默认是fecmall的产品测试数据，由于fecbbc多商户添加了淘宝模式产品，需要对这些历史数据进行初始化数据处理，
因此您需要执行一下初始化脚本

> 如果您不想处理这些数据，您可以进入数据库，将`product_flat`表的产品数据清掉,`product_flat_qty`产品库存表数据清掉，
产品分类关系表`category_product`清掉，然后后台新建淘宝模式产品即可


```
cd addons/fecmall/fecbbc/shell
sh initTbProduct.sh
```

执行完后，可以在后台，产品管理部分，看到产品数据
 

 3.3为产品设置经销商,


您可以在平台后台，产品管理部分，编辑产品，为产品设置经销商


如果产品没有设置经销商，用户将不能将产品加入购物车。


4.设置阿里云短信，微信登陆，微信H5页面分享等


此部分是集成的fecphone扩展，详细设置参看：http://www.fecmall.com/doc/fecshop-guide/addons/cn-2.0/guide-fecmall-addons-phone-account.html

5.其他设置

5.1产品详情开启面包屑导航

平台后台：网站配置--> Appfront配置  --> 分类产品配置

设置  `产品页面-显示面包屑导航`：`yes`




到这里基本就配置完成了，其他的基本是fecmall开源商城部分的配置，这里就不阐述了。















