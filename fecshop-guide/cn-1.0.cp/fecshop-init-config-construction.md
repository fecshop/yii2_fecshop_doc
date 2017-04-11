Fecshop 配置结构
================

> Fecshop的配置是层层覆盖的方式，Fecshop代码部分的配置的优先级
> 最低，但是是最全面的，其次是第三方插件模板的配置，最高的是
> 本地路径。这样可以通过在高优先级的配置中添加配置，进而覆盖
> 底层的配置，来达到重写覆盖的目的。

### 配置覆盖的原理：

打开@app/web/index.php入口文件可以看到：

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

关于`yii\helpers\ArrayHelper::merge()` 函数，是将多维数组
合并，后面的数组覆盖前面的，关于这个数组的详细介绍
请参看文章：[yii2 关于helper类 ArrayHelper::merge（）方法的介绍](http://www.fancyecommerce.com/2016/07/02/yii2-%e5%85%b3%e4%ba%8ehelper%e7%b1%bb-arrayhelpermerge%ef%bc%88%ef%bc%89%e6%96%b9%e6%b3%95%e7%9a%84%e4%bb%8b%e7%bb%8d/)
以及[Yii2 一个隐藏的小坑，致使我的组件的bootstrap方法执行了多次。](http://www.fancyecommerce.com/2016/08/02/yii2-%e4%b8%80%e4%b8%aa%e9%9a%90%e8%97%8f%e7%9a%84%e5%b0%8f%e5%9d%91%ef%bc%8c%e8%87%b4%e4%bd%bf%e6%88%91%e7%9a%84%e7%bb%84%e4%bb%b6%e7%9a%84bootstrap%e6%96%b9%e6%b3%95%e6%89%a7%e8%a1%8c%e4%ba%86/)

总之，后面的数组会覆盖前面的配置，看到这个文件
我们就了解了fecshop的主体配置原理。

下面我们详细介绍一下（按照优先级，由低到高）：

1、yii2的基础配置：

`@common/config/main.php`

`@common/config/main-local.php`

`@app/config/main.php`

`@app/config/main.php`


yii2的框架配置的各个文件的大致作用为：（@app\config目录下的）

- bootstrap.php 这个是yii2初始化的配置文件，一般设置一些别名Alias。
- params-local.php 这个是参数配置文件，用户可以通过config取出数据使用，
这个文件里面的配置一般是本地配置，不会加入到svn版本控制里面。
- params.php  这个也是参数配置文件，功能和params-local.php一样，唯一的不同
在于这个文件会加入svn版本控制，测试和线上保持一致。
- main-local.php ,这个文件是yii2系统的配置文件，一般是本地的配置部分，是不加入svn的。
- main.php，这个文件也是yii2系统的配置文件，是要加入svn版本控制，测试和线上保持一致的，关于
里面的具体配置语法，可以去参看yii2的教程，这里不做详细叙述。



上面这几个是yii2的配置，关于配置请参看yii2文档：

yiiframe官网文档：[Yii2 Configurations ](http://www.yiiframework.com/doc-2.0/guide-concept-configurations.html#configuration-files)

yiichina中文文档：[Yii2 Configurations ](http://www.yiichina.com/doc/guide/2.0/concept-configurations)

2、Fecshop的服务配置（service）

文件在路径`@vendor/fancyecommerce/fecshop/config/`里面

fecshop.php 是入口配置，`/components`文件夹下面的是yii组件配置
，`/services`文件夹下面的是yii service 配置。

3、Fecshop 应用配置

文件路径在: `@vendor/fancyecommerce/fecshop/app/appXXX/config`

各个应用的config，配置的是当前应用的配置，内容为：
当前应用的配置和当前应用的模块配置。

4、第三方配置，

这里需要用户在下面的注释底部添加第三方插件或者模板的配置路径。

```
# thrid part confing
```

5、本地公共配置common

`@common/config/fecshop_local.php`，这个文件加载
`@common/config/fecshop_local_modules/`和
`@common/config/fecshop_local_services/`下的所有文件配置

本地模块和本地服务的**公用重写或添加**的配置都在这里添加

6、

`@app/config/fecshop_local.php`，这里添加的本应用（application）的配置
这里优先级别最高，可以覆盖其他的配置，
这个文件会加载
`@app/config/fecshop_local_modules/`和
`@app/config/fecshop_local_services/` 下的所有文件配置。

可以在这里添加或者重写上面的任何配置。


7、到这里，fecshop的配置结构就讲述完了。
在了解这些之前，您最好先了解好yii2，因为yii2是fecshop的基层
。











