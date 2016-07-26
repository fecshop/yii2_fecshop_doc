Fecshop Cms 服务
===============


1.Article 部分

cms服务的子服务，可以通过

```
Yii::$service->cms->article->XXXXX
```

调用article的方法。

文件路径为：@fecshop\services\cms\Article


配置为：

```
return [
	'cms' => [
		'class' => 'fecshop\services\Cms',
		
		# 子服务
		'childService' => [
			'article' => [
				'class' 			=> 'fecshop\services\cms\Article',
				'storage' => 'mysqldb', # mysqldb or mongodb.
			],
		],
	],
];
```

支持两种存储方式，mysqldb和mongodb，可以通过配置设置、

详细的类方法请到组件里面查看。




2.Static Block 部分
















