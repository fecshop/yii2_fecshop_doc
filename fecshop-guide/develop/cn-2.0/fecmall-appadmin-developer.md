Fecmall Admin 二次开发
=========================

> 关于该入口的描述和说明


### Appadmin 介绍

1.如果您想要重写fecmall原来的功能，可以参看：
[Fecmall 重写功能](fecmall-rewrite-func.md)

2.如果您想做新的功能扩展
，那么需要建立自己的module

在appadmin本地新建模块前，建议先去了解一下 fecmall appadmin端的代码：

`@fecshop/app/appadmin/modules` 下面就是 fecmall appadmin入口的模块部分。

了解清楚 fecmall 后台的大致原理，您就可以自己写一个本地模块了，下面是一个例子，
一步一步的讲述如何从零新建一个后台`Person` modules 

### Appadmin 新增本地模块 示例

> 本部分从0讲解，如何在appadmin入口开发一个本地模块的完整步骤
> ,本部分实现了mysqldb和mongodb两个数据库的实现, 本例子是实现一个Person
> 表的后台编辑的工作

1.数据库新建表

mysql:

```
CREATE TABLE IF NOT EXISTS `example_person` (
  `id` int(20) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL COMMENT '姓名',
  `sex` int(5) DEFAULT NULL COMMENT '1代表男，2代表女，3代表人妖',
  `age` int(5) DEFAULT NULL,
  `about_me` text COMMENT '一句话介绍自己',
  `company` varchar(255) DEFAULT NULL COMMENT '公司',
  `telephone` varchar(150) DEFAULT NULL COMMENT '电话',
  `created_at` int(20) DEFAULT NULL,
  `updated_at` int(20) DEFAULT NULL,
  `created_user_id` int(20) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 AUTO_INCREMENT=5 ;

```

mongodb 不需要新建表


2.新建model 

> 此处我们假设，Person数据除了在appadmin入口使用，还需要在appfront等其他
> 入口使用，因此，我们把model ， service 都放到 公用-common 处

2.1 Mongodb Person Model

新建文件 `@common\local\local_models\mongodb\example\Person.php`

内容如下：

```
<?php
namespace common\local\local_models\mongodb\example;

use yii\mongodb\ActiveRecord;

class Person extends ActiveRecord
{
    
    /**
     * mongodb collection 的名字，相当于mysql的table name
     */
    public static function collectionName()
    {
        return 'example_person';
    }
    /**
     * mongodb是没有表结构的，因此不能像mysql那样取出来表结构的字段作为model的属性
     * 因此，需要自己定义model的属性，下面的方法就是这个作用
     */
    public function attributes()
    {
        return [
            '_id',
            'name',   
            'sex',
            'age',
            'about_me',
            'company',
            'telephone',
            'created_at',
            'updated_at',
            'created_user_id',
        ];
    }
}
```

2.2 Mysqldb Person Model

新建文件 `@common\local\local_models\mysqldb\example\Person.php`

内容如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace common\local\local_models\mysqldb\example;

use yii\db\ActiveRecord;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class Person extends ActiveRecord
{
    
    public static function tableName()
    {
        return '{{%example_person}}';
    }
}

```


3.新建service

> 因为是双数据库，因此，我们需要实现两个service，通过配置去切换使用哪个services

3.1 新增配置：`@common\config\fecshop_local_services\Person.php`

```
<?php
/**
 * FecShop file.
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 * 这是一个演示的例子，方便二次开发者参考，不属于fecshop里面的功能。
 */
