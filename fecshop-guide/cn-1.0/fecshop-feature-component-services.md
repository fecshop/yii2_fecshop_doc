Fecshop 服务层
==============

>fecshop的服务层，分为服务和子服务，服务组件是通过
yii2的组件来完成的，子组件是通过php的魔术方法来得到的。



### fecshop 服务：

必须继承@fecshop\services\Service;

### fecshop 子服务：

必须继承@fecshop\services\ChildService;

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


组件都是单例模式，只能实例化一次。
