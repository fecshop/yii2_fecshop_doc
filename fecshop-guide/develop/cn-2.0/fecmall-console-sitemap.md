fecmall sitemap:生成的脚本
=========================

> 将 homeUrl，产品，分类，cmsPage等页面写入到sitemap文件的脚本

### 关于sitemap

sitemap是网站url字典，这个是为了方便搜索引擎爬取网站的信息，生成sitemap.xml

### 配置

配置文件： `@console/config/fecshop_local_services/Sitemap.php`

```
<?php
/**
 * FecShop file.
 * 
 * @link http://www.fecshop.com/
 *
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
return [
    'sitemap' => [
        'class'         => 'fecshop\services\Sitemap',
        'sitemapConfig' => [
            /*
             * 对于下面的设置，您可能感觉很啰嗦，域名作为store的key，在store service中已经设置，
             * 为什么需要在这里重新搞一套呢？  这样做是为了更加的灵活
             *
             */
            // appfront入口
            'appfront' => [
                // store的key(域名)，
                'fecshop.appfront.fancyecommerce.com' => [
                    'https'            => true,  // false代表使用http，true代表使用https
                    'sitemapDir'       => '@appfront/web/sitemap.xml', // sitemap存放的地址
                    'showScriptName'   => false,    // 是否显示index.php ，譬如http://www.fecshop.com/index.php/xxxxxx,当nginx没有设置重写，这里需要设置为true,这样url中会存在index.php，否则会404
                                                // 这个设置对seo来说，设置为false最合适，也就是隐藏 url中index.php ，这种设置需要开启nginx的url重写
                ],
                // store的key(域名)
                'fecshop.appfront.fancyecommerce.com/fr' => [
                    'https'            => true,  // false代表使用http，true代表使用https
                    'sitemapDir'       => '@appfront/web/fr/sitemap.xml', // sitemap存放的地址
                    'showScriptName'   => false,
                ],

                'fecshop.appfront.es.fancyecommerce.com' => [
                    'https'            => true,  // false代表使用http，true代表使用https
                    'sitemapDir'       => '@appfront/web/sitemap_es.xml',
                    'showScriptName'   => false,
                ],
                'fecshop.appfront.fancyecommerce.com/cn' => [
                    'https'            => true,  // false代表使用http，true代表使用https
                    'sitemapDir'       => '@appfront/web/cn/sitemap.xml',
                    'showScriptName'   => false,
                ],
            ],
        ],
    ],
];
```

`sitemapDir`: 生成的sitemap.xml的文件路径，您必须在操作前创建这个文件相应的文件夹路径

### 执行脚本

```
cd vendor/fancyecommerce/fecshop/shell
sh sitemapGeneral.sh
```

执行的log：

```
[root@iZ942k2d5ezZ shell]# sh sitemapGeneral.sh 
begin xml code
add home url to sitemap xml
add category url to sitemap xml
There are 1 page category to process
Page 1 done
add product url to sitemap xml
There are 1 page product to process
Page 1 done
add cms page url to sitemap xml
There are 1 page product to process
Page 1 done
end xml code
end success
[root@iZ942k2d5ezZ shell]# 

```

执行脚本后，将会生成相应的sitemap的xml文件

### nginx 配置

> sitemap.xml 默认的路径为  http://www.domain.com/sitemap.xml ，因此
> 各个store的域名+'/sitemap.xml' ，要保证可以访问到相应的sitemap文件，因此
> 需要做设置.

对于store `fecshop.appfront.fancyecommerce.com` 和
`fecshop.appfront.es.fancyecommerce.com`,index.php文件都是
`@appfront/web/index.php` , 我们生成了连个不同名字的xml文件
```
@appfront/web/sitemap.xml
@appfront/web/sitemap_es.xml
```

但是我们想让fecshop.appfront.es.fancyecommerce.com/sitemap.xml
访问的是`@appfront/web/sitemap_es.xml`
，这需要在nginx中做设置：

```
    location ~ /sitemap.xml
    {
        if ($host  ~ .*appfront.es.fancyecommerce.com) {
            rewrite ^/sitemap\.xml /sitemap_es.xml last;
        }
    }
```

