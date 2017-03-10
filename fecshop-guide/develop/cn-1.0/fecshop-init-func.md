Fecshop 功能初始化
==================

> 这里讲述的是在fecshop初始化的过程中，通过配置的方式嵌入到Yii2的初始化进程中
> 的部分功能。

1.Yii2初始化知识
-----------------

在入口文件index.php执行 

```
$application = new yii\web\Application($config);
$application->run();
```

Yii2的初始化就开始了，如果我们想让某个组件在初始化的时候就执行，
也就说，在该入口，任何一个页面的访问都会执行这个组件的bootstrap方法，我们可以通过配置的方式添加
到config中即可，譬如fecshop appfront入口在bootstrap中添加了store

```
'bootstrap' => ['store'],
```

store组件的配置为：

```
return [
	'store' => [
		'class' => 'fecshop\components\Store',
	],
];
```

`fecshop\components\Store`的代码如下，上面添加配置后，
会执行store组件的bootstrap方法，$app就是Yii::$app，

```
class Store extends Component implements BootstrapInterface
{
	
	public function bootstrap($app){
		Yii::$service->store->bootstrap($app);
		
    }
	
}
```

然后就会执行@fecshop\services\Store里面的bootstrap方法了，进行
store的初始化工作，具体的请查看具体代码

关于Yii2 bootstrap引导过程更多的知识，您可以查看我的博文：[yii2 初始化的bootstrap过程 -引导](http://www.fancyecommerce.com/2016/05/18/yii2-%E5%88%9D%E5%A7%8B%E5%8C%96%E7%9A%84bootstrap%E8%BF%87%E7%A8%8B-%E5%BC%95%E5%AF%BC/)

2.目前各个入口的bootstrap初始化添加
-----------------------------------



2.1 appfront 添加了store组件的初始化

`vendor/fancyecommerce/fecshop/app/appfront/config/appfront.php`

2.2 appadmin 目前没有添加初始化

2.3 apphtml5 添加了store组件的初始化（目前还没有完成该入口）

`vendor/fancyecommerce/fecshop/app/apphtml5/config/appfront.php`






























