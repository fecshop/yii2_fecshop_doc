Fecshop 关于服务
=================

> fecshop服务是一个公用性的底层，为各个应用系统提供底层服务

1.原则约定
----------

各个“应用系统”，譬如appfront，appadmin，apphtml5，是一个独立的文件结构
，他们都有独立的模块，里面有controller（控制层） block（数据中间逻辑处理层） theme（模板view层）
，但是没有model层，在原则上约定，各个“应用系统”不能直接访问model，
只能访问Fecshop Service（服务），来进行数据的获取和处理工作，然后由service层
访问model层进行数据的获取处理等工作。


2.服务层的功能粒度：
------------------

首先，对于model层的函数粒度，对应的是数据的操作，譬如更改某一行数据，添加一行数据等，这个地球人都知道。

对于service层的函数粒度，一般是我们语言描述需求的最小粒度，譬如：把一个产品加入购物车，
删除购物车的某个产品，调出某个分类下的产品，登录用户，计算产品的最终价格，等等，对于上面的这些最小的
语言描述粒度，会在服务层实现，然后直接访问该服务中的方法即可。

3.实现原理
---------

3.1 实例化过程：

当我们执行 `Yii::$service->cart`，就会访问fecshop cart service 服务
，对应文件 `@fecshop/services/Cart.php`
当执行`Yii::$service->cart->coupon` 就会访问 cart的子服务coupon
，对应文件 `@fecshop/services/cart/Coupon.php`

下面是实现原理：

在index.php入口文件中可以看到如下代码：

```
new fecshop\services\Application($config['services']);
unset($config['services']);
```

