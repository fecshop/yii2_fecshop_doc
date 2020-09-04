Fecro 扩展应用文件结构介绍
===========

> Fecro文件路径以及文件的介绍

### Fecro 安装路径

1.应用市场安装fecro后，扩展包的文件位于`./addons/fecmall/fecro下面`


2.打开这个文件夹，您可以看到完整的fecro的代码文件以及配置文件


### Fecro内部文件介绍

1.文件夹：./administer

fecro扩展初始安装的sql初始化，以及图片文件复制等

`Install.php`: 应用初始安装文件

`Uninstall.php`: 应用卸载的文件

`Upgrade.php`: 应用升级的文件


2.文件夹：`./app`

各个应用入口的文件

3.文件夹：`./models`

models文件夹，里面是数据库model

4.文件夹：`./services`

services文件夹，里面是各个功能services

5.文件：`config.php`

fecro应用扩展的配置文件








