Fecshop 在现有的modules上面开发新controller
========================

对于fecshop已经有了很多的modules，如果你想开发一个新modules，
可以参看下面的教程，
[Fecshop 本地新建modules，开发新功能](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_hand_local_module.html)

如果你不想搞一个新的modules，而是在fecshop原来的modules上面，
进行新的controller开发，那么您可以参看本教程

下面以appfront 的customer模块为例子：

fecshop的appfront 的customer的文件路径为：
@fecshop/app/appfront/modules/Customer,
打开 @fecshop/app/appfront/modules/Customer/controllers
可以看到很多的fecshop开发的controllers，下面我们在原有模块的基础上面开发新的
controller


vendor文件夹下面的文件我们不能改动，因此，我们需要通过重写的方式，
我们可以通过 controllerMap轻松实现

1.在@appfront/config/fecshop_local_modules/下面新建Customer.php文件
（文件名是随便命名的，但是为了易于管理，因此命名对应好会更好一些）

内容如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 *
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
return [
    'customer' => [
        'controllerMap' => [
            'test' => 'appfront\local\local_modules\Customer\controllers\TestController'
        ]

    ],
];
```

上面的代码为添加controllerMap

2.新建文件@appfront\local\local_modules\Customer\controllers\TestController.php 文件
，内容如下：


```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace appfront\local\local_modules\Customer\controllers;

use fecshop\app\appfront\modules\AppfrontController;
use Yii;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class TestController extends AppfrontController
{
    public $enableCsrfValidation = false;

    public function init()
    {
        parent::init();
    }

    public function actionIndex()
    {
        echo 111111;
    }
}


```


3.然后就可以访问这个新建的controller了

http://www.xxxxx.com/customer/test/index

就可以看到上面的输出了 `111111`

4.对于controller的getBlock()方法，还是会去找fecshop模块的block文件路径，因此您可以
有两种方式解决这个问题

4.1不用getBlock()方法，所用到的Block通过namespace use引入进来调用

4.2在此controller中重写getBlock()，让其寻址到您自己的block路径中。

5.新建theme文件

5.1将上面的TestController文件的actionIndex方法更改

```
    public function actionIndex()
     {
         $data = ['name' => 'fecshop terry'];
         return $this->render($this->action->id, $data);
     }
```

5.2新建view文件
@appfront/theme/terry/theme01/customer/test/index.php文件，
填写内容如下：

```

name is <?= $name ?>

```


重新访问:http://www.xxxxx.com/customer/test/index
,可以看到输出如下：

```
name is fecshop terry
```


