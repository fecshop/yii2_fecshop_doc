Fecshop 404页
=============

> 当一些url，找不到相应的controller，就会进入404页面，状态码为404，

404页面，使用的是Yii的 errorHandler组件，fecshop在配置文件
`@fecshop/app/appfront/config/appfront.php`中进行的配置。

```
'errorHandler' => [
		'errorAction' => 'site/helper/error',
	],
		
```

模板路径为：`@fecshop/app/appfront/theme/base/front/site/helper/error.php`
		
如果您想重写404页面，通过多模板重写的方式即可。








