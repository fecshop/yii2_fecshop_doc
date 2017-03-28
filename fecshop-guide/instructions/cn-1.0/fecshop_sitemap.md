Fecshop SiteMap
===============

> sitemap是为了方便搜索引擎蜘蛛爬取而生成的xml文件。

### 配置文件

配置文件为：`@fecshop/config/services/Sitemap.php`,您可以通过配置的方式
对该配置文件进行重写。

```
return [
	'sitemap' => [
		'class' => 'fecshop\services\Sitemap',
		'sitemapConfig' => [
			/**
			 * 对于下面的设置，您可能感觉很啰嗦，域名作为store的key，在store service中已经设置，
			 * 为什么需要在这里重新搞一套呢？  这样做是为了更加的灵活
			 *
			 */
			# appfront入口
			'appfront' => [
				# store的key(域名)，
				'fecshop.appfront.fancyecommerce.com' => [
					'https'			=> false,  # false代表使用http，true代表使用https			
					'sitemapDir' 	=> '@appfront/web/sitemap.xml', # sitemap存放的地址
					'showScriptName'=> true,	# 是否显示index.php ，譬如http://www.fecshop.com/index.php/xxxxxx,当nginx没有设置重写，这里需要设置为true,这样url中会存在index.php，否则会404
												# 这个设置对seo来说，设置为false最合适，也就是隐藏 url中index.php ，这种设置需要开启nginx的url重写
				],
				# store的key(域名)
				'fecshop.appfront.fancyecommerce.com/fr' => [
					'https'			=> false,  # false代表使用http，true代表使用https			
					'sitemapDir' 	=> '@appfront/web/fr/sitemap.xml', # sitemap存放的地址
					'showScriptName'=> true,
				],
				
				'fecshop.appfront.es.fancyecommerce.com' => [
					'https'			=> false,  # false代表使用http，true代表使用https			
					'sitemapDir' 	=> '@appfront/web/sitemap_es.xml',
					'showScriptName'=> true,
				],
				'fecshop.appfront.fancyecommerce.com/cn' => [
					'https'			=> false,  # false代表使用http，true代表使用https			
					'sitemapDir' 	=> '@appfront/web/sitemap_cn.xml',
					'showScriptName'=> true,
				],
			]
		],
	],
];
```
> 如果您的nginx重写没有开启，那么showScriptName需要设置成true，原因参看上面
> 配置里面的说明。

> 上面配置了4个store，(`fecshop.appfront.fancyecommerce.com`)
里面的各个配置项，在配置后面都有说明。

1.上面的store，就是您在各个入口下面的store，每一个store用不同的
域名或者后缀作为首页url，您可以这是pc入口，以及手机web入口，因为他们的
首页url不同，语言不同，进而内容不同，因此他们都需要有自己的sitemap文件。
每一个store配置里面都有sitemap的文件路径地址。




2.生成了sitemap.xml，我们需要通过首页域名+sitemap.xml作为访问路径。
如果在地址下面直接有对应名字的文件，则可以直接访问，但是名字是其他的名字，就需要nginx
设置了。譬如
`fecshop.appfront.es.fancyecommerce.com`生成的sitemap文件名字为
sitemap_es.xml，我们需要设置一下，让url
fecshop.appfront.es.fancyecommerce.com/sitemap.xml可以访问
到sitemap_es.xml


```
location ~ /sitemap.xml 
{   
	if ($host  ~ .*appfront.es.fancyecommerce.com) {  
		rewrite ^/sitemap\.xml /sitemap_es.xml last;  
	}
}
```

可以参看我的nginx的配置如下：

```
server {
    listen     80  ;
    server_name fecshop.appfront.fancyecommerce.com fecshop.appfront.es.fancyecommerce.com;
    root  /www/web/develop/fecshop/appfront/web;
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

        location ~ /sitemap.xml
        {
			if ($host  ~ .*appfront.es.fancyecommerce.com) {
					rewrite ^/sitemap\.xml /sitemap_es.xml last;
			}
        }
		
		 location /fr/ {
			index index.php;
			if (!-e $request_filename){
					rewrite . /fr/index.php last;
			}
        }
         location /es/ {
			index index.php;
			if (!-e $request_filename){
					rewrite . /es/index.php last;
			}
        }

         location /cn/ {
			index index.php;
			if (!-e $request_filename){
					rewrite . /cn/index.php last;
			}
        }

         location /de/ {
            index index.php;
			if (!-e $request_filename){
					rewrite . /de/index.php last;
			}
        }

        location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {
            expires      30d;
        }
		
		location ~ .*\.(js|css)?$ {
            expires      12h;
        }
        
}

		
		
		
```

通过上面的nginx配置

```
 location ~ /sitemap.xml
        {
			if ($host  ~ .*appfront.es.fancyecommerce.com) {
					rewrite ^/sitemap\.xml /sitemap_es.xml last;
			}
        }
```

fecshop.appfront.es.fancyecommerce.com/sitemap.xml 访问的文件
不是 /www/web/develop/fecshop/appfront/web/sitemap.xml
而是 /www/web/develop/fecshop/appfront/web/sitemap_es.xml
文件。

对于访问url中路径和名字与实际文件一致的，不需要在nginx做更改配置。


3.生成xml

通过上面，我们配置好了各个store的参数，我们就可以生成sitemap文件了

执行的shell文件为：`@fecshop/shell/sitemapGeneral.sh`

执行完了，就会在配置相应的地方生成对应的sitemap文件。