return [
    'person' => [
        'class' => 'common\local\local_services\example\Person',
        'storage' => 'PersonMysqldb',   // 'PersonMysqldb'  'PersonMongodb'
    ],
];
```

3.2 service 文件，也就是上面配置中class对应的文件

`@common\local\local_services\example\Person.php`

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace common\local\local_services\example;

use fecshop\services\Service;
use Yii;

/**
 * Example Person services. 用于演示如何创建一个后台功能的例子代码
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class Person extends Service
{
    /**
     * $storagePrex , $storage , $storagePath 为找到当前的storage而设置的配置参数
     * 可以在配置中更改，更改后，就会通过容器注入的方式修改相应的配置值
     */
    public $storage;    // 当前的storage，在config中配置，在初始化的时候会被注入修改
    /**
     * 设置storage的path路径，
     * 如果不设置，则系统使用默认路径
     * 如果设置了路径，则使用自定义的路径
     */
    public $storagePath; 
    protected $_person;

    public function init()
    {
        parent::init();
        $currentService = $this->getStorageService($this);
        $this->_person = new $currentService();
    }
    /**
     * get artile's primary key.
     */
    protected function actionGetPrimaryKey()
    {
        return $this->_person->getPrimaryKey();
    }

    /**
     * get artile model by primary key.
     */
    protected function actionGetByPrimaryKey($primaryKey)
    {
        return $this->_person->getByPrimaryKey($primaryKey);
    }
    

    /**
     * 得到category model的全名.
     */
    protected function actionGetModelName()
    {
        return get_class($this->_person);
    }

    /**
     * @property $filter|array
     * get artile collection by $filter
     * example filter:
     * [
     * 		'numPerPage' 	=> 20,
     * 		'pageNum'		=> 1,
     * 		'orderBy'	=> ['_id' => SORT_DESC, 'sku' => SORT_ASC ],
     'where'			=> [
     ['>','price',1],
     ['<=','price',10]
     * 			['sku' => 'uk10001'],
     * 		],
     * 	'asArray' => true,
     * ]
     */
    protected function actionColl($filter = '')
    {
        return $this->_person->coll($filter);
    }

    /**
     * @property $one|array , save one data .
     * @property $originUrlKey|string , article origin url key.
     * save $data to cms model,then,add url rewrite info to system service urlrewrite.
     */
    protected function actionSave($one, $originUrlKey)
    {
        return $this->_person->save($one, $originUrlKey);
    }

    protected function actionRemove($ids)
    {
        return $this->_person->remove($ids);
    }
    
    protected function actionGetSexArr(){
        return [
            1 => '男',
            2 => '女',
            3 => '人妖',
        ];
    }
}

```

3.3 上面通过配置可以切换不同的services，因此我们要新建mongodb和mysql
对应的services。

> 为了以后的扩展，可能用redis写一个实现，因此，我们要用接口做约定

3.3.1 接口文件`@common\local\local_services\example\person\PersonInterface.php`

```
<?php
/**
 * FecShop file.
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 * Example Person: 在本地开发一个后台编辑模块的例子，非fecshop功能模块
 */

namespace common\local\local_services\example\person;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
interface PersonInterface
{
    public function getByPrimaryKey($primaryKey);

    public function coll($filter);

    public function save($one, $originUrlKey);

    public function remove($ids);
}

```

3.3.2 PersonMongodb

新建文件：`common\local\local_services\example\person\PersonMongodb.php`，代码如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 * Example Person: 在本地开发一个后台编辑模块的例子，非fecshop功能模块
 */

namespace common\local\local_services\example\person;

