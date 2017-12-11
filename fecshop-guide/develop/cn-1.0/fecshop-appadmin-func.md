Fecshop Admin 功能介绍
=========================

> 关于该入口的描述和说明


### Appadmin 介绍


1.产品信息管理

后台可以编辑产品，在操作前，您需要先了解一下fecshop的产品，参看详细：
[Fecshop 产品](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_product.html)


2.产品评论管理

在这里可以查看到前台用户提交的评论，您可以在这里批量审核和批量拒绝，
修改和删除评论等

关于评论的设置，您可以参看[FecShop 产品评论](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_product_review.html)

3.产品收藏管理

显示的是前端用户收藏的产品的数据列表

4.分类管理

在这里可以管理分类数据，详细的可以参看文章：
[Fecshop 分类](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_category.html)

5.url重写管理

产品分类等数据保存时生成的url伪静态链接数据列表，更新的详细参看
: [Fecshop Url重写](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_url_rewrite.html)

6.订单管理

这里是各个入口下的订单列表，关于订单的详细可以参看：
[Fecshop 订单](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_order.html)

7.优惠券

详细参看：[Fecshop 优惠券](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_coupon.html)

8.账户管理

这里可以查看前端部分注册的用户信息

9.Cms 文章Article部分

这里是前端访问的page单页，譬如：https://fecshop.appfront.fancyecommerce.com/about-us

一般是网站的文字条款，关于详细参看：
[Fecshop page页（文章）](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_page.html)

10.静态块-staticBlock

这里是保存了一个个的区域性的html快
，在程序中可以调用这些保存到数据库的html块，
对于一些业务经常需要编辑的部分，可以使用这种静态块
的方式，让业务方便编辑。

更多参看：[Fecshop 静态块](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_static_block.html)


11.我的账户 

个人的账户编辑

12.账户管理

后台入口的账户管理

13.权限管理  菜单管理

这里设置权限组，权限组和菜单绑定，
详细的设置可以参看

[fecshop，如何后台添加菜单，设置权限，并访问](http://www.fecshop.com/topic/437)

14.操作日志  日志管理

这里是一个简单的，后台用户访问的记录，
可以查看公司各个客服业务的操作记录。

15.缓存管理

这里是刷新缓存，注意，这里清空的是后台的缓存。

16.后台配置

这个目前没有用到，这里的初衷是为了在后台设置某些配置，
然后在前端直接取出来，这个针对一些经常变动的配置，
方便业务操作。

17.Log 打印输出

这个无用，要删除掉的

18.ErrorHandle

这个是fecshop的Errorhandle机制，

对于线上环境，如果报错直接输出，会暴露网站的很多信息，这样是非常不安全的，
而如果使用yii2默认的`PROD`的``errorHandler处理方式，只显示一句
`An internal server error occurred.`，用户反馈报错给开发者后， 开发者在日志中看到一堆的报错，不知道那个报错是这个用户的报错， 因此不利于开发者快速的定位问题。

比较好的方式，在报错的时候，系统在写入日志的时候，返回一个错误编码，

```
{
    "code":500,
    "error_no":"5a2113f5bfb7ae617546c872"
}
```

用户访问页面报错后，将错误编码反馈给开发者，开发者 通过错误编码，到日志中找到该用户的报错信息，这样可以更方便的处理用户的 的错误。


更详细的信息参看：[Fecshop Error Handler](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_error_handler.html)








