Fecshop Event
==============

> Fecshop 事件


fecshop的事件，没有使用yii2的事件机制，而是自己做了一个比较
简单的类似事件机制。

### 事件使用

目前只有四个事件：

```
return [
	'event' => [
		'class' => 'fecshop\services\Event',
		# 事件配置表，这是Fecshop默认存在的事件。您可以在配置中添加您的事件函数。
		'eventList' => [
			# 加入购物车before
			'event_add_to_cart_before' 		=> [],
			# 加入购物车after
			'event_add_to_cart_after' 		=> [],
			# 生成订单before
			'event_generate_order_before' 	=> [],
			# 生成订单after
			'event_generate_order_after' 	=> [],
			
		]
		
		
		
	],
];
```

添加事件举例：首先在配置中加入如下:



```
return [
	'event' => [
		'eventList' => [
			# 加入购物车前
			'event_add_to_cart_before' => [
				['appfront\event\CartTest1','beforeAdd1'],
				['appfront\event\CartTest2','beforeAdd2'],
			],
			
		]
		
	],
];
```

然后新建 文件appfront\event\CartTest1.php 并新建

```
class CartTest1
{
	
	public static function beforeAdd1($cartInfo){
		
		//var_dump($cartInfo);
	}
	
	
	
}
```

即可，在函数里面写您想要做的事情了


由于fecshop采用service的方式，感觉event的用处不大，
但还是得有这个机制，就这样做了4个事件。




