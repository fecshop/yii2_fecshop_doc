Fecshop 介绍
====================

> Fecshop，是由Terry一人从2015年初开始，一直坚持到今天的开源电商项目，非商业化运作，是真正
> 开源的电商系统， 遵循OSL3.0开源协议，您可以免费的应用于您的线上商城。如有任何其他疑问，
> 可以联系邮箱：2358269014@qq.com

Fecshop 全称为Fancy ECommerce Shop，是基于php Yii2框架之上开发的一款优秀的开源电商系统，
遵循OSL3.0开源协议，
预计到2017-05月份 ，完成appfront（pc前端web），appadmin（后台）
命令控制台 这几个入口 ，目前appfront和appadmin功能已经打通，但是，系统的代码bug需要排查，
代码需要优化，不建议应用到生产环境，如果您一定要在生产环境中用，可以联系我，我会随时
技术支持,
Terry从事外贸电商6年来， 用了不少开源电商系统，譬如magento，
发现开源框架都有一定 的诟病，在并发方面差，后期扩展，业务发展后期重构难， 
尤其是现在的移动端的发展，多入口的电商模式占据主流， 
性能方面的要求越来越高，Fecshop基于Yii2的高效框架，在此基础上进一步封装，加入了
service层和block层，数据库采用了nosql和mysql结合的方式， 
关系型表放到mysql中，譬如优惠券，购物车，订单等， 
非关系型数据表（非关系型代表不会出现多表强事务类型操作） 放到mongodb中，
缓存用redis，搜索目前用的是mongodb的FullTextSearch功能，
支持一些主流语言的分词与搜索，不过目前中文搜索不支持分词，
后期会扩展ElasticSearch来进行搜索（ElasticSearch有中文插件，安装后支持中文分词）。
总之，Fecshop目前的定位是为了让程序员们有一个方便学习，扩展，开发的电商框架系统，
如果您发现有哪些代码结构可以优化，调整，或者您有更加合理的建议，可以发送到邮箱：
2358269014@qq.com。

GitHub各个包的说明：

1.基础扩展部分：

FEC 基础扩展：https://github.com/fancyecommerce/yii2-fec

DWZ和Yii2封装的后台框架：https://github.com/fancyecommerce/yii2_fec_admin

2.FecShop代码部分

Fecshop 核心代码部分：https://github.com/fancyecommerce/yii2_fecshop

FecShop 入口部分:https://github.com/fancyecommerce/yii2_fecshop_app_advanced

Fecshop的文件结构和Yii2的类似：

Yii2的核心代码部分在：/vendor/yiisoft/yii2

Fecshop核心代码部分在：/vendor/fancyecommerce/fecshop中

Yii2的入口部分有2个.

一个是基础版入口：https://github.com/yiisoft/yii2-app-basic

一个是高级版入口：https://github.com/yiisoft/yii2-app-advanced，

相当于FecShop

入口部分:https://github.com/fancyecommerce/yii2_fecshop_app_advanced

总之，很类似，对这个有疑问的朋友也比较多，为什么要做成扩展包，原因：
要解决fecshop升级和使用者二开的文件冲突问题。
使用者无权修改/vendor/fancyecommerce/fecshop下面的文件，只能通过配置的方式进行
重写，如果强制修改/vendor/fancyecommerce/fecshop下面的文件，升级后将会被清除。

3.Fecshop文档部分：

https://github.com/fancyecommerce/yii2_fecshop_doc

4.个人博客：

http://www.fancyecommerce.com/

5.个人CSDN博客

http://blog.csdn.net/terry_water














