Fecshop 本地新建modules，开发新功能
======================



如果想在fec上面扩展，添加自己的功能，那么可以自己新建模块modules

下面以appfront入口，新建mytest模块的代码例子

1.新建模块的配置文件

`appfront/config/fecshop_local_modules` 下面新建文件Mytest.php ，里面添加代码如下：

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
    'mytest' => [
        'class' => '\appfront\local\local_modules\Mytest\Module',

    ],
];

```

2.新建模块mytest，上面配置文件class对应的类是模块的入口文件

建立文件：appfront/local/local_modules/Mytest/Module.php 里面的代码如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace appfront\local\local_modules\Mytest;

use fecshop\app\appfront\modules\AppfrontModule;
use Yii;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class Module extends AppfrontModule
{
    public $blockNamespace;

    public function init()
    {
        //echo 1;exit;
        // 以下代码必须指定
        $nameSpace = __NAMESPACE__;
        // web controller
        if (Yii::$app instanceof \yii\web\Application) {
            $this->controllerNamespace = $nameSpace . '\\controllers';
            $this->blockNamespace = $nameSpace . '\\block';
        }
        Yii::$service->page->theme->layoutFile = 'main.php';
        parent::init();
    }
}

```

3.新建模块里的controller文件

appfront/local/local_modules/Mytest/controllers/CustomerController.php ，代码如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace appfront\local\local_modules\Mytest\controllers;

use fecshop\app\appfront\modules\AppfrontController;
use Yii;
use yii\web\Response;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class CustomerController extends AppfrontController
{

    public function init()
    {
        parent::init();
        //Yii::$service->page->theme->layoutFile = 'category_view.php';
    }
    
    public function actionTest(){
       // echo 2;exit; 
        $data = $this->getBlock()->getLastData();
        return $this->render($this->action->id, $data);
    }
    
    
}
```

4.新建block文件 appfront/local/local_modules/Mytest/block/customer/Test.php , 代码内容如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace appfront\local\local_modules\Mytest\block\customer;

use Yii;
use yii\base\InvalidValueException;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class Test
{

    public function getLastData()
    {
        
        return ['name' => 'zhangsan'];
    }
}
```

上面我只是简单的返回一个数组。在getLastData() 方法里面，您可以按照自己的业务逻辑实现，最终返回一个数组给controller

5.建立view文件 fecshop/appfront/theme/terry/theme01/mytest/customer/test.php

`terry`:模板包名 ， `theme01`:模板名 ， `mytest/customer/test.php`:view文件路径

内容填写如下：

```
<?= $name  ?>

```

只做了一个简单的输出，然后访问url ： https://fecshop.appfront.fancyecommerce.com/mytest/customer/test
就可以看到了

对于url ：
`mytest` : 模块名字，`customer` : controller名字  ，`test` : action方法名字

到这里就完成了一个基本的模块modules。

















