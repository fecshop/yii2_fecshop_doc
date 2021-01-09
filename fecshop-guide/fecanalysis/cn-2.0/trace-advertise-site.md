站内广告统计
==============

> 网站内部的广告统计


站内广告：指的是网站内部的广告图片，譬如首页的走马灯图片，内容部分的广告图
，分类页面，产品页面等显示的广告图，这些广告图都会对应一个链接，
我们可以在这个广告图的后面加一个广告后缀，然后统计这个广告的点击情况



1.站内广告后缀生成

站内广告的格式如下：

1.1、url的后缀加一个`eid=xxx`即可


1.2、eid的值自己定义，长度为10位之内，字符串和数字都可以

1.3、每一个站内广告的`eid必须唯一`

2.示例

2.1 

url：http://fecshop.appfront.fancyecommerce.com/men

站内广告url：http://fecshop.appfront.fancyecommerce.com/men?eid=1000001

2.2

url：http://fecshop.appfront.fancyecommerce.com/men?color=khaki

站内广告url：http://fecshop.appfront.fancyecommerce.com/men?color=khaki&eid=1000002


3.将生成好的url，挂到广告图片上即可

一定要注意，每一个站内广告的`eid`这个参数不要写错，`eid的值`要`唯一`
，否则将会导致统计不到数据，或者统计出错


4.在菜单中可以查看各个站内广告的点击情况，设备浏览器，停留时间，跳出率等等