use Yii;
use yii\base\InvalidValueException;
use fecshop\services\Service;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class PersonMongodb extends Service implements PersonInterface
{
    public $numPerPage = 20;
     protected $_personModelName = '\common\local\local_models\mongodb\example\Person';
    protected $_personModel;
    
    public function init(){
        parent::init();
        list($this->_personModelName,$this->_personModel) = Yii::mapGet($this->_personModelName);  
    }
    
    public function getPrimaryKey()
    {
        return '_id';
    }

    public function getByPrimaryKey($primaryKey)
    {
        if ($primaryKey) {
            return $this->_personModel->findOne($primaryKey);
        } else {
            return new $this->_personModelName;
        }
    }
    
    /*
     * example filter:
     * [
     * 		'numPerPage' 	=> 20,
     * 		'pageNum'		=> 1,
     * 		'orderBy'	=> ['_id' => SORT_DESC, 'sku' => SORT_ASC ],
     * 		'where'			=> [
                ['>','price',1],
                ['<=','price',10]
     * 			['sku' => 'uk10001'],
     * 		],
     * 	'asArray' => true,
     * ]
     */
    public function coll($filter = '')
    {
        $query = $this->_personModel->find();
        $query = Yii::$service->helper->ar->getCollByFilter($query, $filter);

        return [
            'coll' => $query->all(),
            'count'=> $query->limit(null)->offset(null)->count(),
        ];
    }

    /**
     * @property $one|array
     * save $data to cms model,then,add url rewrite info to system service urlrewrite.
     */
    public function save($one, $originUrlKey)
    {
        $currentDateTime = \fec\helpers\CDate::getCurrentDateTime();
        $primaryVal = isset($one[$this->getPrimaryKey()]) ? $one[$this->getPrimaryKey()] : '';
        if ($primaryVal) {
            $model = $this->_personModel->findOne($primaryVal);
            if (!$model) {
                Yii::$service->helper->errors->add('article '.$this->getPrimaryKey().' is not exist');

                return;
            }
        } else {
            $model = new $this->_personModelName;
            $model->created_at = time();
            $model->created_user_id = \fec\helpers\CUser::getCurrentUserId();
            $primaryVal = new \MongoDB\BSON\ObjectId();
            $model->{$this->getPrimaryKey()} = $primaryVal;
        }
        $model->updated_at = time();
        unset($one['_id']);
        $this->initData($one);
        $saveStatus         = Yii::$service->helper->ar->save($model, $one);
        $model[$this->getPrimaryKey()] = (string)$model[$this->getPrimaryKey()];
        return $model->attributes;
    }
    
    public function initData(&$one){
        $one['sex'] = (int)$one['sex'];
        $one['age'] = (int)$one['age'];
    }
    
    /**
     * remove article.
     */
    public function remove($ids)
    {
        if (!$ids) {
            Yii::$service->helper->errors->add('remove id is empty');

            return false;
        }
        if (is_array($ids) && !empty($ids)) {
            $deleteAll = true;
            foreach ($ids as $id) {
                $model = $this->_personModel->findOne($id);
                if (isset($model[$this->getPrimaryKey()]) && !empty($model[$this->getPrimaryKey()])) {
                    $model->delete();
                } else {
                    //throw new InvalidValueException("ID:$id is not exist.");
                    Yii::$service->helper->errors->add("Person Remove Errors:ID $id is not exist.");
                    $deleteAll = false;
                }
            }
            return $deleteAll;
        } else {
            $id = $ids;
            $model = $this->_personModel->findOne($id);
            if (isset($model[$this->getPrimaryKey()]) && !empty($model[$this->getPrimaryKey()])) {
                $model->delete();
            } else {
                Yii::$service->helper->errors->add("Person Remove Errors:ID:$id is not exist.");

                return false;
            }
        }

        return true;
    }
}

```

3.3.2 PersonMysqldb

新建文件：`common\local\local_services\example\person\PersonMysqldb.php`，代码如下：


```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 * Example Person: 在本地开发一个后台编辑模块的例子，非fecshop功能模块
 */

namespace common\local\local_services\example\person;

