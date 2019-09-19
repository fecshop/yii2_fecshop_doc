Fecmall-2.x 介绍
============


> Fecmall 2.x 版本，是在1版本上面，进行了一系列的底层重构和优化，大幅度的进行整改的版本
> ，关于Fecmall-2版本和1版本的差异，可以参看：[Fecmall-2和1版本差异](fecshop-2-1-diff.md)

### 关于Fecmall项目

Fecmall开源电商系统，是从2015-10月开始筹划开发，一直维护至今的系统，
现在已经是Fecmall-2.x版本，一直维护更新

对于fecmall项目，最开始的初衷是为了满足自身需要（非公司），因为工作当中
的电商系统，使用的开源系统譬如magento，zencart，opcart等，都存在一定的问题，
作为一个`中型电商网站商城`，无法满足自身需要，二次开发繁琐效率低下，
性能问题，以及重构底层（譬如购物车由mysql替换成redis）等，都存在难度，
因此，基于yii2框架开发了fecmall开源电商系统

fecmall-1.x版本，是一个纯程序员电商商城系统，使用了工具比较多，php，
mysql，redis，mongodb，xunsearch，等，因此在安装配置过程中，比较
繁琐，中高级php程序员才玩的起来，光安装这个步骤就把大把的人挡在外面，
随着使用者的关注，吐槽安装难的呼声越来越高，另外，很多的参数配置都是在后台配置，
后台界面丑陋等等，由于是一个程序员产品，因此更多的是关于框架体系，
如何方便程序员应对项目发展中遇到的各种问题，而不是小白用户，
造成使用起来非常的不方便，fecmall优化用户体验势在必行。

fecmall-2版本是为了降低门槛，默认只需要mysql即可，加入了界面安装，
更多的是做用户体验，以及生态应用市场，现在安装越来越方便，安装应用
也可以直接在线安装，应用市场高度开发，开发者都可以上传自己开发的应用赚取RMB，
互利共赢。


Fecmall-2版本在降低门槛的同时，并没有抛弃原来的功能，而是进行了多种实现，
譬如产品serivices，有mongodb和mysql两种实现方式，用户可以
通过后台配置，进行services切换到不同的数据库，这样满足不同的用户的需求。

Terry于2019年6月份开始全职维护Fecmall，并注册公司：青岛飞猫科技有限公司
，申请商标`fecmall`,全力做应用市场，扩展生态，
更好的维护fecmall，让更多的用户参与到fecmall中，免除后顾之忧。

关于fecmall的其他的一些资料，可以参看：

Fecmall介绍： http://www.fecmall.com/first

Fecmall演示：http://www.fecmall.com/yanshi

Fecmall授权协议：http://www.fecmall.com/license

Fecmall项目历程：http://www.fecmall.com/site/timeline

Fecmall案例：http://www.fecmall.com/topic/55#w3

FecmallQA：http://www.fecmall.com/topic/400


### 关于框架

fecmall是一个注重框架体系的电商系统，基于yii2框架开发的电商系统，扩展性强，安全性高，框架层面应对高并发部署，
适合用户搭建属于自己的小型，中型电商系统。



Fecshop 全称为Fancy ECommerce Shop，是一款优秀的开源电商系统，遵循BSD-3-Clause开源协议，
目的是为了方便yii2用户快速的
开发商城，Fecshop作为一款可以持续性发展的商城系统，
在框架层面有以下特性：

1. 由于商城系统的复杂性，原始的框架MVC结构，显的有点力不从心，Fecshop框架
加入了`Block层`，
Controller层只负责调度， Model只负责数据库映射，中间的处理逻辑由block来完成，View层
负责显示，这样各司其职， 以免造成controller文件过于庞大。

2. 加入`独立功能块`，有点类似Yii2的Widget，目的是为了让一些侧栏公用块
可以通过配置的方式
添加，同时，还可以具有设置缓存的功能，譬如侧栏的产品浏览记录，
newsletter等独立显示块可能在很多
页面用到，通过独立功能块可以配置方便的载入。

