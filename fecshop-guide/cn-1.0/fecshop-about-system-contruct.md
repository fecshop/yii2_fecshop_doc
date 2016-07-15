Fecshop 关于系统结构
====================

Fecshop 是由四个独立包组成，github地址为：http://github.com/fancyecommerce/

四个独立包如下：

Fecshop入口部分：[fancyecommerce/yii2_fecshop_app_advanced](https://github.com/fancyecommerce/yii2_fecshop_app_advanced)

Fecshop基础部分：[fancyecommerce/yii2-fec](https://github.com/fancyecommerce/yii2-fec)

Fecshop后台框架：[fancyecommerce/yii2_fec_admin](https://github.com/fancyecommerce/yii2_fec_admin)

Fecshop核心代码：[fancyecommerce/yii2_fecshop](https://github.com/fancyecommerce/yii2_fecshop)



****************************************************************************

#### Fecshop的入口部分：

[fancyecommerce/yii2_fecshop_app_advanced](https://github.com/fancyecommerce/yii2_fecshop_app_advanced)
，分为Appadmin，Appfront，Apphtml5
，Appserver，Appapi，Console，六个入口，common为上面六个入口的公用部分。

> 其中Console为命令行控制入口，Appadmin为后台入口，Appfront为PC端入口
> Apphtml5为手机web入口，Appserver为手机app服务入口，Appapi为api服务入口


#### Fecshop基础部分：

[fancyecommerce/yii2-fec](https://github.com/fancyecommerce/yii2-fec)
安装后位于vendor/fancyecommerce/fec

> 提供一些底层的helper函数，以及底层的controller，block类供上层使用。

#### Fecshop后台框架部分：

[fancyecommerce/yii2_fec_admin](https://github.com/fancyecommerce/yii2_fec_admin)
，安装后位于vendor/fancyecommerce/fec_admin

> 封装了yii2和DWZ框架（JUI），有用户管理，权限管理，菜单管理，操作日志，缓存管理等功能，
> 对增删改查功能进行了封装，可以快速的做出来增删改查并带有搜索排序分页的表单。


#### Fecshop的核心代码部分：

[fancyecommerce/yii2_fecshop](https://github.com/fancyecommerce/yii2_fecshop)
，安装后位于vendor/fancyecommerce/fecshop，

> app文件夹下面的各个入口对应的模块，配置文件，模板文件等，
> config文件下是全体配置，
> interfaces是接口存放的路径，
> migrations是安装数据库的路径，
> models是数据库映射部分，
> services是Fecshop的服务层文件路径，
> shell是脚本存放路径。






























