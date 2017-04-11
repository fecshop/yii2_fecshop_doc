Fecshop 服务原理：
================


在yii2中，组件是可以通过配置的方式添加到Yii::$app中的。

现在我们想添加一个Yii静态变量，$service，下面都称呼这个变量为服务，

可以通过Yii::$service访问，然后添加服务，以及服务的子服务，
譬如我添加了一个cms服务，以及cms服务的子服务article。

那么我想访问cms服务，可以通过Yii::$service->cms访问，

如果我想访问cms服务的子服务，那么，我可以通过Yii::$service->cms->article访问。

上面的使用访问和yii2的组件很类似，是单例模式。下面说具体实现方式：

1.创建一个Yii.php添加$service参数：  @vendor/fancyecommerce/fecshop/yii/Yii.php

```
    <?php
    $dir = __DIR__ . '/../../../yiisoft/yii2';
    require($dir.'/BaseYii.php');
    /**
     * Yii is a helper class serving common framework functionalities.
     *
     * It extends from [[\yii\BaseYii]] which provides the actual implementation.
     * By writing your own Yii class, you can customize some functionalities of [[\yii\BaseYii]].
     *
     * @author Qiang Xue <qiang.xue@gmail.com>
     * @since 2.0
     */
    class Yii extends \yii\BaseYii
    {
      public static $service;
      
    }
    spl_autoload_register(['Yii', 'autoload'], true, true);
    Yii::$classMap = require($dir.'/classes.php');
    Yii::$container = new yii\di\Container();
```

2.在入口文件index.php中，将对yii的Yii.php去掉，换成：


```
    require(__DIR__ . '/../../vendor/fancyecommerce/fecshop/yii/Yii.php');
```


也就是加载上面，我创建的文件。

然后修改index.php底部代码：

```
    new fecshop\services\Application($config['services']);
    unset($config['services']);
    //var_dump($config);
    $application = new yii\web\Application($config);
    $application->run();
```

也就是添加了代码：

```
    new fecshop\services\Application($config['services']);
    unset($config['services']);
```

这个代码的作用是，给$service变量赋值，Yii::$service = fecshop\services\Application($config[‘services’]);

3.下面我们实现这个Application。


```
    <?php
    /**
     * FecShop file.
     *
     * @link http://www.fecshop.com/
     * @copyright Copyright (c) 2016 FecShop Software LLC
     * @license http://www.fecshop.com/license/
     */
    namespace fecshop\services;
    use Yii;
    use yii\base\Component;
    use yii\base\InvalidConfigException;
    /**
     * @author Terry Zhao <2358269014@qq.com>
     * @since 1.0
     */
    class Application
    {
      public $childService;
      public $_childService;
      
      
      public function __construct($config = [])
        {
            Yii::$service     = $this;
            $this->childService = $config;
        }
      /**
       * 得到services 里面配置的子服务childService的实例
       */
      public function getChildService($childServiceName){
        if(!$this->_childService[$childServiceName]){
          $childService = $this->childService;
          if(isset($childService[$childServiceName])){
            $service = $childService[$childServiceName];
            $this->_childService[$childServiceName] = Yii::createObject($service);
          }else{
            throw new InvalidConfigException('Child Service ['.$childServiceName.'] is not find in '.get_called_class().', you must config it! ');
          }
        }
        return $this->_childService[$childServiceName];
      }
      
      /**
       * 
       */
      public function __get($attr){
        return $this->getChildService($attr);
        
      }
      
    }
```

4. 在配置中添加配置：


```
    [
    'services' => [
        'cms' => [
            'class' => 'fecshop\services\Cms',
            
            # 子服务
            'childService' => [
                'article' => [
                    'class'             => 'fecshop\services\cms\Article',
                    'storage' => 'mysqldb', # mysqldb or mongodb.
                ],
            ],
        ],
    ]
```

5.上面的配置，给cms添加了一个子服务article。

cms 对应的class的代码如下：


```
    <?php
    /**
     * FecShop file.
     *
     * @link http://www.fecshop.com/
     * @copyright Copyright (c) 2016 FecShop Software LLC
     * @license http://www.fecshop.com/license/
     */
    namespace fecshop\services;
    use Yii;
    use yii\base\InvalidValueException;
    use yii\base\InvalidConfigException;
    use fec\helpers\CSession;
    use fec\helpers\CUrl;
    /**
     * Breadcrumbs services
     * @author Terry Zhao <2358269014@qq.com>
     * @since 1.0
     */
    class Cms extends Service
    {
      /**
       * cms storage db, you can set value: mysqldb,mongodb.
       */
      public $storage = 'mysqldb';
      
    }
```


