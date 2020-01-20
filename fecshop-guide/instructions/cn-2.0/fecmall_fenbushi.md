Fecmall分布式部署
============

> 访问压力大，可以mysql，mongodb，php放到不同的主机上面，
多台php-fpm的方式部署。


多台`php`服务器，会涉及到如下的一些问题


### 图片问题

1.您可以`图片云OSS`解决，国内的`七牛云`，`阿里云`都有存储图片，以及对图片`缩放水印`等处理的功能
，您可以把图片放到云端，这样直接就解决了分布式php，`图片存储`的问题

[Fecmall 阿里云图片oss存储fecmall产品图片](http://addons.fecmall.com/27157121)

[Fecmall 七牛云图片文件服务oss存储fecmall产品图片](http://addons.fecmall.com/75526679)

您可以点击上面得了链接，使用`官方扩展`完成分布式图片的问题



2.如果您不使用云服务器，可以自己搞一个图片服务器，然后通过`linux NFS`将
图片服务器的`appimage`映射到`php`服务器中fecmall目录下的`appimage`，
这个相当于`内网服务器挂载`，各个php服务器的`appimage`文件夹，都是挂载的图片服务器的`appimage`，
然后将`图片域名`解析到图片服务器，即可解决


### 缓存和session

fecmall的`缓存`和`session`存储在`redis`里面，因此此问题解决


[Fecmall 使用redis](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecshop-2-use-redis.html)

### js和css


fecmall分布式后，对于前台会出现`js`和`css`找不到的问题，这是因为
`nginx`接收请求，发给php请求，php处理完成后返回，但是js和css的url请求可能走的是另外的机器（另外的机器可能没有被执行，导致js和css没有被发布），进而导致文件无法访问
，可以这样接解决（`appadmin`无法通过这种方式解决，`appfront，apphtml5`可以这样解决，对于其他的入口不加载js和css，因此不需要考虑这个问题）

1.找一台机器，将这个机器的某个文件夹`A`挂载到各个php中(譬如路径：`/www/web/fecshop/jscss/appfront/assets`),
可以通过linux的NFS挂载，也就是在各个php访问文件夹`/www/web/fecshop/jscss/appfront/assets`，对应的是这台机器的这个文件

2.在这台机器上面配置域名 `http://appfront.xxxx.com` ，对应到文件夹`A`

3.打开`@app/config/fecshop_local_services/Page.php`文件

```
/**
                 * @var string the root directory string the published asset files.
                 * 设置: js和css的发布路径
                 * 譬如设置为：'@appimage/assets'，也可以将 @appimage 换成绝对路径
                 */
                //'basePath' => '@webroot/assets',
                /**
                 * @var string the base URL through which the published asset files can be accessed.
                 * 设置: js和css的URL路径
                 * 可以将 @web 换成域名 ， 譬如  `http:://www/fecshop.com/assets`
                 * 这样就可以将js和css文件使用独立的域名了【把域名对应的地址对应到$basePath】。
                 */
                //'baseUrl' => '@web/assets',
                'basePath' => '/www/web/fecshop/jscss/appfront/assets',
                'baseUrl' => 'http://appfront.xxxx.com',
```

`baseUrl`里面设置的是上面的域名

`basePath`是各个php的文件夹，这个文件夹就是局域网远程服务器`A`的文件


这样，各个php实例的php将`js`和`css`发布到路径'/www/web/fecshop/jscss/appfront/assets'，但这个文件夹
是远程挂载过来的，实际是服务器的`A`文件夹，这样各个php的发布路径是同一个文件系统

对于页面加载`js`，域名会使用`baseUrl`设置的域名，而这个域名 `http://appfront.xxxx.com`解析到了远程服务器的`A`文件夹，因此可以访问到css和js文件。

4.如果使用`cdn`。那么很容易，因为js css是独立的域名，将这个域名解析到你的cdn服务器，然后做一下源站IP指向就OK

关于cdn，可以使用fecmall官方cdn扩展：[Fecmall CDN加速扩展应用](http://addons.fecmall.com/86929949)

5.后台框架，是不支持fecshop的page assets services的，
因此 https://github.com/fecshop/yii2_fecshop/blob/master/services/page/Asset.php 对其是无效的。

但是，后台的访问量不大，都是自己人使用，不支持分布式也没啥关系。

如果您一定要用分布式部署后台，需要您自己二次开发一下了。


### 数据库存储, 搜索引擎

一般用分布式php，都是流量比较大，可以将默认的mysql services存储，改成mongodb services存储，mongodb作为nosql数据库，并发数
比mysql提高一个数量级，
安装一下mongodb，后台配置一下services即可


[Fecmall-Service数据库配置](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecshop-2-service-database.html)

[Fecmall-使用Mongodb](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecshop-2-use-mongo.html)


搜索部分，您可以使用xunsearch，如果流量变大，可以使用elasticSearch搜索工具，提高并发。

[Fecmall-搜索引擎配置](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecshop-2-search-engine.html)

### 其他

然后设置fecmall访问相应的`mysql mongodb`即可
，mysql如果访问量达可以做分库分表，mongodb可以做复制集, 等等


[详解yii2实现分库分表的方案与思路](http://www.fecshop.com/topic/645)

对于mysql分库分表处理，一边是为了应用  高并发读和高并发写同时存在的表，
譬如订单表，购物车表，
但由于购物车对数据严格要求低，可以用redis来解决，对于强事务的订单表，可以用分库分表解决（一般网站没有那么多订单，
用上这个的，基本都是一天几千单设置万单以上的电商商城）