use Yii;
use yii\base\InvalidValueException;
use fecshop\services\Service;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class PersonMysqldb extends Service implements PersonInterface
{
    public $numPerPage = 20;
    protected $_personModelName = '\common\local\local_models\mysqldb\example\Person';
    protected $_personModel;
    
    public function init(){
        parent::init();
        list($this->_personModelName,$this->_personModel) = Yii::mapGet($this->_personModelName);  
    }
    /**
     *  language attribute.
     */
    protected $_lang_attr = [
        'about_me',
    ];

    public function getPrimaryKey()
    {
        return 'id';
    }

    public function getByPrimaryKey($primaryKey)
    {
        if ($primaryKey) {
            $one = $this->_personModel->findOne($primaryKey);
            foreach ($this->_lang_attr as $attrName) {
                if (isset($one[$attrName])) {
                    $one[$attrName] = unserialize($one[$attrName]);
                }
            }

            return $one;
        } else {
            return new $this->_personModelName();
        }
    }
    
    

    /*
     * example filter:
     * [
     * 		'numPerPage' 	=> 20,
     * 		'pageNum'		=> 1,
     * 		'orderBy'	=> ['_id' => SORT_DESC, 'sku' => SORT_ASC ],
            'where'			=> [
                ['>','price',1],
                ['<=','price',10]
     * 			['sku' => 'uk10001'],
     * 		],
     * 	'asArray' => true,
     * ]
     */
    public function coll($filter = '')
    {
        $query = $this->_personModel->find();
        $query = Yii::$service->helper->ar->getCollByFilter($query, $filter);
        $coll = $query->all();
        if (!empty($coll)) {
            foreach ($coll as $k => $one) {
                foreach ($this->_lang_attr as $attr) {
                    $one[$attr] = $one[$attr] ? unserialize($one[$attr]) : '';
                }
                $coll[$k] = $one;
            }
        }
        //var_dump($one);
        return [
            'coll' => $coll,
            'count'=> $query->limit(null)->offset(null)->count(),
        ];
    }

    /**
     * @property $one|array
     * save $data to cms model,then,add url rewrite info to system service urlrewrite.
     */
    public function save($one, $originUrlKey)
    {
        $currentDateTime = \fec\helpers\CDate::getCurrentDateTime();
        $primaryVal = isset($one[$this->getPrimaryKey()]) ? $one[$this->getPrimaryKey()] : '';
        if ($primaryVal) {
            $model = $this->_personModel->findOne($primaryVal);
            if (!$model) {
                Yii::$service->helper->errors->add('person '.$this->getPrimaryKey().' is not exist');

                return;
            }
        } else {
            $model = new $this->_personModelName();
            $model->created_at = time();
            $model->created_user_id = \fec\helpers\CUser::getCurrentUserId();
        }
        //$this->initStatus($model);
        $model->updated_at = time();
        foreach ($this->_lang_attr as $attrName) {
            if (is_array($one[$attrName]) && !empty($one[$attrName])) {
                $one[$attrName] = serialize($one[$attrName]);
            }
        }
        $primaryKey = $this->getPrimaryKey();
        $model      = Yii::$service->helper->ar->save($model, $one);
        // 保存的数据格式返回
        foreach ($this->_lang_attr as $attr) {
            $model[$attr] = unserialize($model[ $attr]);
        }
        return $model->attributes;
    }
    
    //protected function initStatus($model){
    //    $statusArr = [$model::STATUS_ACTIVE, $model::STATUS_DELETED];
    //    if ($model['status']) {
    //        $model['status'] = (int) $model['status'];
    //        if (!in_array($model['status'], $statusArr)) {
    //            $model['status'] = $model::STATUS_ACTIVE;
    //        }
    //    } else {
    //        $model['status'] = $model::STATUS_ACTIVE;
    //    }
    //}

    public function remove($ids)
    {
        if (!$ids) {
            Yii::$service->helper->errors->add('remove id is empty');

            return false;
        }
        if (is_array($ids) && !empty($ids)) {
            
            foreach ($ids as $id) {
                $model = $this->_personModel->findOne($id);
                if (isset($model[$this->getPrimaryKey()]) && !empty($model[$this->getPrimaryKey()])) {
                    $model->delete();
                } else {
                    Yii::$service->helper->errors->add("Person Remove Errors:ID $id is not exist.");
                    
                    return false;
                }
            }
               
        } else {
            $id = $ids;
            $model = $this->_personModel->findOne($id);
            if (isset($model[$this->getPrimaryKey()]) && !empty($model[$this->getPrimaryKey()])) {
                $model->delete();
            } else {
                Yii::$service->helper->errors->add("Person Remove Errors:ID:$id is not exist.");

                return false;
            }
        }

        return true;
    }
    
}

```


至此，我们把model 和 services层都新建好了，下面我们可以开始写我们的模块了

4.模块部分


> 此处做的是appadmin端，做Person表数据的增删改查

4.1模块配置

新建文件：@appadmin/config/fecshop_local_modules/Person.php

加入模块配置：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 * 这是一个例子模块，用于展示一下如何二次开发，非fecshop必要模块
 */
return [
    'person' => [
        'class' => '\appadmin\local\local_modules\Person\Module',
    
    
    ],
];
```

4.2 编写模块代码

4.2.1 模块入口文件Module