artile的代码如下：


```
    <?php
    /**
     * FecShop file.
     *
     * @link http://www.fecshop.com/
     * @copyright Copyright (c) 2016 FecShop Software LLC
     * @license http://www.fecshop.com/license/
     */
    namespace fecshop\services\cms;
    use Yii;
    use yii\base\InvalidValueException;
    use yii\base\InvalidConfigException;
    use fec\helpers\CSession;
    use fec\helpers\CUrl;
    use fecshop\services\Service;
    use fecshop\services\cms\article\ArticleMysqldb;
    use fecshop\services\cms\article\ArticleMongodb;
    /**
     * Breadcrumbs services
     * @author Terry Zhao <2358269014@qq.com>
     * @since 1.0
     */
    class Article extends Service
    {
      public $storage = 'mongodb';
      protected $_article;
      
      
      public function init(){
        if($this->storage == 'mongodb'){
          $this->_article = new ArticleMongodb;
        }else if($this->storage == 'mysqldb'){
          $this->_article = new ArticleMysqldb;
        }
      }
      /**
       * Get Url by article's url key.
       */
      public function getUrlByPath($urlPath){
        //return Yii::$service->url->getHttpBaseUrl().'/'.$urlKey;
        return Yii::$service->url->getUrlByPath($urlPath);
      }
      /**
       * get artile's primary key.
       */
      public function getPrimaryKey(){
        return $this->_article->getPrimaryKey();
      }
      /**
       * get artile model by primary key.
       */
      public function getByPrimaryKey($primaryKey){
        return $this->_article->getByPrimaryKey($primaryKey);
      }
      
      
      
      /**
       * @property $filter|Array
       * get artile collection by $filter
       * example filter:
       * [
       *     'numPerPage'   => 20,    
       *     'pageNum'    => 1,
       *     'orderBy'  => ['_id' => SORT_DESC, 'sku' => SORT_ASC ],
       *     'where'      => [
       *       'price' => [
       *         '?gt' => 1,
       *         '?lt' => 10,
       *       ],
       *       'sku' => 'uk10001',
       *     ],
       *   'asArray' => true,
       * ]
       */
      public function coll($filter=''){
        return $this->_article->coll($filter);
      }
      
      /**
       * @property $one|Array , save one data .
       * @property $originUrlKey|String , article origin url key.
       * save $data to cms model,then,add url rewrite info to system service urlrewrite.                 
       */
      public function save($one,$originUrlKey){
        return $this->_article->save($one,$originUrlKey);
      }
      
      public function remove($ids){
        return $this->_article->remove($ids);
      }
      
    }
```

他们继承的service类代码如下：


```
    <?php
    /**
     * FecShop file.
     *
     * @link http://www.fecshop.com/
     * @copyright Copyright (c) 2016 FecShop Software LLC
     * @license http://www.fecshop.com/license/
     */
    namespace fecshop\services;
    use Yii;
    use yii\base\Object;
    use yii\base\InvalidConfigException;
    /**
     * @author Terry Zhao <2358269014@qq.com>
     * @since 1.0
     */
    class Service extends  Object
    {
      public $childService;
      public $_childService;
      
      /**
       * 得到services 里面配置的子服务childService的实例
       */
      public function getChildService($childServiceName){
        if(!$this->_childService[$childServiceName]){
          $childService = $this->childService;
          if(isset($childService[$childServiceName])){
            $service = $childService[$childServiceName];
            $this->_childService[$childServiceName] = Yii::createObject($service);
          }else{
            throw new InvalidConfigException('Child Service ['.$childServiceName.'] is not find in '.get_called_class().', you must config it! ');
          }
        }
        return $this->_childService[$childServiceName];
      }
      
      /**
       * 
       */
      public function __get($attr){
        return $this->getChildService($attr);
        
      }
      
    }
```

然后，我就可以使用了，按照上面的方法

```
    Yii::$service->cms->$storage     # 获取存储方式，这个变量可以在service配置中注入。
    Yii::$service->cms->article->remove($ids)  # cms服务对应子服务artile的删除功能。
```

由于这种方式是单例模式，因此，可以用这种方式，在controller和model之间，做一个中间服务层，方便日后的扩展和使用，譬如我如果把mysql换成了mongodb，只需要把这个服务的public方法 重新实现以下就可以了，目前fecshop采用了这种实现方式。

