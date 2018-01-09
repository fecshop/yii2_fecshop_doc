Fecshop 2.Store初始化
==================

> 这里讲述的是在fecshop初始化的过程中，Store部分的初始化


Store ，关于Yii2框架的bootstrap知识
可以参看： [启动引导（Bootstrapping）](http://www.yiichina.com/doc/guide/2.0/runtime-bootstrapping)
，

Fecshop Store的初始化，就是利用Yii2的bootstrap机制，
打开@fecshop/app/appfront(apphtml5|appserver)/config/appfront.php(apphtml5.php|appserver.php)
, 可以看到配置

```
'bootstrap' => ['store'],
```

上面的意思代表：Yii2初始化的时候，执行store component，然后我们去找store component的配置

store组件的配置文件：`@fecshop/config/components/Store.php` ，可以看到如下配置

```
return [
	'store' => [
		'class' => 'fecshop\components\Store',
	],
];
```

在yii2初始化的时候，会执行store component class对应文件的booststrap()方法，
我们打开`fecshop\components\Store.php`,可以发现：


```
class Store extends Component implements BootstrapInterface
{
	public function bootstrap($app){
		Yii::$service->store->bootstrap($app);
    }
}
```

执行的 store service的bootstrap()方法(对于fecshop service的知识，详细参看：
[Fecshop 服务](fecshop-service-abc.md)

我们去找 store service的配置文件:`@fecshop\services\Store.php`，查看
`bootstrap()` 方法
，代码详细这里就不粘贴了，您可以自己查看，大致干了下面几件事情：

```
1.是否是api类型入口，如果是，则 `Yii::$app->user->enableSession = false;`
2.通过htmlUlr，获取当前的store key（在安装配置store的时候，各个store key就是去掉`http://`的域名）
3.通过配置获取stores，循环stores匹配当前的store key，匹配成功，则取出来相应的配置信息进行
初始化
3.1 设备检测，如果是手机web访问的pc网址，则跳转到html5页面
3.2 初始化store信息到store services
3.3 初始化语言信息
3.4 初始化当前模板
3.5 初始化货币
3.6 appserver入口的一些特殊的初始化的处理

```


到此，store的初始化部分就讲述完了。

> 关于Yii2 bootstrap引导过程更多的知识，您可以查看我的博文：[yii2 初始化的bootstrap过程 -引导](http://www.fancyecommerce.com/2016/05/18/yii2-%E5%88%9D%E5%A7%8B%E5%8C%96%E7%9A%84bootstrap%E8%BF%87%E7%A8%8B-%E5%BC%95%E5%AF%BC/)