新建文件：`appadmin\local\local_modules\Person\Module.php`

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace appadmin\local\local_modules\Person;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class Module extends \fec\AdminModule
{
    public function init()
    {
        //echo 1;exit;
        // 以下代码必须指定
        $this->controllerNamespace = __NAMESPACE__ . '\\controllers';
        $this->_currentDir = __DIR__;
        $this->_currentNameSpace = __NAMESPACE__;
        $this->blockNamespace = __NAMESPACE__ . '\\block';
        // 指定默认的man文件
        $this->layout = '/main_ajax.php';
        parent::init();
    }
    
}

```

4.2.2 新建模块controller基类

新建文件`appadmin\local\local_modules\Person\PersonController`

代码如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace appadmin\local\local_modules\Person;

/*
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
use fecadmin\FecadminbaseController;
use Yii;
use fecshop\app\appadmin\modules\AppadminController;

class PersonController extends AppadminController
{
    
}

```

5.在模块中新建我们的controller block view

5.1新建controller文件：`appadmin\local\local_modules\Person\controllers\IndexController.php`

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace appadmin\local\local_modules\Person\controllers;

use appadmin\local\local_modules\Person\PersonController;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class IndexController extends PersonController
{
    public function actionIndex()
    {
        $data = $this->getBlock()->getLastData();

        return $this->render($this->action->id, $data);
    }

    public function actionManageredit()
    {
        $data = $this->getBlock()->getLastData();

        return $this->render($this->action->id, $data);
    }

    public function actionManagereditsave()
    {
        $data = $this->getBlock('manageredit')->save();
    }

    public function actionManagerdelete()
    {
        $this->getBlock('manageredit')->delete();
    }
}

