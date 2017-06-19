Fecshop 消息MQ
==============

> 这里的MQ，以及例子为rabbitMQ 的使用，当然，您可以使用其他的Mq，
> zhuravljov/yii2-queue同样支持，[详情参看地址](https://github.com/zhuravljov/yii2-queue/blob/master/docs/guide/README.md#queue-drivers)

### 1.环境

queue的支持，需要安装rabbitMq和php amqp扩展

1.1 [安装 RabbitMQ – centos 6](http://www.fancyecommerce.com/2017/06/02/%e5%ae%89%e8%a3%85-rabbitmq-centos-6/)

1.2 [rabbitmq php 安装amqp扩展](http://www.fancyecommerce.com/2017/06/02/rabbitmq-php-%e5%ae%89%e8%a3%85amqp%e6%89%a9%e5%b1%95/)

1.3 安装  [Yii2 php-amqplib](https://github.com/zhuravljov/yii2-queue)扩展 ，您在根目录的composer.json
中`require`部分添加代码` "php-amqplib/php-amqplib": "2.6.*"`
和 `"php-amqplib/php-amqplib": "2.6.*"` 即可。
即可

```
 "require": {
    "php": ">=5.4.0",
    "yiisoft/yii2": ">=2.0.6",
    "yiisoft/yii2-bootstrap": "*",
    "yiisoft/yii2-swiftmailer": "*",
    "yiisoft/yii2-apidoc": "~2.0.0",
    "fancyecommerce/fecshop": ">=1.1.3.1",
    "php-amqplib/php-amqplib": "2.6.*",  
    "zhuravljov/yii2-queue": "*"
         
},
```

然后执行 `composer update` ,安装。 

### 2.Mq的设置

在配置文件`@fecshop\app\console\config\console.php`

```
//配置RabbitMq 部分
    'bootstrap' => [
        'queue', // The component registers own console commands
    ],
    
    'components' => [
        'queue' => [
            //'class' => \zhuravljov\yii\queue\amqp\Queue::class,
            'class' => 'zhuravljov\yii\queue\amqp\Queue',
            'host'  => 'localhost',
            'port'  => 5672,
            'user'  => 'mqadmin',
            'password' => 'mqadmin20177',
            'queueName' => 'queue',
        ],
    ],
```

上面的用户名和密码就是在上面安装rabbitMq时设置的用户名和密码。

### 3.使用

使用是非常简单的，Yii2的queue组件非常棒。

（注意：下面的方式仅限于MQ的生产方和消费方都是fecshop（Yii2），
因为传递的是对象，如果消费方不是fecshop，那么，消费方是没有传递的对象的定义，因此是不行的）

3.1 定义一个执行类，您想要做xx事情，就在下面execute($queue)方法中，譬如：

```
<?php
namespace fecshop\app\console\modules\Amqp\block;

use yii\base\Object;

class PushTest extends Object implements \zhuravljov\yii\queue\Job
{
    public $name;
    public $age;
    
    # 这里是具体要做的事情。
    public function execute($queue)
    {
        echo 'name:'.$this->name.'###'.'age:'.$this->age;
    }
}
```

这是一个对象，里面有相应的值，这个对象必须实现execute($queue) 方法。

里面的内容，您可以做输出，也可以做调用。总之，您想要做的事情都在
execute($queue)方法中

3.2 生产方

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace fecshop\app\console\modules\Amqp\controllers;

use Yii;
use yii\console\Controller;
use fecshop\app\console\modules\Amqp\block\PushTest;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class TestController extends Controller
{
    
    public function actionTest()
    {
        Yii::$app->queue->push(new PushTest([
            'name'  => 'terry',
            'age'   => 31,
        ]));
    }

    
}
```

生产方的new PushTest() 就是上面我们定义的类。

3.3 执行

您可能纳闷，为什么不需要写消费方的代码？
这里是不需要的，这个Yii2扩展做的非常棒，解耦的非常好，
因为生产方传递的是一个对象，消费方直接执行这个对象的execute()方法。
消费方就是下面的`queue/listen`

生产端命令，这个就是上面写的controller

```
./yii amqp/test/test
```

消费端命令

```
./yii queue/listen
```

在生产端执行后，就可以看到输出了

```
name:terry###age:31
```

### 4.应答机制

应答机制：当消费方接收解析，执行的时候，有可能会失败，这样就有疏漏，
为了防止这种情况，我们可以用应答机制，
消费方在连接初始化的时候，告诉需要开启应答，消费方获取消息后，
MQ不会删除消息，等消费方接受消息执行成功后，应答机制告知MQ，
MQ才会删除消息，这样，就避免消息执行失败。

默认是开启应答的

4.1消费方消费成功后，告诉RabbitMq，RabbitMq认为这个消息消费成功，才会删除消息。

4.2消费方执行时间很长，RabbitMq是没有超时时间的，因此不会把这个消息给其他的消费方消费

4.3如果程序卡住，kill进程，连接断开，MQ会认为消费失败，把消息发送给其他的消费者消费。

4.4上面的PushTest->execute($queue)，如果里面添加了exit()退出代码，这样会直接停掉，导致没有应答,MQ会重新发送给其他消费方。
，因此这个函数里面是不能写入exit之类的代码的。


监听部分的代码分析：`vendor\zhuravljov\yii2-queue\src\drivers\amqp\Queue.php`

下面是listen部分的代码

```
/**
     * Listens amqp-queue and runs new jobs.
     */
    public function listen()
    {
        $this->open();
        $callback = function(AMQPMessage $message) {
            # 此处调用执行。
            # 执行$this->handleMessage，会调用PushTest->execute($queue)，
            # 执行完成后，返回true
            if ($this->handleMessage(null, $message->body)) {
                # 下面是应答代码，执行后，告诉MQ,消费完成
                # 注意，Rabbit是没有超时概念的，如果上面函数一直执行，没有完成，那么这个未完成的消费不会分给其他的消费方
                # 消费完成，进行应答
                $message->delivery_info['channel']->basic_ack($message->delivery_info['delivery_tag']);
            }
        };
        # 多个消费方负载方面的设置。
        $this->channel->basic_qos(null, 1, null);
        # 第三个参数  no_ack 的 值为false代表，需要应答，true代表不需要应答。
        $this->channel->basic_consume($this->queueName, '', false, false, false, false, $callback);
        while(count($this->channel->callbacks)) {
            $this->channel->wait();
        }
    }
```

fecshop有一个测试的例子，你可以在两个终端执行：

生产方：`./yii amqp/test/test`

消费方：`./yii queue/listen`

### 5.功能使用

对于fecshop，目前还没有做MQ部分的功能，有一些地方是可以用的
，譬如发邮件部分，用MQ发送邮件可以节省很多响应时间，
目前只是接纳到框架中，如果您有需求，可以使用MQ扩展或者重构。

### 6.和其他系统的MQ对接

有时候需要和其他的系统进行对接，譬如从erp MQ里面对接产品数据，
MQ传递的是一个序列化，或者json格式的数据，那么，上面的方式就不好用了
，我们可以用下面的方式，来写和外部系统MQ的对接。

6.1 生产方：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace fecshop\app\console\modules\Amqp\controllers;

use Yii;
use yii\console\Controller;
use fecshop\app\console\modules\Amqp\block\PushTest;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class TestController extends Controller
{
    protected $_numPerPage = 50;

    /**
     * 得到当前的时间。
     */
    public function actionTest()
    {
        # 这个是对象的方式，消息的传递和接收都是fecshop的时候使用
        //Yii::$app->queue->push(new PushTest([
        //    'name'  => 'terry',
        //    'age'   => 31,
        //]));
        
        # 这是一种比较随便的方式，发送的数组会以序列化的方式发送过去
        # 由于传递的不是对象，接收方需要进行处理。
        Yii::$app->queue->push([
            'name'  => 'water',
            'age'   => 331,
        ]);
    }

    
}
```

通过上面的push方法，传递一个序列化的数组给MQ。


6.2 消费方

如果其他的系统生产数据给MQ（序列化数组格式），我们消费，

定义queue组件：

```
'components' => [
    'queue' => [
        //'class' => \zhuravljov\yii\queue\amqp\Queue::class,
        //'class' => 'zhuravljov\yii\queue\amqp\Queue',
        'class' => 'fecshop\app\console\modules\Amqp\block\Queue',
        'host'  => 'localhost',
        'port'  => 5672,
        'user'  => 'mqadmin',
        'password' => 'mqadmin20177',
        'queueName' => 'queue',
    ],
],
```

实现上面的class

```
<?php
namespace fecshop\app\console\modules\Amqp\block;

use yii\base\Object;

class Queue extends \zhuravljov\yii\queue\amqp\Queue
{
    
    /**
     * @inheritdoc
     */
    protected function handleMessage($id, $message)
    {
        $d = unserialize($message);
        # 这里填写执行代码
        //  do some thing ...
        
        \Yii::info('222','fecshop_debug');
        return true;
    }
    
    /*
     protected function handleMessage($id, $message)
    {
        if ($this->messageHandler) {
            return call_user_func($this->messageHandler, $id, $message);
        } else {
            return parent::handleMessage($id, $message);
        }
    }
    */
}
```

我们在新的组件中重写 handleMessage 方法，然后在里面处理接收的数据即可。

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace fecshop\app\console\modules\Amqp\controllers;

use Yii;
use yii\console\Controller;
use fecshop\app\console\modules\Amqp\block\PushTest;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 * 这是一个测试RabbitMq 的一个例子。这里作为消息生产方。
 * 你可以通过执行 ./yii amqp/test/test 来生产数据。
 */
class TestController extends Controller
{
    protected $_numPerPage = 50;

    /**
     * 测试
     */
    public function actionTest()
    {
        // 这个是对象的方式，消息的传递和接收都是fecshop的时候使用
        // Yii::$app->queue->push(new PushTest([
        //    'name'  => 'terry',
        //    'age'   => 31,
        // ]));
        
        // 这是一种比较随便的方式，发送的数组会以序列化的方式发送过去
        // 传递的给MQ的个数格式为序列化数组。
        Yii::$app->queue->push([
            'name'  => 'water',
            'age'   => 331,
        ]);
    }
    
    
    public function actionListen()
    {
        Yii::$app->queue->listen();
    }
    
   
    
}
```

然后执行

生产： `./yii  amqp/test/test`

消费： `./yii  amqp/test/listen`








如果有多个MQ接收消息，
可以定义多个组件


```
'components' => [
    'queue1' => [
       
    ],
    'queue2' => [
       
    ],
    'queue3' => [
       
    ],
],
```

每一个指定一个class即可。

