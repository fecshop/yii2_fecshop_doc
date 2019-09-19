FecMALL 组件开发
================


yii2中自定义全局组件：

yii2中定义了很多的组件，我们可以自己添加一个组件，步骤如下：

1.建立文件MyComponent.php，也即是我们自定义的组件:

```
    <?php
    namespace app\component;
    use Yii;
    use yii\base\Component;
    use yii\base\InvalidConfigException;
     
    class MyComponent extends Component
    {
      
      public $terry;
      
      public function welcome()
      {
        echo $this->terry."Hello..Welcome to MyComponent";
      }
     
    }
```

custom component ，自定义组件。

2.添加配置，在config.php文件的component中：

```
    'mycomponent' => [
         'class' => 'appadmin\component\MyComponent',
         'terry' => 'xxxx',
     ],
```

3.调用：

```
    Yii::$app->mycomponent->welcome();
```


可以看到以下的输出：xxxxHello..Welcome to MyComponent1



这些知识都是Yii2的知识范畴。


[yii2 添加 自定义 组件 custom component，以及模块 module 原理的详解剖析](http://www.fancyecommerce.com/2016/05/18/yii2-%E6%B7%BB%E5%8A%A0-%E8%87%AA%E5%AE%9A%E4%B9%89-%E7%BB%84%E4%BB%B6-custom-component/)






