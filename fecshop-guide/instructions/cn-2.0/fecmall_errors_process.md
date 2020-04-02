fecmall 错误处理：model errors， helper errors services，以及page message services error处理
================



> Fecmall的错误处理机制讲解，对各个部分的错误处理原理，以及传递的详细说明



### fecmall 错误处理概览：


fecmall 在错误处理方面，有三个部分：

1.`model errors`:yii2框架的 model 错误处理部分

2.`helper errors services`：fecmall services的错误处理部分

3.`page message services`：fecmall对于前端商城显示的`错误提示`信息 和 `成功提示` 信息，进行的处理部分



### fecmall 错误处理详细讲解：



1.`model errors`： yii2的model，yii2框架层面，已经对models error进行了实现，当进行rules验证，model保存等，当出现报错的情况，可以通过`$errors = $model->errors;`进行获取



1.1model rules定义

对于model定义：https://github.com/fecshop/yii2_fecshop/blob/master/models/mysqldb/customer/CustomerRegister.php#L29

```
public function rules()
    {
        $parent_rules = parent::rules();
        $current_rules = [
            ['id', 'filter', 'filter' => 'trim'],
            ['email', 'filter', 'filter' => 'trim'],
            ['email', 'email'],
            ['email', 'validateEmail'],

            ['password', 'filter', 'filter' => 'trim'],
            ['password', 'string', 'length' => [6, 30]],
            // 注册账户，名字不作为必填选项
            ['firstname', 'filter', 'filter' => 'trim'],
            // ['firstname', 'string', 'length' => [1, 50]],
             // 注册账户，名字不作为必填选项
            ['lastname', 'filter', 'filter' => 'trim'],
            // ['lastname', 'string', 'length' => [1, 50]],
            
            ['is_subscribed', 'validateIsSubscribed'],
        ];

        $rules = array_merge($parent_rules, $current_rules);
        if (is_array($this->_rules)) {
            $rules = array_merge($rules, $this->_rules);
        }

        return $rules;
    }
```

1.2进行rules验证，并且获取验证后的报错信息：譬如：https://github.com/fecshop/yii2_fecshop/blob/master/services/Customer.php#L219


```
$model = $this->_customerRegisterModel;
$model->attributes = $param;
if (!$model->validate()) {
    $errors = $model->errors;
    Yii::$service->helper->errors->addByModelErrors($errors);

    return false;
}
```

可以看到，通过`$errors = $model->errors;`进行获取rules的验证的报错信息

1.3对于model保存信息，发生报错，也是这样获取:https://github.com/fecshop/yii2_fecshop/blob/master/services/Customer.php#L204


```
$saveStatus = $model->save();
            if (!$saveStatus) {
                $errors = $model->errors;
                Yii::$service->helper->errors->addByModelErrors($errors);
                
                return false;
            }
```

通过上面我们可以看到，操作yii2框架的model，报错信息都是通过`$errors = $model->errors;`来获取


2.`fecmall helper errors services`:fecmall services的错误处理部分

fecmall在架构方面，controller block不能直接调用model，需要先调用services，然后由services调用model，来处理中间逻辑，因此services需要有单独的错误处理机制

`helper errors services`，也就是类： https://github.com/fecshop/yii2_fecshop/blob/master/services/helper/Errors.php

打开这个类，可以看到里面的相应的逻辑（fecmall的services，都是`懒加载`模式的，`单例模式`对象）

2.1对于逻辑处理的错误添加到helper errors services，譬如：https://github.com/fecshop/yii2_fecshop/blob/master/services/Customer.php#L374


```
Yii::$service->helper->errors->add('Password length must be greater than 6, less than 30');
```

这些错误一般是，在services逻辑处理过程中，因为传递参数问题，数据库数据异常等原因导致的，程序报错，中断退出的错误.

2.2Yii2框架的`model errors`加入`helper errors services`

```
$errors = $model->errors;
Yii::$service->helper->errors->addByModelErrors($errors);
```

