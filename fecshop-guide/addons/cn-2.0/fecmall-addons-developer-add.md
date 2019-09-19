Fecmall-开发应用以及发布
===============

> 了解了fecmall应用的安装原理，加载原理以及如何发布，本部分完整的串一下整个过程

### Fecmall应用开发步骤


1.应用市场，成为开发者，创建应用

1.1申请成为开发者，详细参看： [Fecmall-开发者中心](fecmall-addons-developer-center.md)

成为开发者，成为开发者，才有资质进行开发。



2.Fecmall电商商城，创建应用文件

Fecmall开发了应用快速创建工具（快速初始化文件），您可以在后台创建应用

登陆账户后，填写信息，即可初始化


*  [Fecmall-应用初始化工具](fecmall-addons-developer-init-tools.md)



3.找到初始化创建的应用文件



进入文件夹：`@addons/package包名/应用插件包名/`,
可以看到文件

`config.php`： 应用配置文件

`README.md`：说明文件

`administer/Install.php`：应用安装文件

`administer/Uninstall.php`：应用卸载文件

`administer/Upgrade.php`：应用升级文件

4.进行应用功能开发

这个部分，如何在config.php进行配置，参考`Fecmall开发者`部分的文档



5.打包上传

进入文件夹：`@addons/package包名/应用插件包名/`

```
zip -r   应用插件包名.zip  ./*
```

注意，一定要进入`应用插件包名`里面进行打包，然后上传

参看：[Fecmall-开发者中心](fecmall-addons-developer-center.md)

6.管理员审核

管理员审核通过后，就可以下载了，如果是其他的账户，需要先进行应用的下单，添加到`我的应用`
中才可以安装


























