Fecshop 模块开发
===============

> 此处说的模块，就是Yii2框架的模块。下面是如何定义一个模块，
> 以cms模块为例

### 添加模块

1.添加配置 ， @fecshop/app/appfront/config/modules/Cms.php

```
return [
	'cms' => [
		'class' => '\fecshop\app\appfront\modules\Cms\Module',
	],
];
```

这里定义了模块的名字，以及模块的入口文件：

2.入口文件内容如下：

```
<?php
namespace fecshop\app\appfront\modules\Cms;
use Yii;
use fecshop\app\appfront\modules\AppfrontModule;
class Module extends AppfrontModule
{
    public $blockNamespace;
    public function init()
    {
		# 以下代码必须指定
		$nameSpace = __NAMESPACE__;
		# web controller
		if (Yii::$app instanceof \yii\web\Application) {
			$this->controllerNamespace 	= 	$nameSpace . '\\controllers';
			$this->blockNamespace 	= 	$nameSpace . '\\block';
		# console controller
		} elseif (Yii::$app instanceof \yii\console\Application) {
			$this->controllerNamespace 	= 	$nameSpace . '\\console\\controllers';
			$this->blockNamespace 	= 	$nameSpace . '\\console\\block';
		}
		//$this->_currentDir			= 	__DIR__ ;
		//$this->_currentNameSpace	=   __NAMESPACE__;
		
		# 指定默认的man文件
		//$this->layout = "home.php";
		Yii::$service->page->theme->layoutFile = 'home.php';
		parent::init();  
		
    }
}

```

这里面对模块进行了初始化。

`$this->controllerNamespace` : 指的是模块的controller路径

`$this->blockNamespace` ： 指的是模块的block路径

`Yii::$service->page->theme->layoutFile = 'home.php';`： 指定模板layout下面的
文件名字

### 模块的结构：

模块里面有几个部分：

模块入口部分：Modules.php，这里是模块配置中class对应的文件，
这个文件里面定义了controllers，block等等很多模块参数的初始化。

模块的controllers部分：模块的控制层部分，这里

模块的block部分：模块的中间逻辑处理层，处理完成的数据返回controllers

模块的helpers部分：帮助类，一般是一些静态类处理部分。一些非数据库的操作处理。

如果您想要重写模块，可以在配置部分的class指向您重写的文件地址即可。













