Fecmall Admin 文件结构
=========================

> 关于该入口的描述和说明


### Appadmin 文件路径


Appadmin端，是fecmall后台入口，主要涉及到一些数据库数据的编辑工作，该入口的文件是在
`@fecshop/app/appadmin` 文件夹下面

### fec_admin库包

fec_admin github地址为：https://github.com/fecshop/yii2_fec_admin
，fecadmin是Yii2+JUI（DWZ），封装的库包，用来快速的做后台的扩展。

fecshop安装后，会以依赖的方式把fecamin安装在vendor/fancyecommerce/fec_admin文件夹下面

appadmin，依赖于fecadmin库包，在此基础上做的进一步的封装。



### Appadmin文件结构

1.主文件夹文件结构

Appadmin部分，基于fec_admin，在此基础上重新进行了封装，
打开 `@fecshop/app/appadmin`，你会发现下面的文件（
https://github.com/fecshop/yii2_fecshop/tree/master/app/appadmin）：

`config`:  appadmin端的配置部分

`languages`: appadmin端的多语言部分（后台目前还没有做多语言）

`modules`: appadmin的模块部分

`theme`: appadmin的模板部分

2.模板路径配置

fecmall appadmin 默认模板的配置：`@fecshop/app/appadmin/config/params.php` 配置参数 `appadminBaseTheme`

fecmall appadmin 本地模板路径：`@appadmin/config/params.php` 配置参数 `localThemeDir`

关于模板知识，更多：[fecshop模板开发](fecshop-theme.md)

3.modules介绍

可以参看 [fecshop 文件架构](fecmall-construct-framework.md)






