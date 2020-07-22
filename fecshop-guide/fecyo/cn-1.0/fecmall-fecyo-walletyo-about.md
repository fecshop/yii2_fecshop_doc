Walletyo扩展-关于和介绍
================

> walletyo是基于fecyo上面的扩展，扩展的功能：用户钱包，用户积分，分销功能，后续会逐步添加团购，秒杀等功能



### Walletyo扩展介绍

> 目前该扩展支持`pc`, `h5`以及 微信小程序。

fecyo是基于fecmall开源系统开发的中文电商扩展，但fecyo在营销方面弱，需要进行功能强化，
因此，开发了walletyo扩展，您需要先安装fecyo，然后再安装walletyo扩展，walletyo扩展功能列表如下：

1.`用户钱包`：用户在商城的`虚拟钱包`，可以通过购物，`充值`等方式赚取站内余额，也可以进行`提现`等操作

2.`用户积分`：用户在商城的`积分`，用户可以通过购物`赚取积分`，下次下单可以使用积分`抵消`部分金额

3.`分销功能`：分销商分享产品`赚取佣金`的商业模式，最高`三级`分销，可后台设置`层数`，另外还有分销商`等级`，分销商`分销比率`，
`分销商钱包`，分销商`取现`等等功能

4.`秒杀功能`：已开发。


### Demo:

Pc: http://fecyo.fecshop.com/cn/

H5:http://fecyoh5.fecshop.com/cn/

微信小程序：

![](images/gh_cbfe7e8cdbe1_344.jpg)


商城前端测试用户：  `18661832865`    `111111`  ， 您可以使用该测试账户登陆demo查看分销商的功能



### Walletyo扩展安装


Walletyo扩展应用市场地址：http://addons.fecmall.com/46536133


1.后台在线安装即可，应用市场如何安装应用，参看：http://www.fecmall.com/doc/fecshop-guide/addons/cn-2.0/guide-fecmall-addons-install.html

1.1您应该先安装`fecyo`，然后在安装`walletyo`扩展

1.2安装完成后刷新`cache`，否则某些后台菜单会不显示。

2.应用扩展优先级配置


后台菜单：`应用中心` --> `应用管理` -->  `已安装应用`

设置一下应用的优先级`Priority`: walletyo 的值要比 fecyo的值大，值越大优先级越高。

3.设置store（加入walletyo的模板路径）

1.Store设置（配置第三方模板路径）

1.1网站配置 --> Appfront配置  -->  Store配置

编辑，弹出框，第三方模板路径： `@walletyo/app/appfront/theme,@fecyo/app/appfront/theme/fecyo`

1.2网站配置 --> Apphtml5配置  -->  Store配置

编辑，弹出框，第三方模板路径： `@walletyo/app/apphtml5/theme,@fecyo/app/apphtml5/theme/fecyo`