查看 fecshop\services\Application.php的代码如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
namespace fecshop\services;
use Yii;
use yii\base\Component;
use yii\base\InvalidConfigException;
/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class Application
{
	public $childService;
	public $_childService;
	
	
	public function __construct($config = [])
    {
        Yii::$service 		= $this;
        $this->childService = $config;
    }
	/**
	 * 得到services 里面配置的子服务childService的实例
	 */
	public function getChildService($childServiceName){
		if(!$this->_childService[$childServiceName]){
			$childService = $this->childService;
			if(isset($childService[$childServiceName])){
				$service = $childService[$childServiceName];
				$this->_childService[$childServiceName] = Yii::createObject($service);
			}else{
				throw new InvalidConfigException('Child Service ['.$childServiceName.'] is not find in '.get_called_class().', you must config it! ');
			}
		}
		return $this->_childService[$childServiceName];
	}
	
	/**
	 * 
	 */
	public function __get($attr){
		return $this->getChildService($attr);
		
	}
	
}
```


service配置，譬如：@fecshop\config\services\Cart.php

```
<?php
/**
 * FecShop file.
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
return [
	'cart' => [
		'class' => 'fecshop\services\Cart',
		
		# 子服务
		'childService' => [
			'quote' => [
				'class' => 'fecshop\services\cart\Quote',
			],
			'quoteItem' => [
				'class' => 'fecshop\services\cart\QuoteItem',
			],
			
			'info' => [
				'class' => 'fecshop\services\cart\Info',
				/**
				 * 单个sku加入购物车的最大个数。
				 */
				'maxCountAddToCart' => 100,
				# 上架状态产品加入购物车时，
				# 如果addToCartCheckSkuQty设置为true，则需要检查产品qty是否>购买qty，
				# 如果设置为false，则不需要，也就是说产品库存qty小于购买qty，也是可以加入购物车的。
				'addToCartCheckSkuQty' => true,
			],
			'coupon' => [
				'class' => 'fecshop\services\cart\Coupon',
			],
		],
	],
];
```

Yii::$service->cart 就是cart服务

Yii::$service 对应的是 fecshop\services\Application
当执行Yii::$service->cart时，找不到cart变量就会执行 __get()魔术方法，进而执行
getChildService(),将上面cart配置的class对应的文件`fecshop\services\Cart`，
进行实例化，也就是说 Yii::$service->cart 对应的是 fecshop\services\Cart 实例化的对象，
如果下次使用 Yii::$service->cart ，不会再实例化对象，FecShop Service是单例模式。

Fecshop子服务：Yii::$service->cart->coupon，通过上面的配置，会实例化
`fecshop\services\cart\Coupon`，子服务的原理和服务类似，都是单例模式。

3.2 关于service类

上面讲解了
Yii::$service->cart，如何找到 fecshop\services\Cart的步骤，下面详细讲述
service类。

所有的服务类，譬如上面说的cart服务，都必须继承
`@fecshop\services\Service`。
里面的方法都必须以action开头（如果不以action开头，而是实际的方法，那么
将方法声明为public ，也是可以访问的，但是这种方式不会经过上面提到的魔术方法，
因此，是无法记录该方法
的开始和结束时间），和controller中类似，
譬如执行  `Yii::$service->cart->addProductToCart($item)`，对应的是
fecshop\services\Cart中的 `protected function actionAddProductToCart($item)`方法。

原理为：当访问 addProductToCart时，由于找不到该函数，就会执行
`@fecshop\services\Service->__call()`魔术方法，然后由魔术方法，
将 `addProductToCart` 改成  `actionAddProductToCart`，然后去查找函数，就会找到
，这样做的好处是，可以在`__call()`函数中记录每一个service的方法调用开始时间
和结束时间，这样就可以更好的调试出来哪一个service方法耗费的时间长，
这个是为了更好地统计各个services的状况，譬如：排查耗费时间最长的services，
使用最频繁的services等，
当然会耗费一定的时间，
在线上可以关掉log记录时间的功能，也可以间断性的手动开启，进行线上调试。


关于services log的开启：`@fecshop\config\services\Helper`中看到如下配置：

```
return [
	'helper' => [
		'class' => 'fecshop\services\Helper',
		# 子服务
		'childService' => [
			'ar' => [
				'class' => 'fecshop\services\helper\AR',
			],
			'log' => [
				'class' => 'fecshop\services\helper\Log',
				'log_config' => [
					# service log config
					'services' => [	
						# if enable is false , all services will be close
						'enable' => false,  # 这里可以开启services log功能。
```

通过配置helper log服务的enable设置为true，可以开启services的日志功能

当然helper log服务还有其他的一些设置，具体请参看详细代码。

当然，您可以把服务中的类函数定义成`public` ，函数名不以`action`开头，
这种方式定义的函数，开启services log，不会被记录，因为直接找到函数名，不会
访问魔术方法`__call()`。



4.关闭Service
---------

对于您自己开发的`service`，您如果想去掉很轻松，把`service`对应的配置去掉,
就无法访问这个`Service`了。

对于fecshop开发的`Service`，您可以通过配置的方式关掉某个services
，在配置中加入 `'enableService' => false`  就可以了


譬如：搜索有mongodb和xunsearch搜索，mongodb对应外文搜索，
而xunsearch对应的是中文搜索，如果我是做跨境电商的，我不需要中文搜索，
那么，我就不需要安装xunsearch，后台产品编辑save的时候，也不需要把产品
同步到xunSearch中，因此，我们可以通过加入（或修改） `'enableService' => false`
就可以了

打开文件： @common/config/fecshop_local_services/Search.php

可以看到xunSearch的配置：

```
'xunSearch'  => [
    'fuzzy'         => true,  // 是否开启模糊查询
    'enableService' => true,
    'synonyms'      => true, //是否开启同义词翻译
    'searchLang'    => [
        'zh' => 'chinese',
    ],
],
```

设置 `'enableService' => false` , 将关掉xunSearch Services
，然后，我们关掉xunSearch（kill进程），然后后台保存产品，会发现保存成功，


对于Service关闭的原理，可以参看文件 `@fecshop/services/Service.php` 文件











