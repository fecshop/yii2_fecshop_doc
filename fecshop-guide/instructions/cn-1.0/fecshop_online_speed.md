Fecshop 性能问题
===============

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

`mysql` 的配置文件参数优化

3.Mongodb配置优化

资料：[关于php mongodb的最大连接数](http://www.fecshop.com/topic/445)


注：上面的配置参数的优化，首先要了解相应的配置参数的含义，
然后根据具体情况做优化配置，譬如，机器内存36G，那么可以把
php的进程数设置多一些。

### Fecshop生产环境配置优化

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

更新版本号的方式参看[Fecshop theme js and css](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-js-css.html#jscss)
, 这篇文章的 `js和css 浏览器缓存和版本` 部分

这样js和css更新后，会强制浏览器加载最新的js和css文件，
而不是去使用浏览器缓存。

1.3 使用cdn

参看[Fecshop theme js and css](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-js-css.html#jscss)

2.config优化，开启单文件配置

fecshop的配置最终是由N个配置`php文件`合并而成，
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

fecshop的缓存分为局部缓存和全页缓存，使用的是yii2的机制，

开启缓存可以加速，详细参看：
[fecshop cache](fecshop_cache.md)


4.浏览器加载加速

> fecshop已经遵循下面的优化方式，如果您开发了新的模块，建议也这样，加快浏览器页面
的渲染。

4.1 js部分

fecshop的css放到html页面的头部，js放到页面的底部，这样可以让浏览器
快速加载

4.2 js和css 链接url用独立的域名
，`图片链接url`用独立的域名，使用独立域名的好处，可以参看文章：
[网站的图片，css，js 为什么要和网站的域名不一样](http://www.fancyecommerce.com/2017/04/17/%E7%BD%91%E7%AB%99%E7%9A%84%E5%9B%BE%E7%89%87%EF%BC%8Ccss%EF%BC%8Cjs-%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E5%92%8C%E7%BD%91%E7%AB%99%E7%9A%84%E5%9F%9F%E5%90%8D%E4%B8%8D%E4%B8%80%E6%A0%B7/)

5 扩展优化

可以使用`elasticSearch`，用于产品，分类，搜索页查询，
目前fecshop不支持用`elasticSearch`，可以自己扩展。


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

### 采用fecshop官方插件提速

[Fecshop 官方扩展列表](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-pkg-list.html)


### 其他

等等，如果你有新的优化建议，可以在fecshop.com发帖。
