Fecshop Session为什么要自己封装
===============================

Fecshop自己封装了session，而不是直接使用Yii2的session，也就是
session services


因为fecmall是多入口模式，除了传统的pc和html5这种支持php session的入口，还有
appserver这种前后端彻底分离，基于api的入口，
而session是贯穿在services里面的，而services是各个入口的公用层，
因此，使用yii2的session是不能满足的，需要封装解决


关于 Fecmall Session更详细的介绍，参看：

[Fecmall Session 机制](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_session.html)


