```

5.2 block部分：

5.2.1 新建文件`appadmin\local\local_modules\Person\block\index\Index.php`

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace appadmin\local\local_modules\Person\block\index;

use fec\helpers\CUrl;
use fecshop\app\appadmin\interfaces\base\AppadminbaseBlockInterface;
use fecshop\app\appadmin\modules\AppadminbaseBlock;
use Yii;

/**
 * block cms\article.
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class Index extends AppadminbaseBlock implements AppadminbaseBlockInterface
{
    /**
     * init param function ,execute in construct.
     */
    public function init()
    {
        /*
         * edit data url
         */
        $this->_editUrl = CUrl::getUrl('person/index/manageredit');
        /*
         * delete data url
         */
        $this->_deleteUrl = CUrl::getUrl('person/index/managerdelete');
        /*
         * service component, data provider
         */
        $this->_service = Yii::$service->person;
        parent::init();
    }

    public function getLastData()
    {

        // hidden section ,that storage page info
        $pagerForm = $this->getPagerForm();
        // search section
        $searchBar = $this->getSearchBar();
        // edit button, delete button,
        $editBar = $this->getEditBar();
        // table head
        $thead = $this->getTableThead();
        // table body
        $tbody = $this->getTableTbody();
        // paging section
        $toolBar = $this->getToolBar($this->_param['numCount'], $this->_param['pageNum'], $this->_param['numPerPage']);

        return [
            'pagerForm'        => $pagerForm,
            'searchBar'        => $searchBar,
            'editBar'        => $editBar,
            'thead'        => $thead,
            'tbody'        => $tbody,
            'toolBar'    => $toolBar,
        ];
    }

    /**
     * get search bar Arr config.
     */
    public function getSearchArr()
    {
        $data = [
            [    // selecit的Int 类型
                'type'=>'select',
                'title'=>'性别',
                'name'=>'sex',
                'columns_type' =>'int',  // int使用标准匹配， string使用模糊查询
                'value'=> Yii::$service->person->getSexArr(),
                //[                    // select 类型的值
                //    1=>'男',
                //    2=>'女',
                //    3=>'人妖',
                //],
            ],
            [    // 字符串类型
                'type'=>'inputtext',
                'title'=>'姓名',
                'name'=>'name',
                'columns_type' =>'string',
            ],
            [    // 时间区间类型搜索
                'type'=>'inputdatefilter',
                'name'=> 'created_at',
                'columns_type' =>'int',
                'value'=>[
                    'gte'=>'用户创建时间开始',
                    'lt' =>'用户创建时间结束',
                ],
            ],
            [    // 时间区间类型搜索
                'type'=>'inputfilter',
                'name'=> 'age',
                'columns_type' =>'int',
                'value'=>[
                    'gte'=>'年龄开始',
                    'lt' =>'年龄结束',
                ],
            ],
        ];

        return $data;
    }

    /**
     * config function ,return table columns config.
     */
    public function getTableFieldArr()
    {
        $table_th_bar = [
            [
                'orderField'    => $this->_primaryKey,
                'label'            => 'ID',
                'width'            => '50',
                'align'        => 'center',

            ],
            [
                'orderField'        => 'name',
                'label'             => '姓名',
                'width'             => '50',
                'align'             => 'left',
                'lang'              => false,
            ],
            [
                'orderField'        => 'age',
                'label'             => '年龄',
                'width'             => '50',
                'align'             => 'left',
                'lang'              => false,
            ],
            [
                'orderField'        => 'sex',
                'label'             => '性别',
                'width'             => '50',
                'align'             => 'center',
                'display'           => Yii::$service->person->getSexArr(),
            ],
            [
                'orderField'    => 'created_user_id',
                'label'            => '创建人',
                'width'            => '110',
                'align'        => 'center',
            ],
            [
                'orderField'    => 'created_at',
                'label'            => '创建时间',
                'width'            => '110',
                'align'        => 'center',
                'convert'        => ['int' => 'datetime'],
            ],
            [
                'orderField'    => 'updated_at',
                'label'            => '更新时间',
                'width'            => '110',
                'align'        => 'center',
                'convert'        => ['int' => 'datetime'],
            ],

        ];

        return $table_th_bar;
    }

    /**
     * rewrite parent getTableTbodyHtml($data).
     */
    public function getTableTbodyHtml($data)
    {
        $fileds = $this->getTableFieldArr();
        $str .= '';
        $csrfString = \fec\helpers\CRequest::getCsrfString();
        $user_ids = [];
        foreach ($data as $one) {
            $user_ids[] = $one['created_user_id'];
        }
        $users = Yii::$service->adminUser->getIdAndNameArrByIds($user_ids);
        foreach ($data as $one) {
            $str .= '<tr target="sid_user" rel="'.$one[$this->_primaryKey].'">';
            $str .= '<td><input name="'.$this->_primaryKey.'s" value="'.$one[$this->_primaryKey].'" type="checkbox"></td>';
            foreach ($fileds as $field) {
                $orderField = $field['orderField'];
                $display = $field['display'];
                $val = $one[$orderField];
                if ($orderField == 'created_user_id') {
                    $val = isset($users[$val]) ? $users[$val] : $val;
                    $str .= '<td>'.$val.'</td>';
                    continue;
                }
                if ($val) {
                    if (isset($field['display']) && !empty($field['display'])) {
                        $display = $field['display'];
                        $val = $display[$val] ? $display[$val] : $val;
                    }
                    if (isset($field['convert']) && !empty($field['convert'])) {
                        $convert = $field['convert'];
                        foreach ($convert as $origin =>$to) {
                            if (strstr($origin, 'mongodate')) {
                                if (isset($val->sec)) {
                                    $timestramp = $val->sec;
                                    if ($to == 'date') {
                                        $val = date('Y-m-d', $timestramp);
                                    } elseif ($to == 'datetime') {
                                        $val = date('Y-m-d H:i:s', $timestramp);
                                    } elseif ($to == 'int') {
                                        $val = $timestramp;
                                    }
                                }
                            } elseif (strstr($origin, 'date')) {
                                if ($to == 'date') {
                                    $val = date('Y-m-d', strtotime($val));
                                } elseif ($to == 'datetime') {
                                    $val = date('Y-m-d H:i:s', strtotime($val));
                                } elseif ($to == 'int') {
                                    $val = strtotime($val);
                                }
                            } elseif ($origin == 'int') {
                                if ($to == 'date') {
                                    $val = date('Y-m-d', $val);
                                } elseif ($to == 'datetime') {
                                    $val = date('Y-m-d H:i:s', $val);
                                } elseif ($to == 'int') {
                                    $val = $val;
                                }
                            } elseif ($origin == 'string') {
                                if ($to == 'img') {
                                    $t_width = isset($field['img_width']) ? $field['img_width'] : '100';
                                    $t_height = isset($field['img_height']) ? $field['img_height'] : '100';
                                    $val = '<img style="width:'.$t_width.'px;height:'.$t_height.'px" src="'.$val.'" />';
                                }
                            }
                        }
                    }

                    if (isset($field['lang']) && !empty($field['lang'])) {
                        //var_dump($val);
                        //var_dump($orderField);
                        $val = Yii::$service->fecshoplang->getDefaultLangAttrVal($val, $orderField);
                    }
                }
                $str .= '<td>'.$val.'</td>';
            }
            $str .= '<td>
						<a title="编辑" target="dialog" class="btnEdit" mask="true" drawable="true" width="1000" height="580" href="'.$this->_editUrl.'?'.$this->_primaryKey.'='.$one[$this->_primaryKey].'" >编辑</a>
						<a title="删除" target="ajaxTodo" href="'.$this->_deleteUrl.'?'.$csrfString.'&'.$this->_primaryKey.'='.$one[$this->_primaryKey].'" class="btnDel">删除</a>
					</td>';
            $str .= '</tr>';
        }

        return $str;
    }
}

```

