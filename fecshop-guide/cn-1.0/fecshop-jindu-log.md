Fecshop 开发LOG
===========


- 2016-08-04 **【未完成】 完善 安装与配置 文档


- 2016-08-04 **【未完成】 做一个手机web home 页面：

- 2016-08-04 **【未完成】 appfront 建立error页面：

- 2016-08-04 **【未完成】 细化初始配置，需要填步骤：

1. 通过composer update 安装依赖库包
2. ./init 初始化
3. nginx配置路径指向
4. 配置store的域名设置 `@app\config\fecshop_local_services\Store.php`
5. 配置mysql  mongodb  redis等 `@common\config\main-local.php`
6. 配置语言：`@app\config\fecshop_local_services\FecshopLang.php`
7. 配置货币：`@app\config\fecshop_local_services\Page.php`
8. 如果是开发环境，需要assets每次都复制文件都web路径下面，则不需要编辑，
@app\config\main.php:

```
'assetManager' => [
			//'forceCopy' => true,
		],
```
如果是线上， 将forceCopy设置成false `['forceCopy' => false]`

9. 如果想要修改模板，则需要设置当前store模板路径。
10. 通过rewrite 去除掉url中的index
首先需要在nginx 或者apache中设置，下面是nginx的设置：

```
server {
    listen     80  ;
    server_name www.fecshop.com;
    root  /www/web/online-2/www.fecshop.com/appfront/web;
    server_tokens off;
    include none.conf;
    index index.php index.html index.htm;
    access_log /www/web_logs/access.log wwwlogs;
    error_log  /www/web_logs/error.log  notice;
    location ~ \.php$ {
		fastcgi_pass   127.0.0.1:9000;
		fastcgi_index  index.php;
		include fcgi.conf;
	}

	location /en/ {
        index index.php;
        if (!-e $request_filename){
            rewrite . /en/index.php last;
        }
    }

	location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {
			expires      30d;
	}

	location ~ .*\.(js|css)?$ {
			expires      12h;
	}
	location /api {
			rewrite /api/([a-z][0-9a-z_]+)/?$ /api.php?type=$1;
	 }


}
```

注意，如果设置的域名为： www.xxx.com/en ，则必须添加

```
location /en/ {
        index index.php;
        if (!-e $request_filename){
            rewrite . /en/index.php last;
        }
    }
```

关于apache的配置，请自行百度

11. 开启网站去除index.php的设置：

11.1 后台使用的是yii2的urlManager，

因此：

```
'urlManager' => [
	'class' => 'yii\web\UrlManager',
	'enablePrettyUrl' => true,
	'showScriptName' => false,
	'rules' => [
	],
],
```

即可。

对于多模板的前台，appfront  apphtml5  appserver
使用的是：

12 如果是开发环境， 在common中将forceCopy 设置为true
'assetManager' => [
	'forceCopy' => true,
],




















- 2016-08-03 **【已完成】验证：
http://fecshop.appfront.fancyecommerce.com/fr/fashion-hand-bag-for-women22
http://fecshop.appfront.fancyecommerce.com/fashion-hand-bag-for-women22
http://fecshop.appfront.es.fancyecommerce.com/fashion-hand-bag-for-women22
http://fecshop.appfront.fancyecommerce.com/cn/fashion-hand-bag-for-women22
几种域名模式下是否正常。

- 2016-08-03 **【已完成】** 把service的所有对外部提供访问的函数，由public 改成protected ，
然后，改成通过__call函数中转访问各个service的方法，可以通过log
在数据库保存，直接页面打印，通过参数打印等多种方式输出log。


- 2016-08-01 **【未完成】** 做一个fecshop的网站，略粗。


- 2016-07-31 **【已完成】** 调整 url  包括url服务以及fec\helpers\CUrl

- 2016-07-31 **【已完成】** fecshop的框架搭建 和 composer安装fecshop。






