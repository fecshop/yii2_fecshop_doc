Fecmall数据清理脚本
==========

> fecmall的一些数据清理



### Fecmall数据清理脚本

为了方便处理和安装，fecerp基于fecmall，扩展的形式开发，但是需要将一些fecmall的东西清理掉，
特此开发了此脚本

对于fecerp系统新建的表，都是以`erp_`开头，fecmall原有的一些表会用到，有一些表不会用到，但是
，fecmall的表还是都保留了下来，不做处理


目前清理脚本，主要处理的是admin_url_key表里面的资源部分，将fecmall的资源清空，方便做权限控制

脚本文件路径：

```
./addons/fecmall/fecerp/shell/clearFecmallData.sh
```

您安装fecerp后，可以执行这个脚本，进行清理

```
cd  ./addons/fecmall/fecerp/shell
sh clearFecmallData.sh

```





