5.2.1 新建文件`appadmin\local\local_modules\Person\block\index\Manageredit.php`

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace appadmin\local\local_modules\Person\block\index;

use fec\helpers\CRequest;
use fec\helpers\CUrl;
use fecshop\app\appadmin\interfaces\base\AppadminbaseBlockEditInterface;
use fecshop\app\appadmin\modules\AppadminbaseBlockEdit;
use Yii;

/**
 * block cms\article.
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class Manageredit extends AppadminbaseBlockEdit implements AppadminbaseBlockEditInterface
{
    public $_saveUrl;

    public function init()
    {
        $this->_saveUrl = CUrl::getUrl('person/index/managereditsave');
        parent::init();
    }

    // 传递给前端的数据 显示编辑form
    public function getLastData()
    {
        return [
            'editBar'     => $this->getEditBar(),
            'textareas'   => $this->_textareas,
            'lang_attr'   => $this->_lang_attr,
            'saveUrl'     => $this->_saveUrl,
        ];
    }

    public function setService()
    {
        $this->_service = Yii::$service->person;
    }

    public function getEditArr()
    {
        return [
            [
                'label'=>'姓名',
                'name'=>'name',
                'display'=>[
                    'type' => 'inputString',
                    'lang' => false,  // 不是多语言属性
                ],
                'require' => 1,
            ],
            
            [
                'label'=>'性别',
                'name'=>'sex',
                'display'=>[
                    'type' => 'select',
                    'data' => Yii::$service->person->getSexArr(),
                    //[
                    //    1    => '激活',
                    //    2    => '关闭',
                    //],
                ],
                'require' => 1,
                'default' => 1,
            ],

            [
                'label'=>'年龄',
                'name'=>'age',
                'display'=>[
                    'type' => 'inputString',
                ],
                'require' => 0,
            ],

            [
                'label'=>'公司',
                'name'=>'company',
                'display'=>[
                    'type' => 'inputString',
                    'lang' => false,
                ],
                'require' => 0,
            ],

            [
                'label'=>'介绍自己',
                'name'=>'about_me',
                'display'=>[
                    'type' => 'textarea',
                    'lang' => true,
                    'rows'    => 14,
                    'cols'    => 110,
                ],
                'require' => 0,
            ],
            
            [
                'label'=>'电话',
                'name'=>'telephone',
                'display'=>[
                    'type' => 'inputString',
                    'lang' => false,
                ],
                'require' => 0,
            ],
            
            
            
        ];
    }

    /**
     * save article data,  get rewrite url and save to article url key.
     */
    public function save()
    {
        $request_param = CRequest::param();
        $this->_param = $request_param[$this->_editFormData];
        /*
         * if attribute is date or date time , db storage format is int ,by frontend pass param is int ,
         * you must convert string datetime to time , use strtotime function.
         */
        $this->_service->save($this->_param, 'person/index/index');
        $errors = Yii::$service->helper->errors->get();
        if (!$errors) {
            echo  json_encode([
                'statusCode'=>'200',
                'message'=>'save success',
            ]);
            exit;
        } else {
            echo  json_encode([
                'statusCode'=>'300',
                'message'=>$errors,
            ]);
            exit;
        }
    }

    // 批量删除
    public function delete()
    {
        $ids = '';
        if ($id = CRequest::param($this->_primaryKey)) {
            $ids = $id;
        } elseif ($ids = CRequest::param($this->_primaryKey.'s')) {
            $ids = explode(',', $ids);
        }
        $this->_service->remove($ids);
        $errors = Yii::$service->helper->errors->get();
        if (!$errors) {
            echo  json_encode([
                'statusCode'=>'200',
                'message'=>'remove data  success',
            ]);
            exit;
        } else {
            echo  json_encode([
                'statusCode'=>'300',
                'message'=>$errors,
            ]);
            exit;
        }
    }
}

