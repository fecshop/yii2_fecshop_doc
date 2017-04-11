Fecshop 服务层
==============

> fecshop的服务层，分为服务和子服务，以及子子服务。目前
> fecshop只有两层服务。



### Fecshop 服务介绍：

服务和子服务都必须继承@fecshop\services\Service

您可以在fecshop服务里查看详细介绍：

[Fecshop服务的原理](fecshop-services-abc.md)

[Fecshop服务的规则](fecshop-services-rule.md)

### 服务的配置：

譬如：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
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

cms是服务的配置，通过childService来配置cms
服务的子服务article，子服务也是通过class加参数，
通过配置注入的方式得到

### 服务的特点：

组件都是单例模式，只能实例化一次，是通过服务类
和服务配置，通过容器生成，在框架的任意地方都可以调用
，非常方便，作为整个系统的底层中间层，用来连接
modules和model之间的通信，
modules通过调用服务来完成具体的功能，服务是通过model调用数据
，然后组织数据返回给modules。
这样的好处就是：1.对于多个应用入口，各个入口的modules
都是独立的，service作为公用部分，减少代码的冗余，
2.为日后的代码重构，虽然业务的发展，系统可能在很多方面需要重构，
可能，有大的更改，譬如：服务层的底层代码，不在由php实现
而是由接口的方式调用java的api来实现底层，等等。
为了速度的考虑，服务的实现尽量简洁。













