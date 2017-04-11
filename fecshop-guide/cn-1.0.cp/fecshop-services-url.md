Fecshop Url 服务。
================


1.得到当前的url

`Yii::$service->Url->getCurrentUrl()`

2.生成，并保存重写url

`Yii::$service->Url->saveRewriteUrlKeyByStr($str,$originUrl,$originUrlKey,$type='system')`

通过传递 字符串，和原来的url，重写后的url(这个可以为空，如果为空，会由字符串生成)。
生成并保存重写后的url到url_rewrite.

3.删除重写url

`Yii::$service->Url->removeRewriteUrlKey($url_key)`

$url_key 为重写后的url（自定义url）。

4.通过重写后的url得到原来的url

`Yii::$service->Url->getOriginUrl($urlKey)`

5.通过path得到url

`Yii::$service->Url->getUrlByPath($path,$https=false)`

6.得到当前的url的base部分

`Yii::$service->Url->getCurrentBaseUrl()`

7.得到首页url

`Yii::$service->Url->homeUrl()`



配置：

```
return [
	'url' => [
		'class' 	=> 'fecshop\services\Url',
		'randomCount'=> 8,  # if url key  is exist in url write table ,  add a random string  behide the url key, this param is define random String length
		# 子服务
		'childService' => [
			'rewrite' => [
				'class' => 'fecshop\services\url\Rewrite',
				'storage' => 'mysqldb',
			],
		],
	],
];
```

`randomCount`：随机字符串个数。

`storage` ：设置存储的数据库，可以选择mysqldb和mongodb
