```

5.3 theme（view）文件

5.3.1新建文件：appadmin/theme/local/theme01/person/index/index.php

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
use fec\helpers\CRequest;
/** 
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
?>
<form id="pagerForm" method="post" action="<?= \fec\helpers\CUrl::getCurrentUrl();  ?>">
	<?=  CRequest::getCsrfInputHtml();  ?>
	<?=  $pagerForm;  ?>
</form>
<div class="pageHeader">
	<form rel="pagerForm" onsubmit="return navTabSearch(this);" action="<?= \fec\helpers\CUrl::getCurrentUrl();  ?>" method="post">
		<?php echo CRequest::getCsrfInputHtml();  ?>
		<div class="searchBar">
			<?php  echo $searchBar; ?>
		</div>
	</form>
</div>
<div class="pageContent">
	<div class="panelBar">
		<?= $editBar;  ?>
	</div>
	<div class="panelBar">
		<?= $toolBar; ?>
	</div>
	<table class="table" width="100%" layoutH="138">
		<?= $thead; ?>
		<tbody>
			<?= $tbody; ?>
		</tbody>
	</table>
	
</div>
<style>
.textInput{width:90px;}
</style>
```

5.3.2新建文件：appadmin/theme/local/theme01/person/index/manageredit.php



```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
use yii\helpers\Html;
use fec\helpers\CRequest;
use fecadmin\models\AdminRole;
/** 
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
?>
<style>
.checker{float:left;}
.dialog .pageContent {background:none;}
.dialog .pageContent .pageFormContent{background:none;}
</style>

<div class="pageContent"> 
	<form  method="post" action="<?= $saveUrl ?>" class="pageForm required-validate" onsubmit="return validateCallback(this, dialogAjaxDoneCloseAndReflush);">
		<?php echo CRequest::getCsrfInputHtml();  ?>	
		<div layouth="56" class="pageFormContent" style="height: 240px; overflow: auto;">
			
				<input type="hidden"  value="<?=  $product_id; ?>" size="30" name="product_id" class="textInput ">
				
				<fieldset id="fieldset_table_qbe">
					<legend style="color:#cc0000">编辑信息</legend>
					<div>
						<?= $editBar; ?>
						
						
						
						
					</div>
				</fieldset>
				
				
				<?= $lang_attr ?>
				
				<?= $textareas ?>
				
				
		</div>
	
		<div class="formBar">
			<ul>
				<!--<li><a class="buttonActive" href="javascript:;"><span>保存</span></a></li>-->
				<li><div class="buttonActive"><div class="buttonContent"><button onclick="func('accept')"  value="accept" name="accept" type="submit">保存</button></div></div></li>
			
				<li>
					<div class="button"><div class="buttonContent"><button type="button" class="close">取消</button></div></div>
				</li>
			</ul>
		</div>
	</form>
</div>	


```


至此，我们把需要的代码文件都新建好了，我们需要去后台新建菜单


设置菜单权限可以参看文档：http://www.fecshop.com/topic/437

在用户管理下面新建菜单，如图：

![](images/r1.png)

关于后台加入菜单，以及设置权限可以参看文档：http://www.fecshop.com/topic/437

然后把菜单加入到权限组，然后刷新缓存，刷新浏览器，就可以看到菜单了，
然后访问这个菜单就可以看到我们做的增删改查列表，并且带有搜索，排序，分页等
功能，如图：

![](images/r2.png)

![](images/r3.png)

到这里就完成了，您参考这个例子，可以开发您的业务了。



