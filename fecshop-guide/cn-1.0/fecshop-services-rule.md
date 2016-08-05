Fecshop Service 规则
====================

遵守规则：

1. Service里面的变量，需要外部注入数值，因此，需要是public
但是，按照service对的规则，service的成员变量不能直接外部访问，必须通过get set方法
调用，这是为了日后的扩展，

2. service里面的所有方法必须是protected声明（一些特殊的fecshop系统service除外）
,如果service的一个方法允许外部访问，则前面加入action，方法的首字母大写，譬如 ：
`Yii::$service->url->getUrl();`
在url service里面的函数命名为  `protected function actionGetUrl()`

如果这个方法不允许外部访问，则按照原来的即可，不需要加action。
这样就即可 `protected function getUrl()`

3. service 返回的数据可以是字符串，数组，数组，但是不能是对象，这个是为了以后的重构考虑，











