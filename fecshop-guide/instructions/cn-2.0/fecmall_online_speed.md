Fecmall 性能问题
===============


Fecmall性能Ab压测：http://www.fecmall.com/topic/1573

### 硬件配置

硬件配置当然是越快越好，内存越大越好，这个没得说哈，内存一定要够用。

内存够大，cpu够多，够快

数据库硬盘尽量用SSD，加快读写


### 环境配置

1.php配置，php细节配置参数很多，有很多根据服务器情况的设置和优化


[PHP-FPM进程数的设定](http://www.fecshop.com/topic/459)

开启`Opcache`，参考：[php 安装 zend opcache](http://www.fancyecommerce.com/2016/09/24/php-%E5%AE%89%E8%A3%85-zend-opcace/)

使用php7，最近新出的php7.2引入的JIT，
比php7.1提升了10%的性能，

php7的优化：[让PHP7达到最高性能的几个Tips](http://www.laruence.com/2015/12/04/3086.html)

等等

2.Mysql配置优化

2.1、`mysql` 的配置文件参数优化

2.2、有时候，程序员写代码在对象的生成调用，没有写类变量保存中间结果，造成
每次调用方法都是去数据库查询，造成相同的sql执行多次的情况，
对于这类的问题的排查，最好的方式是在本地机，访问某个前端页面，打印mysql执行
的sql语句，查看sql语句是否存在问题，另外对于线上，可以把mysql的慢查询日志打印出来。

打印sql语言的方法  [mysql 将执行的所有sql语句，输出到log日志（写入log日志）, 以及将慢查询sql输出到日志文件](http://www.fecshop.com/topic/835)

2.3、对于mysql的操作，`增删改查`，对于`查询`，我们可以通过`慢查询日志`将其打印出来，
但是对于`增删改`, 如果执行慢，一般都是锁的问题，也就是尽量的使用到行锁。

因此，对于mysql，尽量用innodb，支持行锁，但是，innode使用行锁还是使用表锁，
是有条件的，是基于索引的。

譬如 update customer set age = 19 where name = 'terry'

如果 customer表的name字段有索引，那么就会使用行锁，锁的行就是name = 'terry'，
也就是 name = 'terry'的数据有多少行，就会锁多少行的数据，
如果customer表的所有数据行的name的值都是terry，那么就会锁所有的行，
因此，就相当于表锁了，因此，如果name字段没有加索引，那么就相当于锁住所有的行，
那么就是表锁了，对于update操作，如果where条件存在多个字段的条件查询，不一定所有的所有的列都加
索引，如果where条件是三个字段，而索引只有2个字段，那么就会锁住这两个字段命中的数据行，
因此根据实际情况做好索引，除了可以优化查询，对于update更新同样重要，
update 的where条件中的字段索引命中的数据行越少，锁的数据行就越少

其他的关于表锁的，可以参看:http://www.fecshop.com/topic/283

2.4另外，对于自己开发的功能，有的功能可以使用乐观锁：

关于Yii2的乐观锁和悲观锁可以参看：http://www.digpage.com/lock.html

2.5【闲谈】 有一些系统，可以被拆成多个子系统，通过api对接，
各个api的方法要满足幂等性，譬如：http://www.fecshop.com/topic/534
，通过程序的方式来控制回滚，上面的这个文章有一个大致的介绍，有兴趣的可以读读，
由于这块我了解的也只限于理论层面（和java架构师聊的知识），没有具体操作过，
因此，有兴趣您看看就好。



3.Mongodb配置优化

资料：[关于php mongodb的最大连接数](http://www.fecshop.com/topic/445)

将mysql service改为mongodb servies，使用高并发的mongodb替代mysql，增强并发。

注：上面的配置参数的优化，首先要了解相应的配置参数的含义，
然后根据具体情况做优化配置，譬如，机器内存36G，那么可以把
php的进程数设置多一些。

### Fecmall生产环境配置优化

1.asset设置

1.1关闭`forceCopy`

对于需要css的端口  appfront 和apphtml5，打开 `@app/config/fecshop_local_services/Page.php`
，设置：


```
'forceCopy' => false,

```

关闭后，如果更新js和css信息，您需要去`@app/web/assets` 下面手动清空
``assets文件，清空后，Yii2的下次访问会自动复制最近的js和css文件

当然，如果你的网站访问量不大，开启也是可以的，更新js和css会方便一些，不需要去`@app/web/assets `下面手动清空

1.2 更新js和css后，更新版本号

更新版本号的方式参看[Fecmall theme js and css](http://www.fecshop.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-js-css.html#jscss)
, 这篇文章的 `js和css 浏览器缓存和版本` 部分

这样js和css更新后，会强制浏览器加载最新的js和css文件，
而不是去使用浏览器缓存。

1.3 使用cdn

参看[Fecmall theme js and css](http://www.fecshop.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-js-css.html#jscss)

2.config优化，开启单文件配置

fecmall的配置最终是由N个配置`php文件`合并而成，
在每次初始化 前执行，为了加速，可以先把配置文件合并成单文件，
然后加载这个合并成的单配置文件，就会比较节省资源，加快速度。

设置：在入口文件`@app/web/index.php` 代码： `$use_merge_config_file = false;` 处设置。
`true` 代表打开，`false`代表关闭


打开配置加速开关前，您需要先生成单配置文件。
您需要执行 http://www.domain.com/index-merge-config.php 进行生成单文件配置数组。
注意：打开后，当您修改了配置，
都需要重新生成单文件配置数组，否则修改的配置不会生效,。

建议：

```
1.本地开发环境关闭，开发环境如果访问量不大，关闭也行，
如果访问量大，建议打开

2.http://www.domain.com/index-merge-config.php是访问执行，因此，
我们希望只能由我们自己人执行，因此，

2.1.您可以把这个`index-merge-config.php`文件的名字改一下，改成 `fdad78fds7fds7fds8.php` ，只有自己人
知道的文件路径

2.2在nginx上面对这个文件访问做一下密码控制，详细参看：
[nginx 某个目录访问设置账户密码访问](http://www.fecshop.com/topic/407)
```

3.开启缓存

fecmall的缓存分为局部缓存和全页缓存，使用的是yii2的机制，

开启缓存可以加速，详细参看：
[fecmall cache](fecmall_cache.md)


4.浏览器加载加速

> fecmall已经遵循下面的优化方式，如果您开发了新的模块，建议也这样，加快浏览器页面
的渲染。

4.1 js部分

fecmall的css放到html页面的头部，js放到页面的底部，这样可以让浏览器
快速加载

4.2 js和css 链接url用独立的域名
，`图片链接url`用独立的域名，使用独立域名的好处，可以参看文章：
[网站的图片，css，js 为什么要和网站的域名不一样](http://www.fancyecommerce.com/2017/04/17/%E7%BD%91%E7%AB%99%E7%9A%84%E5%9B%BE%E7%89%87%EF%BC%8Ccss%EF%BC%8Cjs-%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E5%92%8C%E7%BD%91%E7%AB%99%E7%9A%84%E5%9F%9F%E5%90%8D%E4%B8%8D%E4%B8%80%E6%A0%B7/)

5 扩展优化

可以使用`elasticSearch`，用于产品，分类，搜索页查询，
目前fecmall不支持用`elasticSearch`，可以自己扩展。


6 `mysql`  `mongodb` 设置`慢查询`日志，把慢查询的语句找出来，定位到功能，
然后进行处理

7 nginx访问日志设置开始和结束时间，把`间隔时间`比较长的url找出来

8.services部分也可以开启日志，不过消耗比较大，可以短时间的开启，
查看各个`services`的各个方法执行消耗的时间。
具体实现可以参看文件 `@fecshop/services/Service.php`

9.如果访问量比较大，

9.1 数据库：可以把`mongodb`做复制集，`mysql`做主从复制

9.2 图片：图片可以放到`云库`，如果图片放到自己的服务器，可以通过`NFS`，将
图片服务器的磁盘挂载到`php服务器`的图片路径下，然后把域名指向图片服务器。

9.3 加几个php机器，`nginx`做负载均衡

9.4 `缓存`和`session` 放到`redis`服务器里面

这样各个层都是单独的服务器，分布式拆开，性能会提升很多。

最后，如果您开发了新模块，可以参看一下[Yii2的性能优化建议](http://www.yiichina.com/doc/guide/2.0/tutorial-performance-tuning)

### 采用fecmall官方插件提速

[Fecmall 官方扩展列表](http://www.fecshop.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-pkg-list.html)

10.对于appserver端，是给vue这类使用的，如果您的appserver域名和vue的域名不一样，
使用的是跨域名的方式，就会涉及到跨域问题
就会使用的cros来满足跨域，cros会在首次，以及访问过程中时不时的发送options
请求来获取是否可以访问内容（cros不了解的可以自己查询），
因此，对于options请求，在index.php部分直接返回，会更节省资源

@appserver/web/index.php 将头部注释去掉即可

```
<?php
/**
 * 【Appserver端性能优化】：如果vue和appserver是不一样的域名，对于这种跨域的前端和后端交互，需要cros机制，具体您可以自己查阅
 * 原理为：第一次发送options请求，如果请求成功，获取服务端允许的请求类型，然后再发起具体的数据请求
 * 对于options请求，不涉及到数据，因此直接返回即可，因此下面加了下面的代码
 * 对于下面的设置的允许的值，是fecshop目前允许的，如果您添加了其他的，请在下面自行修改
 * 下面的cros的信息要和 @fecshop/app/appserver/modules/AppserverTokenController.php 这个文件里面的设置要一致。
 * 默认，下面是注释掉，您可以根据自己的情况，取消掉下面的注释，让options请求在index.php文件执行的时候直接返回，节省资源。
 */ 
/*  !!!将这块代码的注释去掉，去掉前详细读完上面的注释
if ($_SERVER['REQUEST_METHOD'] == 'OPTIONS') {
    $cors_allow_headers = ['fecshop-uuid','fecshop-lang','fecshop-currency','access-token'];       
    header('Access-Control-Allow-Origin: *');
    header("Access-Control-Allow-Headers: Origin, X-Requested-With, Content-Type, Accept, ".implode(', ',$cors_allow_headers));
    header('Access-Control-Allow-Methods: GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS');
    exit;
}
*/
```



### 其他

等等，如果你有新的优化建议，可以在fecshop.com发帖，一起成长。

Terry对fecmall，开启opcache和fecmall缓存过程中的速度测试，参看：
[Fecmall 性能速度测试（测速）](http://www.fecshop.com/topic/1573)