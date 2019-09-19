![Fecmall 介绍](images/fecmall_logo.png)
====================

> Fecmall，是由Terry从2015年初开始，一直坚持到今天的开源电商项目，是真正
> 开源的电商系统， 遵循BSD-3-Clause开源协议，您可以免费的应用于您的线上商城。如有任何其他疑问，
> 可以联系邮箱：2358269014@qq.com


Fecmall 全称为Fancy ECommerce Mall，是基于php Yii2框架之上开发的一款优秀的开源电商系统，
遵循BSD-3-Clause开源协议，Fecmall支持多语言，多货币，架构上支持pc，手机web，手机app，和erp对接等入口，您可以免费快速的定制和部署属于您的电商系统。
截止到2017-12-15，appfront（pc前端web），appadmin（后台），apphtml5（wap端web），
appserver（VUE，手机app的api提供端），console（命令行），
appapi（和第三方系统通信端）都已经完成，现在已经趋于稳定，
Terry在2010年开始进入跨境电商领域， 用了不少开源电商系统，譬如magento，
发现开源框架都有一定 的诟病，在并发方面差，后期扩展，业务发展后期重构难， 
尤其是现在的移动端的发展，多入口的电商模式占据主流， 
性能方面的要求越来越高，Fecshop基于Yii2的高效框架，在此基础上进一步封装，加入了
service层和block层，数据库采用了nosql和mysql结合的方式， 
关系型表放到mysql中，譬如优惠券，购物车，订单等， 
非关系型数据表（非关系型代表不会出现多表强事务类型操作） 放到mongodb中，
缓存用redis，搜索目前用的是mongodb的FullTextSearch功能，
支持一些主流语言的分词与搜索，对于中文搜索，使用的是xunsearch，
后期会扩展ElasticSearch来进行搜索（ElasticSearch有中文插件，安装后支持中文分词）。
总之，Fecmall目前的定位是为了让程序员们有一个方便学习，扩展，开发的电商框架系统，
如果您发现有哪些代码结构可以优化，调整，或者您有更加合理的建议，可以发送到邮箱：
2358269014@qq.com。

**Fecmall线上案例**：http://www.fecmall.com/topic/55

**关于Fecmall**：http://www.fecmall.com/first

**Fecmall的各种问题解答QA**：http://www.fecmall.com/topic/400

**Fecmall 【Appfront】PC Web Demo **：http://fecshop.appfront.fancyecommerce.com/

**Fecmall 【Apphtml5】Mobile Web Demo（WAP）**：http://fecshop.apphtml5.fancyecommerce.com

**Fecmall 【Appserver】Mobile VUE Demo(Appserver,前后端彻底分离模式)**：http://demo.fancyecommerce.com/#/

**Fecmall 开源协议**：http://www.fecshop.com/license

**Fecmall 使用说明文档地址：** http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-README.html

**Fecmall 二次开发文档地址：** http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-README.html

**Fecmall Github地址：**https://github.com/fancyecommerce/yii2_fecshop

**Fecmall oschina地址：** https://www.oschina.net/p/fecshop

**Terry个人博客：**http://www.fancyecommerce.com/

**TerryCSDN博客：**http://blog.csdn.net/terry_water