2.3错误加入`helper errors services`后，service报错退出，上层（譬如controller，block层）调用services的函数返回false，那么就可以通过函数获取报错信息

```
Yii::$service->helper->errors->get(',');  // 以多个报错信息，用逗号隔开
```

2.4`helper errors services`，加入了翻译机制，您可以根据需要加入翻译

2.5总结：`helper errors services`是捕捉services方法调用过程中的报错信息，供调用层（controller，block层）查看报错信息，然后进行错误的处理

譬如appfront apphtml5的web等，可能输出到错误显示部分，console层命令行输出报错信息，等等

3.`page message services`：基于浏览器层的提示信息显示（成功信息和错误信息，该部分功能，是针对前端商城页面显示的提示信息，譬如注册账户，注册功能信息，或者注册失败的提示信息等）

对于appfront，apphtml5这2个层面，是面向pc浏览器，和手机浏览器的入口，报错信息部分，fecmall通过 `page message services`部分进行处理：https://github.com/fecshop/yii2_fecshop/blob/master/services/page/Message.php

3.1对于商城的`提示信息显示`（`成功`信息和`错误`信息）,一般只显示一次，即进行销毁，譬如注册用户，显示注册成功，刷新页面后不会继续限制，fecmall是通过`yii flash session`来实现的

关于`yii flash session`： https://www.yiichina.com/doc/guide/2.0/runtime-sessions-cookies#flash-data

3.2我们可以通过`addError`方法
，进行添加`错误提示`信息：
https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/modules/Customer/block/account/Register.php#L60

```
Yii::$service->page->message->addError(['Captcha can not empty']);
```

3.3我们可以通过`addCorrect`方法
，进行添加 `成功提示` 信息：
https://github.com/fecshop/yii2_fecshop/blob/8bcfc0a9b652d6e1ee57334ec653e449681ead58/app/appfront/modules/Customer/block/editaccount/Index.php#L95

```
Yii::$service->page->message->addCorrect('edit account info success');
```
 
3.4在商城部分显示`错误提示`信息 和 `成功提示` 信息

https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/theme/base/front/customer/account/register.php#L12

```
<?= Yii::$service->page->widget->render('base/flashmessage'); ?>
```

3.4.1部分代码实现，追踪该部分 `base/flashmessage` 配置，通过配置查看对应view文件路径

https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/config/appfront.php#L154

```
'flashmessage' => [
    'view'  => 'widgets/flashmessage.php',
],
```

view文件路径为：`widgets/flashmessage.php`

3.4.2然后去找这个view文件

https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/theme/base/front/widgets/flashmessage.php

详细代码如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
?>
<?php 	$corrects = Yii::$service->page->message->getCorrects(); ?>
<?php 	$errors   = Yii::$service->page->message->getErrors(); ?>
<?php 	if((is_array($corrects) && !empty($corrects)) || (is_array($errors) && !empty($errors)   )):  ?>
		<div class="fecshop_message">
<?php 		if(is_array($corrects) && !empty($corrects)):  ?>
<?php 			foreach($corrects as $one): ?>
				<div class="correct-msg">
					<div><?= Yii::$service->page->translate->__($one); ?></div>
				</div>
<?php			endforeach; ?>
<?php		endif; ?>
<?php 		if(is_array($errors) && !empty($errors)):  ?>
<?php 			foreach($errors as $one): ?>
				<div class="error-msg">
					<div><?= Yii::$service->page->translate->__($one); ?></div>
				</div>
<?php			endforeach; ?>
<?php		endif; ?>
		</div>
<?php 	endif; ?>
```

也就是通过`$corrects = Yii::$service->page->message->getCorrects();`取出来`成功提示` 信息

也就是通过`$errors   = Yii::$service->page->message->getErrors();`取出来`错误提示` 信息

OK, femmall这三者的报错信息部分的处理逻辑，已经完全讲述清楚。


























