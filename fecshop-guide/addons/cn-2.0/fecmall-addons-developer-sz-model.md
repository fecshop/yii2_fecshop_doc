Fecmall-model部分
=========

> fecmall model的介绍，使用，fecmall的model，本质就是yii2框架的models


### Fecmall-model部分

1.当我们新建了一个表，就要为这个表建立model。


譬如：


```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace fecerp\models\mysqldb;

use yii\db\ActiveRecord;
use yii\base\InvalidValueException;
/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class Task extends ActiveRecord
{
    const STATUS_INIT  = 1;
    const STATUS_BEGIN = 2;
    const STATUS_COMPLETE = 3;
    const STATUS_CANCEL = 4;
    
    public static function tableName()
    {
        return '{{%erp_task}}';
    }
    
}

```


2.services中引入model

在service里面引入models即可，譬如：https://github.com/fecshop/yii2_fecshop/blob/master/services/cart/Quote.php#L52

```
    protected $_cartModelName = '\fecshop\models\mysqldb\Cart';

    protected $_cartModel;

    public function init()
    {
        parent::init();
        list($this->_cartModelName, $this->_cartModel) = Yii::mapGet($this->_cartModelName);
    }
```

为什么在service使用model，需要使用`Yii::mapGet()`? , 这样做，是为了重写model，通过该函数先
从配置里面查看是否存在重写，如果存在重写就会使用重写后的model

3.model重写

可以通过`fecRewriteMap`机制，在扩展插件中重写fecmall的原有的services


```
 'common' => [
    'enable' => true,
    // 公用层的具体配置下载下面
    'config' => [
        
        'fecRewriteMap' => [
            '\fecshop\models\mongodb\Product'  => '\fecyo\models\mongodb\Product',
            '\fecshop\models\mysqldb\customer\Address'  => '\fecyo\models\mysqldb\customer\Address',
            '\fecshop\models\mysqldb\Order'  => '\fecyo\models\mysqldb\Order',
            
            '\fecshop\models\mysqldb\customer\CustomerRegister'  => '\fecyo\models\mysqldb\customer\CustomerRegister',
            '\fecshop\models\mysqldb\customer\CustomerLogin'  => '\fecyo\models\mysqldb\customer\CustomerLogin',
            '\fecshop\models\mysqldb\Customer'  => '\fecyo\models\mysqldb\Customer',
            
        ],
    ],
],
```

左边是原来的model，右边是重写后的model



### model rules


model rules是规则验证，是yii2的知识，详细参看yii2文档:
[Yii2 model 验证规则rules](https://www.yiichina.com/doc/guide/2.0/structure-models#validation-rules)


更多的关于yii2 models的知识，请参看：[Yii2 model](https://www.yiichina.com/doc/guide/2.0/structure-models#validation-rules)














