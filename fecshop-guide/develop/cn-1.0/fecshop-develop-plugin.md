Fecshop 插件开发
================

> 做插件，也就是做composer包，
> yii2 fecshop的代码都是以composer包的方式发布的
> ，您可以通过


### Fecshop插件的制作：

Fecshop插件是以composer包的方式制作，
开发一个扩展的步骤有点小麻烦，这里有详细的截图步骤：

[Yii2 – 如何写一个插件 ， 如何做一个扩展](http://www.fancyecommerce.com/2016/05/10/yii2-%E5%A6%82%E4%BD%95%E5%86%99%E4%B8%80%E4%B8%AA%E6%8F%92%E4%BB%B6-%EF%BC%8C-%E5%A6%82%E4%BD%95%E5%81%9A%E4%B8%80%E4%B8%AA%E6%89%A9%E5%B1%95/)

上面的步骤，就是做一个composer包，传到github中，并在composer中
发布，这样就可以通过composer加载过来了。

### 加载第三方发布的composer包，并配置。

通过下面的命令可以加载过来第三方发布的composer包,譬如：composer的：zqy234/terrytest包

```
composer require --prefer-dist zqy234/terrytest
```

第三方以composer包的方式发布的插件，
插件肯定有一些配置，通过一个入口配置文件，将其他的所有的配置文件
通过require方式加载过来，然后将这个入口文件放到
@app/web/index.php中。

```
$config = yii\helpers\ArrayHelper::merge(
		require(__DIR__ . '/../../common/config/main.php'),
		require(__DIR__ . '/../../common/config/main-local.php'),
		require(__DIR__ . '/../config/main.php'),
		require(__DIR__ . '/../config/main-local.php'),
		# fecshop services config
		require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/config/fecshop.php'),
		# fecshop module config
		require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/app/appfront/config/appfront.php'),
		
		# thrid part confing
		
		# common modules and services.
		require(__DIR__ . '/../../common/config/fecshop_local.php'),
		 
		# appadmin local modules and services.
		require(__DIR__ . '/../config/fecshop_local.php')
		
	);
```

放到注释 `# thrid part confing` 的下面部分。
就可以把插件的配置加载过来。注意顺序不要放错，因为
后面的配置文件的优先级高，会覆盖前面的配置。

**注意**：这里说的插件，其实就是一个composer的包，
fecshop  yii2 其实都是一个composer的包，
他们之间有依赖关系，如果有依赖，composer会以依赖的方式
把相应的包加载过来。


