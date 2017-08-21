搜索
============

> 对于搜索，目前使用了2种方式，对于外文，譬如法语，德语，西班牙语
> 都是用的mongodb的full Search ，但是mongodb的搜索不支持中文，
> 目前中文部分用的是xunsearch，对于中小网站都没啥问题，
> 后面会扩展用elasticSearch(目前还没有做)来做搜索工作。

### 安装xunsearch

http://www.fancyecommerce.com/2016/09/24/xunsearch-%e5%ae%89%e8%a3%85%ef%bc%8c%e4%bd%bf%e7%94%a8/

其他参考资料：

http://www.xunsearch.com/

https://getyii.com/topic/61

http://www.yiichina.com/code/661


### 搜索配置部分：

配置文件为：

fecshop的配置文件路径为： `@fecshop/config/services/Search.php`

用户可以在`@common/config/fecshop_local_services/Search.php` 
这里进行重写配置。

完整的配置如下：

```
return [
	'search' => [
		'class' => 'fecshop\services\Search',
		'filterAttr' => [
			'color','size', # 在搜索页面侧栏的搜索过滤属性字段
		],
		'childService' => [
			'mongoSearch' => [
				'class' 		=> 'fecshop\services\search\MongoSearch',
				'searchIndexConfig'  => [
					'name' => 10,  
					'description' => 5,  
				], 
				#more : https://docs.mongodb.com/manual/reference/text-search-languages/#text-search-languages
				'searchLang'  => [
					'en' => 'english',
					'fr' => 'french',
					'de' => 'german',
					'es' => 'spanish',
					'ru' => 'russian',
					'pt' => 'portuguese',
				],
			],
			'xunSearch'  => [
				'class' 		=> 'fecshop\services\search\XunSearch',
				'fuzzy' => true,  # 是否开启模糊查询
				'synonyms' => true, #是否开启同义词翻译
				'searchLang'    => [
					'zh' => 'chinese',
				],
			],
		],
	]
];
```

1.侧栏属性过滤

`filterAttr` : 在搜索页面侧栏显示的过滤属性，选择后在侧栏会显示该属性的过滤选项信息

2.mongodb配置 也就是配置数组里面 `mongoSearch`下面的配置。

`searchIndexConfig`为配置搜索的权重比，
上面的配置代表为：`name`的权重为10，`description`的权重为5.

`searchLang`为语言设置，因为搜索要涉及到分词，因此要和语言挂钩的，
对于mongodb的搜索，有一个语言的文字对应表，网址为：
https://docs.mongodb.com/manual/reference/text-search-languages/#text-search-languages
，您需要根据上面语言的名字，在这里配置各个语言的参数。譬如：法语配置，`fr`为语言二位简码，
在上面网址中法语的名字为：`french`,
因此在上面进行配置：`'fr' => 'french'`,

3.国产搜索软件`xunSearch`

xunSearch作者写了一个yii2的扩展，用于中文搜索，
因为mongodb是老外的玩意，不支持中文分词，因此，我用了比较小巧
的`xunSearch`，（当然专业的搜索工具还是`elasticSearch`），
关于语言的配置和上面大致一样，不过这里只设置中文就好了，如果您是
外贸网站，那么根本不需要使用xunsearch啦。

`xunSearch配置组件`：组件的配置文件：`fecshop/config/components/XunSearch.php`，
打开这个文件，你会发现：`'iniDirectory' => '@fecshop/config/xunsearch'`, 
也就是active record的配置，有点类似elasticSearch的`mapping`，
也就是数据model的配置文件的文件夹路径，我们进入@fecshop/config/xunsearch，
发现下面有search.ini文件，我们打开
`@fecshop/config/xunsearch/search.ini` 文件，这里是对search的一些配置，
具体语法可以参看http://www.xunsearch.com/ 查阅，这里不做讲解。
当然，如果您不想扩展fecshop的xunSearch搜索，你可以不需要明白这些，直接用就好。

对于`@fecshop/config/xunsearch/search.ini`中的配置，我们需要了解的是
`project.name = search`
， 这个和`fecshop\models\xunsearch\Search.php`里面的`projectName()`返回的名字一致即可。




### 数据同步到搜索工具中

通过上面，我们大致就设置完了，然后我们需要跑初始化脚本，
也就是将数据同步到我们的搜索工具中，需要跑的脚本为：
首先shell进入路径 @fecshop/shell/search ， 然后执行  sh fullSearchSync.sh
即可，跑完后，mongodb的搜索和xunSearch的搜索都把数据同步过去。

```
[root@iZ942k2d5ezZ search]# pwd
/www/web/develop/fecshop/vendor/fancyecommerce/fecshop/shell/search
[root@iZ942k2d5ezZ search]# sh fullSearchSync.sh 
There are 37 products to process
There are 1 pages to process
##############ALL BEGINING###############
Page 1 done
begin delete Mongodb Search Date 
##############ALL COMPLETE###############
[root@iZ942k2d5ezZ search]# 

```

### 去除某个搜索

如果您想去除某个搜索，譬如您是做跨境出口电商的，不想做中文，那么
可以去除xunsearch，您只需要在配置中加入一个` 'enable' => false`就可以了，
譬如：

```
return [
	'search' => [
		'class' => 'fecshop\services\Search',
		'filterAttr' => [
			'color','size', # 在搜索页面侧栏的搜索过滤属性字段
		],
		'childService' => [
			'mongoSearch' => [
				'class' 		=> 'fecshop\services\search\MongoSearch',
				'searchIndexConfig'  => [
					'name' => 10,  
					'description' => 5,  
				], 
				#more : https://docs.mongodb.com/manual/reference/text-search-languages/#text-search-languages
				'searchLang'  => [
					'en' => 'english',
					'fr' => 'french',
					'de' => 'german',
					'es' => 'spanish',
					'ru' => 'russian',
					'pt' => 'portuguese',
				],
			],
			'xunSearch'  => [
				'class' 		=> 'fecshop\services\search\XunSearch',
                'enable'        => false,
				'fuzzy' => true,  # 是否开启模糊查询
				'synonyms' => true, #是否开启同义词翻译
				'searchLang'    => [
					'zh' => 'chinese',
				],
			],
		],
	]
];
```

加入 `'enable'        => false,` 后，xunsearch将可不用。

因此，您可以打开文件：@common\config\fecshop_local_services\Search.php
加入 ` 'enable'        => false,`  即可。

```
'xunSearch'  => [
    'fuzzy'         => true,  // 是否开启模糊查询
    'enable'        => false,
    'synonyms'      => true, //是否开启同义词翻译
    'searchLang'    => [
        'zh' => 'chinese',
    ],
],
```


### 使用

在前台就可以使用搜索功能进行搜索了。




















