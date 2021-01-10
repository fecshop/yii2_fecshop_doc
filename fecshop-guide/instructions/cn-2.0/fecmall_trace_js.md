Fecmall Trace Js追踪
=============

> 通过FA，百度追踪js，google analysis js，facebook js等，将js代码片段加入到fecmall中，进而追踪和统计fecmall商城用户访问数据



### Fecmall Trace Js追踪 - 类型


类型：

一.FA（Fecmall Analysis）数据分析系统

默认集成在fecmall中，已经将各个打点加入，将数据收集到FA中进行数据统计，关于FA，详细参看：
[FA-2.0数据分析系统介绍](http://www.fecmall.com/doc/fecmall-guide/fecfa/cn-2.0/guide-fecmall-analysis-2-about.html)

FA系统需要自己搭建，用户数据完全保存到自己的数据库中，而且FA是开源的，您可以根据自己的需要进行二次开发添加业务打点，进行数据追踪。

二.第三方追踪js

百度`追踪js`，`google analysis js`，`facebook js`等，都会给与一段`js代码`您拿到这段js代码后，将其添加到fecmall商城中即可

对于`2.9.4以前`的版本，需要您手动更改代码添加

而对于`2.9.4+`版本，您可以在`后台添加js片段`

1.pc入口添加追踪js代码：


打开后台 `网站配置` --->  `appfront配置` --->  `基础配置`


在`第三方追踪Js片段`中，将您的js代码添加进去，保存即可

2.h5入口添加追踪js代码：


打开后台 `网站配置` --->  `apphtml5配置` --->  `基础配置`


在`第三方追踪Js片段`中，将您的js代码添加进去，保存即可


3.打开fecmall商城，查看`源代码`,检查一下，是否有添加的js代码，确认您添加的js是否成功。























