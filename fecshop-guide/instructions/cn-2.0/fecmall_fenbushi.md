Fecmall分布式部署
============

>访问压力大，可以mysql，mongodb，php放到不同的主机上面，
多台php-fpm的方式部署。


多台php服务器，会涉及到如下的一些问题


### 图片问题

如果您使用的是云服务器，并且重写了fecmall图片部分的存储，这样处理可以解决

如果您不使用云服务器，可以自己搞一个图片服务器，然后通过linux NFS将
图片服务器的appimage映射到php服务器中fecmall目录下的appimage，
这个相当于内网服务器挂载，各个php服务器的appimage文件夹，都是挂载的图片服务器的appimage，
然后将图片域名解析到图片服务器，即可解决


### 缓存和session

fecmall的缓存和session存储在redis里面，因此此问题解决

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


这样，各个php实例的php将js和css发布到路径'/www/web/fecshop/jscss/appfront/assets'，但这个文件夹
是远程挂载过来的，实际是服务器的`A`文件夹，这样各个php的发布路径是同一个文件系统

对于页面加载js，域名会使用`baseUrl`设置的域名，而这个域名 `http://appfront.xxxx.com`解析到了远程服务器的`A`文件夹，因此可以访问到css和js文件。

4.如果使用`cdn`。那么，将css js  img复制到CDN服务器，得到相应的访问url


设置`baseUrl`为cdn的base url，然后fecshop就会加载设置后的css和js url

5.后台框架，是不支持fecshop的page assets services的，
因此 https://github.com/fecshop/yii2_fecshop/blob/master/services/page/Asset.php 对其是无效的。

另外后台的访问量不大，都是自己人使用，不支持分布式也没啥关系。


### 其他

然后设置fecmall访问相应的mysql mongodb即可
，mysql如果访问量达可以做分库分表，mongodb可以做复制集, 等等


[详解yii2实现分库分表的方案与思路](http://www.fecshop.com/topic/645)














