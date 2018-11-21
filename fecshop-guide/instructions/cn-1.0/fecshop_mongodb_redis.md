Fecshop 为什么要引入redis mongodb
===============



参看：http://www.fecshop.com/topic/400

里面有回复：

为什么要引入mongodb？对于产品模块，是树形结构，因此在mysql中需要很多的表存储，然后在查询的时候，通过join联合查询得出来数据，作为一个通用商城，用户需要有可以自己在不修改数据库表结构（譬如mysql的表结构）的前提下给产品添加属性，因此，需要通过EAV的引入满足（magento就是引入EAV模型来解决的），这样就会有大量的join，magento的一个分类查询，需要join十几张表，在产品数据几万+的情况下，mysql join操作非常吃内存，并发高的时候性能非常的地下，如果，我想通过单表存储，又能满足我的复杂的查询，又能方便的添加产品属性（不需要修改表结构），又能快速查询，产品数据几万也不会 影响网站性能等等，引入mongodb数据库可以很好的解决这个问题。

关于为什么要引入mongodb，更详细的回答，参看：http://www.fecshop.com/topic/97

1.2、为什么要引入redis？ redis作为内存型数据库，对于存储session和cache，读写非常的快速，另外，如果拆成分布式，php多台主机，需要共享缓存和session，引入redis能更好的解决这些问题




mongodb的并发高，易于横向扩展，高可用复制集也很容易搭建，而且支持多维数据存储，缺点是不支持多表事务

因此对于不需要多表事务的数据，存储到mongodb中，譬如：产品，分类，cms page等，mongodb的高并发数比mysql优异很多

但是对于需要多表事务的存储到mysql中，譬如cart  order 产品库存表， coupon等，都在mysql

在实际操作中，有一些数据理论上要求100%，但是实际有点差异也不会影响很大，譬如cart表，在生成订单后需要清空购物车，这是一个事务多表操作，但是在实际情况中，即使没有清空购物车也不会带来致命的影响，
因此cart也可以存储到redis中，譬如fecshop的redis cart扩展：https://github.com/fecshop/yii2_fecshop_redis_cart

对于各个数据库对应的表:http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-database.html

多种数据库，肯定对新手第一次的学习增强难度，但是fecshop的定位就是要做一个实战性比较强的电商框架，
而且fecshop的架构，不是依赖于某一种存储方式的，通过services层的引入，你可以方便的重构底层，同一个功能，可以提供多种实现，譬如：https://github.com/fecshop/yii2_fecshop/tree/master/services/cms/staticblock
就有mysql和mongodb两种实现，可以通过配置切换选择哪种存储方式，当然，底层存储不局限于model，也可以是远程的api。

易于扩展，易于重构，尤其是易于重构底层，是fecshop很具有特色的地方，因此发挥各个数据库的优势，让系统更强劲。














