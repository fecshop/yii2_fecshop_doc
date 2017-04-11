Fecshop 模块层
==============

> fecshop的具体功能都是模块的方式进行组织，采用的是yii2
的模块。

fecshop 模块

fecshop的模块配置在：@fecshop\app\appXXX\config中，
下面是appadmin下的cms模块的配置的例子：

```php
<?php
return [
	'cms' => [
			'class' => '\fecshop\app\appadmin\modules\Cms\Module',   
	],
];


```

通过class，就知道模块的入口文件的位置，下面找到这个文件,下面这个是appadmin下面的cms模块的配置，


```php
<?php
namespace fecshop\app\appadmin\modules\Cms;
use Yii;
class Module extends \fec\AdminModule
{
    public function init()
    {
		
		# 以下代码必须指定
        $this->controllerNamespace 	= 	__NAMESPACE__ . '\\controllers';
		$this->_currentDir			= 	__DIR__ ;
		$this->_currentNameSpace	=   __NAMESPACE__;
		
		# 指定默认的man文件
		$this->layout = "/main_ajax.php";
		parent::init();  
		
    }
}

```

下面是appfront下面的cms的配置：

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

下面是appfront的cms模块的module文件

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

各个入口的module，根据自身功能的需要，还是有一些差异。
通过上面可以看到module在[[init]]方法中，进行了一些列的初始化，
譬如根据不同的应用类型，web application 还是console application
设置不同的[[controllerNamespace]] 和[[blockNamespace]],
指定 page的子服务 theme 的 layoutFile等等。

模块的结构：

模块分为：

**controllers** 该文件夹下面为controllers文件，这里的文件
为控制器，本身不操作数据，数据的逻辑处理由block层完成，
返回结果给controller，然后有controller调用render方法
将数据传递给view，画出来整个页面

**block** ，该文件夹下面为block文件。block相当于模块的肌肉
将controller调用block后，由block进行调用服务组件，进行逻辑处理
，将最终的数据，以数组的方式返回给controller中

**helpers** 该文件夹下面为helpers文件。
完成一些模块公用型的功能。

**Module.php**  模块的入口文件

需要注意的是，模块中view文件，在appadmin中，是存在于
模块中的，因为后台不需要更换模板，
而对于前台，是需要多种模板的，因此view文件是在theme路径下面，
而不是在module下面。

另外 模块中是不允许直接调用model的，虽然在语法上是允许的，
模板对底层数据的操作是通过服务组件完成的，这种方式
可以对多入口，以及日后的重构提供很大的方便。也就是说
，这样的方式，是为了以后的扩展和重构。


对于其他更加详细的，请参阅源码注释。














