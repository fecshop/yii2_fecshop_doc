Fecmall xunsearch自定义search.ini
===================


### 配置文件search.ini文件的配置解读

fecmall xunsearch 配置文件search.ini文件为： @fecshop/config/xunsearch/search.ini

内容如下：

```
project.name = search
project.default_charset = UTF-8
;服务端用默认值
server.index = xunsearch:8383
server.search = xunsearch:8384
 
[_id]
type = id
 
[name]
type = title

[description]
type = body
 
[sku]
type = string
index = mixed

[spu]
type = string
index = mixed

[score]
type = numeric
index = none

[url_key]
type = string
index = none

[price]
type = numeric
index = none

[cost_price]
type = numeric
index = none

[special_price]
type = numeric
index = none

[special_from]
type = numeric
index = none

[special_to]
type = numeric
index = none

[final_price]
type = numeric
index = self

[image]
type = string
index = none

[short_description]
type = string
index = none

[created_at]
type = numeric
index = none

[sync_updated_at]
type = numeric
index = none

[color]
type = string
index = self 

[size]
type = string
index = self 
 
```

`project.name = search`: xunsearch的库名

`project.default_charset = UTF-8`： 编码

`server.index = xunsearch:8383`: 这个是xunsearch Index的host和端口，`xunsearch` 代表是host，这里可以填写ip，也可以填写host名称（在/etc/hosts中添加ip映射即可），`8383`是端口`port`

`server.search = xunsearch:8384`: 这个是xunsearch Search的host和端口，`xunsearch` 代表是host，这里可以填写ip，也可以填写host名称（在/etc/hosts中添加ip映射即可），`8384`是端口`port`

对于上面的配置ip，配置的是xunsearch, 需要添加host映射

vi /etc/hosts,添加下面的内容

```
127.0.0.1  xunsearch
```


### 如何自定义search.ini 配置文件



对于fecmall的配置，打开文件 @fecshop/config/components/xunSearch.php 可以看到

```
return [
    'xunsearch' => [
        'class' => 'hightman\xunsearch\Connection', // 此行必须
        'iniDirectory' => '@fecshop/config/xunsearch',    // 搜索 ini 文件目录，默认：@vendor/hightman/xunsearch/app
        'charset' => 'utf-8',   // 指定项目使用的默认编码，默认即时 utf-8，可不指定
    ],
```



`iniDirectory` 指明init文件路径为：`@fecshop/config/xunsearch`，进入这个文件夹可以发现文件
`@fecshop/config/xunsearch/search.ini` ， 


关于`search.ini`的内容以及解读参看：http://www.fecshop.com/topic/1504



这个是fecmall的对于xunsearch的配置文件，如果你想要自定义，那么，在本地config文件重写这个xunsearch components配置

譬如新建文件  @common/config/xunsearch/search.ini，然后在配置文件 @common/config/fecshop_local.php文件中添加配置

在return数组中添加 xunsearch components的配置，这个会覆盖fecshop的默认配置

```
return [
    'modules'  => $modules,
    'services' => $services,
    'components' => [
        'xunsearch' => [
            'iniDirectory' => '@common/config/xunsearch',    // 搜索 ini 文件目录，默认：@vendor/hightman/xunsearch/app
        ],
    ]
];
```

然后在文件 @common/config/xunsearch/search.ini 中添加你的xunsearch配置就可以了。


























