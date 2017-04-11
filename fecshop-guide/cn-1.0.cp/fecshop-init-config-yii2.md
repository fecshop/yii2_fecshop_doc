Fecshop Yii2配置
================

> fecshop 是依托yii2而做的商城系统，因此很多地方需要按照
> yii2的语法进行配置

1、数据库配置：

对于mysql redis mongodb 请参看：
[fecshop 初始配置](http://www.fecshop.com/doc/fecshop-guide/cn-1.0/guide-fecshop-install.html#2-fecshop-app-advanced)


2、语言配置：

文件：`@appfront\config\main.php`

```
'i18n' => [
	'translations' => [
		'appfront' => [
			'basePaths' => [
				'@appfront/languages',
			],
			'sourceLanguage' => 'en_US', # 如果 en_US 也想翻译，那么可以改成en_XX。
		],
	],
],
```

i18n功能已经被重写，在`@fecshop\app\appfront\config\appfront.php`中可以看到

```
'i18n' => [
	'translations' => [
		'appfront' => [
			//'class' => 'yii\i18n\PhpMessageSource',
			'class' => 'fecshop\yii\i18n\PhpMessageSource',
			'basePaths' => [
				'@fecshop/app/appfront/languages',
			],
		],
	],
],
```

其中 `@appfront\config\main.php`配置的 '@appfront/languages'下的
翻译文件会覆盖 `@fecshop\app\appfront\config\appfront.php` 中配置的
'@fecshop/app/appfront/languages',
也就是说，如果含有相同的数组key，则上面的配置会覆盖下面的配置。

[fecshop 多语言介绍](fecshop-feature-mutil-languages.md)

在配置的路径下面您会发现相应语言的文件夹，譬如：
`@appfront\languages\`下面有`de_DE`,`en_US`,`zh_CN`
这个相应语言里面添加配置。

3、Asset配置：

```
'assetManager' => [
	'forceCopy' => true,
],
```

yii2的asset，大致就是将库包中的js css img 复制到
@app/web/asset下面，如果将`forceCopy`设置为false，
在初始化的时候会检查文件是否存在，如果不存在则发布文件到
assets下面，如果存在，则不复制，
如果将`forceCopy`设置为true，则每次刷新页面的时候
都会强制复制，在开发环境，将`forceCopy`设置为true，
在线上将`forceCopy`设置为false，
线上如果要更新js和css ，可以删除asset下面的所有文件，
yii2在初始化的时候发现没有文件，会复制过去文件。

4、如何将开发环境的debug去掉？

在@app\config\main-local.php处，将下面代码去掉：

```
if (YII_ENV_DEV) {
    // configuration adjustments for 'dev' environment
    $config['bootstrap'][] = 'debug';
    $config['modules']['debug'] = 'yii\debug\Module';

    $config['bootstrap'][] = 'gii';
    $config['modules']['gii'] = 'yii\gii\Module';
}
```

将index.php的代码：
```
defined('YII_DEBUG') or define('YII_DEBUG', true);
defined('YII_ENV') or define('YII_ENV', 'dev');
```
改成：

```
defined('YII_DEBUG') or define('YII_DEBUG', false);
defined('YII_ENV') or define('YII_ENV', 'prod');
```

5、重写404页面：

```
'errorHandler' => [
	'errorAction' => 'site/helper/error',
],
```

您可以将`errorAction` 改成其他的。
如果制作一个404页面参看：[Yii2 如何制作一个404页面](http://www.fancyecommerce.com/2016/08/04/yii2-%e5%88%b6%e4%bd%9c%e4%b8%80%e4%b8%aa404%e9%a1%b5%e9%9d%a2/)

6、设置首页：

```
'urlManager' => [
	'rules' => [
		'' => 'cms/home/index',
	],
],
```
上面的代码是：`@fecshop\app\appfront\config\appfront.php`
中的配置，如果您想更改首页到另外一个路由，譬如/xx/yy/zz
可以在`@app\config\main.php`或者其他文件的组件配置中添加


```
'urlManager' => [
	'rules' => [
		'' => 'xx/yy/zz',
	],
],
```

就会被更改。

7、Request
为了Url自定义的需要，fecshop已经重写了yii2的Request，不要轻易
重写配置

```
'request' => [
	'class' => 'fecshop\yii\web\Request',
],
```


8、其他的，需要多看yii2 framework的文档

[yii2 文档地址](http://www.yiiframework.com/doc-2.0/guide-index.html)





















