Fecro 跨境电商企业版安装
==============


> FecMall Fecro 跨境电商B2C企业版, 进行安装和配置





准备工作READY
--------

1.安装fecmall开源商城，安装地址参看：[Fecmall开源商城安装](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecshop-2-graphical-install.html)

2.应用市场注册账户，加入购物车，免费下单，应用市场地址：http://addons.fecmall.com/59577615

*注意1*: 因为是在线下载安装，Fecro的压缩包大致为6MB，php默认的执行时间为30秒，如果在此时间内下载超时，将会安装报错，
因此您需要设置php的最大超时时间，详细参看帖子：http://www.fecmall.com/topic/2474

*注意2*: Fecro是`系统级别`的扩展，`不能安装`fecmall开源系统对应的`模板`，安装后不兼容，如果后续开发了针对fecro的模板，会着重说明


应用市场在线安装Fecro
-----------

1.下单完成后，fecmall后台在线安装fecro应用系统，关于应用市场的使用，参看：[Fecmall应用市场-安装应用扩展文档](http://www.fecmall.com/doc/fecshop-guide/addons/cn-2.0/guide-fecmall-addons-install.html)

2.安装完成后，就进入配置阶段


Fecro配置
-----------

1.Store设置（配置第三方模板路径）

1.1网站配置 --> Appfront配置  -->  Store配置

编辑，弹出框，第三方模板路径： `@fecro/app/appfront/theme/fecro`

1.2网站配置 --> Apphtml5配置  -->  Store配置

编辑，弹出框，第三方模板路径： `@fecro/app/apphtml5/theme/fecro`


2.测试产品数据初始化

fecro已经默认集成了淘宝产品插件，因此，默认的fecmall的测试产品，需要初始化一下（ 关于淘宝模式产品 ）

```
cd addons/fecmall/fecro/shell
sh initTbProduct.sh
```


3.首页Banner以及底部静态块配置

详细参看：[FecMall Fecro 首页Banner以及静态块配置](fecmall-fecro-banner-config.md)


对于支付，物流等配置，请参看fecmall的文档。


### Fecro 图片

Fecro的图片在安装的时候自动复制，但有一些童鞋反应图片没有复制完全，如果出现这个情况，可以手动操作一下

将文件夹`./addons/fecmall/fecro/app/appimage/common/addons/fecro/`下面所有的图片
覆盖到`./appimage/common/addons/fecro/`文件夹下面

譬如linux下执行cp命令

```
\cp -rf  {$fecmall_root_dic}/addons/fecmall/fecro/app/appimage/common/addons/fecro/*   {$fecmall_root_dic}/appimage/common/addons/fecro/

```

将`{$fecmall_root_dic}`替换成您的fecmall安装的文件路径，然后再执行cp命令。





























