Fecmall Admin 功能介绍
=========================

> 关于该入口的描述和说明


### Appadmin 介绍


1.产品管理

1.1产品信息管理

后台可以编辑产品，在操作前，您需要先了解一下fecshop的产品，参看详细：
[Fecmall 产品](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_product.html)

您可以对spu产品，譬如颜色尺码，进行一次全部添加

![](images/p3.png)

1.2产品属性管理

您可以编辑，新增产品属性，属性分为`普通属性` 和 `spu属性`

`普通属性`： 是产品的一个属性，用来记录值

`spu属性`：规格属性，譬如颜色尺码等

1.3产品属性组管理

您可以添加`产品属性组`，为产品属性组添加`产品属性`，并设置排序参数，
当创建新产品选择该属性组后，就会拥有该属性组对应的属性。

![](images/p5.png)

1.4产品参数管理

您可以编辑产品的一些参数

1.5产品评论管理

在这里可以查看到前台用户提交的评论，您可以在这里批量审核和批量拒绝，
修改和删除评论等

关于评论的设置，您可以参看[FecShop 产品评论](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_product_review.html)

1.6产品收藏管理

显示的是前端用户收藏的产品的数据列表

1.7产品批量上传

您可以批量上传你的产品数据

2.分类管理

2.1分类信息管理

在这里可以管理分类数据，详细的可以参看文章：
[Fecmall 分类](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_category.html)

2.2分类排序参数配置

您可以配置分类排序的参数

3.url重写管理

产品分类等数据保存时生成的url伪静态链接数据列表，更新的详细参看
: [Fecmall Url重写](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_url_rewrite.html)

4.应用中心

4.1应用市场

您在[应用市场商城](http://addons.fecmall.com/)购买应用后,
可以在此处看到自己购买的应用，点击安装，即可进行在线安装应用。

4.2已安装应用

对于已经安装的应用进行管理

4.3应用Gii生成

应用开发者使用的功能，您可以使用该功能进行Gii初始生成应用插件。

5.商城管理

5.1订单管理

这里是各个入口下的订单列表，关于订单的详细可以参看：
[Fecshop 订单](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_order.html)

5.2订单参数管理

您可以在这里进行订单参数的配置

5.3购物车参数配置

您可以在这里对购物车参数进行配置

5.4优惠券

详细参看：[Fecmall 优惠券](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_coupon.html)

5.5用户管理

查看管理商城前端用户

5.6Newsletter

订阅newsletter的用户列表


6.网站商城配置

这里的配置项非常的多，您可以在这里对商城进行全访问的配置，这里不一一列举。




7.Cms 

7.1文章Article部分

这里是前端访问的page单页，譬如：https://fecshop.appfront.fancyecommerce.com/about-us

一般是网站的文字条款，关于详细参看：
[Fecmall page页（文章）](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_page.html)

7.2.静态块-staticBlock

这里是保存了一个个的区域性的html快
，在程序中可以调用这些保存到数据库的html块，
对于一些业务经常需要编辑的部分，可以使用这种静态块
的方式，让业务方便编辑。

更多参看：[Fecmall 静态块](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_static_block.html)


8.我的账户 

个人的账户编辑

9.账户管理

后台入口的账户管理

10.权限管理  菜单管理

这里设置权限组，权限组和菜单绑定，
详细的设置可以参看

[fecmall，如何后台添加菜单，设置权限，并访问](http://www.fecshop.com/topic/437)

11.操作日志  日志管理

这里是一个简单的，后台用户访问的记录，
可以查看公司各个客服业务的操作记录。

12.缓存管理

这里是刷新缓存，注意，这里清空的是后台的缓存。



13.Log 打印输出

这个无用，要删除掉的

14.ErrorHandle

这个是fecmall的Errorhandle机制，

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


更详细的信息参看：[Fecmall Error Handler](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_error_handler.html)








