Fecshop 模块开发
================

### 1.添加模块配置

下面是添加或者重写一个模块的配置例子：

```
<?php
return [
	'cms' => [
		'class' => '\fecshop\app\appfront\modules\Cms\Module',
		'params'=> [
			'homeTitle' 			=> 'fecshop home page',
			'homeMetaKeywords'		=> 'fecshop , fancy ecommerce shop ',
			'homeMetaDescription'	=> 'fancy ecommerce shop , base Yii2 framework',
		],
	],
];
```

然后需要建立module文件：


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

然后建立 controller等等，这些语法，都是yii2的方式。

需要注意的是，您在重新或者新建本地开发模块的时候
，您需要遵循相应区块的方式，最简单的方式就是模仿，
找一个系统中的例子，复制出来，然后修改路径，
这是最稳妥的方式。










