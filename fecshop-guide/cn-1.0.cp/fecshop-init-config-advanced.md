Fecshop 配置
============

1、服务的配置：

@fecshop\config\services\ 文件夹下面是对服务的配置

譬如cms服务：

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

给cms service 添加子服务，譬如上面
给cms服务添加一个article子服务。


2、组件的配置：

`@fecshop\config\component\`下面

里面是重写或者添加的一些组件


3、模块的配置：

`@fecshop\app\appXXX\config\modules` 下面。

4、本地配置

`@common\config\`

`@app\config\`

以上都是本地的一些配置，在这个路径下面，都会有

文件：fecsop_local.php， 

文件夹：fecshop_local_modules（配置本地模块） 和 fecshop_local_services
（配置本地服务）

5、详细

各个配置的详细作用，请在相应的文件中查看，每个配置项都
标注了其中的作用。











