Fecshop 服务使用
================


您可以在任何地方，通过`Yii::$service`,使用服务，譬如

`Yii::$service->cart->coupon->addCoupon()`，就是用cart服务下面的子服务下面的
addCoupon()方法。

那么如何制作一个服务呢？下面是详细的步骤：

1.首先定义一个类，继承fecshop\services\Service

```
<?php
namespace appfront\services;
use Yii;
use yii\base\InvalidValueException;
use yii\base\InvalidConfigException;
use fecshop\services\Service;

class Test extends Service
{
	public $name;
	protected function actionGet(){
		
		return $this->name ;
	}
}

```

2.添加配置：

在@app\config\fecshop_local_services文件夹下面添加一个文件Test.php内容为：

```
<?php
/**
 * FecShop file.
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
return [
	'test' => [
		'class' => 'appfront\services\Test',
		'name'  => 'terry',
	]
];
```

然后，就可以执行
`echo  Yii::$service->test->get();` ,输入为:`terry`，
这个是上面的配置中的值，在test服务实例化的时候，name参数会被注入到
Test类的类变量`name`中，这个和Yii2的component（组件）的原理类似。

3.服务停用

如果在配置中加入 ` 'enable' => false ` ，则该services将不可用

譬如：

```
return [
	'test' => [
		'class' => 'appfront\services\Test',
        'enable'=> false,
		'name'  => 'terry',
	]
];
```

则该services 不在可用。相当于从配置中删除。


