3. 在Model层的上层加入`服务层Services`，这样，Controller，Block，View 层，在原则上
不能直接调用model，必须通过Services层以及子Services层，然后Services访问各个
model，组织数据，事务处理等操作，将数据结果返回给上层，这种设计可以方便以后业务
发展后，进而根据业务特点进行重构，或者以后如果出现新技术，新方式，
都重构成自己想要的样子，譬如，
将某个底层由mysql换成mongodb，或者为了应付高并发读写并且多事务性的功能部分，
进行分库分表的设计方式。

4. Fecshop`多模板系统`，Fecshop设置了多个模板路径，各个模板路径下的文件被加载
的优先级不同，其中，Fecshop的模板路径下的文件最全面，但是优先级最低，
，第三方模板路径优先级其次，用户本地模板路径优先级最高，
用户可以通过
复制相应路径下的view或者js，css文件到本地模板路径，存在于高优先级
模板路径的文件会被优先加载，这样用户可以通过多模板系统的原理进行模板的
制作，同时，不影响Fecshop模板的升级，如果Fecshop view文件升级后被修改，
那么用户可以比对本地模板文件与升级模板文件的代码的不同，
复制更改的代码到本地模板路径
即可。第三方的模板路径的优先级介于本地模板路径和Fecshop
模板路径之间。

5. `重写机制`，Fecshop的功能基本都可以被用户重写，包括servies层，Modules，
Controller，Block，Views，View Layout，
以及Js Css Img等，都可以被用户重写，其中 Js，Css，Img，Views，View Layout
 是通过多模板
路径优先级来实现的，其他的是通过配置文件的覆盖更改来实现重写，这样，用户
就可以很方便重构Fecshop或者第三方的功能和模板。

6. 升级最小化干扰，Fecshop的核心文件是放到vendor/fancyecommerce/fecshop
路径下面，和第三方扩展，用户二次开发路径完全隔离开，
Fecshop可以通过composer进行核心功能的升级，用户只需要通过composer升级
即可。

7. 快速高效，`Fecshop Servises`遵循Yii2的懒加载方式，只初始化使用到的组件服务，
缓存方面有整页缓存，block部分缓存，动态数据ajax加载等方式，让您的网站快速响应。

8. `Fecshop 多入口模式`，分为 appadmin（后台）， appfront（PC前端），apphtml5（手机web），
appserver（手机app服务），appapi（erp，或者其他接口对接），
不同的业务，不同的设备，进入不同的入口，各个入口共用服务层services，
但是modules部分独立，这样相互干扰最小，可以相互独立开发。

9. 后台封装化，fec_admin扩展可以快速的实现增删改查类型的表单列表，
方便用户快速的做增删改查。

鉴于以上特点，您可以下载安装fecshop，然后更改fecshop的模板和功能，扩展自己想要
的功能，或者安装第三方开发好了的扩展或者模板，来快速的组建起来您的网站。


### 关于商用

Fecmall代码100%开源，遵循BSD开源协议，在国内的鱼龙混杂的环境下，
为了更好保护fecmall的版权信息，进行了一些条件的附加，详细参看:http://www.fecmall.com/license

通俗的理解fecmall的授权协议：如果是您公司内部的项目，或者你的朋友等一些项目，
您基于fecmall做相应的商城，是免费授权的，
如果您是建站公司，将fecmall进行二次开发，然后包装成了新的`建站产品`，然后重新
命名（譬如命名：xxxShop）,进行商业宣传完全自研等等一些伪造话语，
对于这种不良商家的这种行为是不允许的，基于fecmall的新产品，必须以fecmall开头命名

Fecmall单商户系统是`没有付费`版本的，只有一个开源版本并一直维护开发，
只对应用市场的应用插件模板进行收费。

总之，fecmall作为一款真正开源的电商商城，在保护自身的情况下，最大化的开放。

### 关于二次开发

fecmall是一款对程序员友好的电商系统，基于composer发布库包，方便升级的同时，
允许程序员在不修改源代码文件的前提下，对程序功能进行重写，以及开发新的功能。

### 关于应用市场

为了完善fecmall的生态，丰富fecmall的应用插件模板，上线了Fecmall应用市场，
最大化的开放，php开发者可以将自己开发的应用发布到应用市场平台，赚取 RMB
，详细参看：[Fecmall应用开发市场](http://www.fecmall.com/doc/fecshop-guide/addons/cn-2.0/guide-fecmall_addons_about.html)



























