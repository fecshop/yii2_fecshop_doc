Fecshop Helper 服务
===================

Helper是一些帮助服务。

1.AR子服务

ActiveRecord服务。对Ar的一些常规快捷操作。


2.Errors子服务

用来保存各个服务在执行过程中的报错，
在执行过程中，可以通过`Yii::$service->helper->errors->add($str)`来
增加错误信息，可以通过 `Yii::$service->helper->errors->get()`来获取
错误信息，如果没有报错信息，则返回为空。


3.MobileDetect子服务

判断是否是手机设备，用来在pc端跳转到手机端。


