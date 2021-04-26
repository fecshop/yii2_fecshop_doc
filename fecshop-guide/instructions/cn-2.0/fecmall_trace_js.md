Fecmall Trace Js用户行为追踪统计
=============

> 通过FA，百度追踪js，google analysis js，facebook js等，将js代码片段加入到fecmall中，进而追踪和统计fecmall商城用户访问数据



### Fecmall Trace Js追踪 - 类型


类型：

**一. FA（Fecmall Analysis）数据分析系统**

默认集成在fecmall中，已经将各个打点加入，将数据收集到FA中进行数据统计，关于FA，详细参看：
[FA-2.0数据分析系统介绍](http://www.fecmall.com/doc/fecmall-guide/fecfa/cn-2.0/guide-fecmall-analysis-2-about.html)

FA系统需要自己搭建，用户数据完全保存到自己的数据库中，而且FA是开源的，您可以根据自己的需要进行二次开发添加业务打点，进行数据追踪。

**二. 第三方追踪js**

百度`追踪js`，`google analysis js`，`facebook js`等，都会给与一段`js代码`您拿到这段js代码后，将其添加到fecmall商城中即可

对于`2.9.4以前`的版本，需要您手动更改代码添加

而对于`2.9.4+`版本，您可以在`后台添加js片段`

1.pc入口添加追踪js代码：


打开后台 `网站配置` --->  `appfront配置` --->  `基础配置`


在`第三方追踪Js片段`中，将您的js代码添加进去，保存即可

2.h5入口添加追踪js代码：


打开后台 `网站配置` --->  `apphtml5配置` --->  `基础配置`


在`第三方追踪Js片段`中，将您的js代码添加进去，保存即可

3.多个`js片段`问题


对于`GTM`，有2个js片段，或者您想添加多个统计js，譬如想加入`facebook js`和`google analysis js`，那么，您可以先添加第一个`js片段`，然后`回车`，
将第N个js片段添加上去，也就是此处可以填写`多个js片段`，`保存`即可。


3.打开fecmall商城，查看`源代码`,检查一下，是否有添加的js代码，确认您添加的js是否成功。



### 代码解析

如果您后台添加了js，但是没有效果，您可以先从这几个部分入手

1.按照上面的js添加后，打开pc页面，浏览器查看源代码html，查看您添加的js是否找到，
如果能找到说明添加的没有问题，而是您的js有问题


2.如果找不到，可以从代码角度找一下原因。

2.1查看你页面的theme目录下的layout文件，是否存在？

譬如文件：`@fecshop/app/appfront/theme/base/front/layouts/main.php`

```
<?= Yii::$service->page->widget->render('base/trace',$this); ?>
```


2.2您安装了扩展，或者自己开发添加的layout文件，如果没有这个代码，请添加上即可

譬如，fecro 首页对应的layouts文件：`@fecro/app/appfront/theme/fecro/layouts/home.php`









