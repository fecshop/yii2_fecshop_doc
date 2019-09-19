Fecmall 邮件
============

> 当用户注册邮箱，下单，忘记密码等，都会给用户发送一封邮件，邮件部分
> 支持多语言。

Fecmall后台设置邮件


![xx](images/af2.png)




### 邮件模板配置介绍，以及邮件多语言原理



`viewPath` 就是邮件模板html部分 ， `widget`是动态数据提供部分。


对于邮件模板 ， `widget` （动态数据） 和 `viewPath`（静态文件）
功能形成了模板内容。

`widget` 对应的是动态数据的php对象，譬如：` 'widget'		=> 'fecshop\services\email\widgets\customer\newsletter\Body' `
对应的是`@fecshop\services\email\widgets\customer\newsletter\Body.php`文件

`view`是html部分的路径，在该路径下面需要有`subject`（邮件标题）和`body`（邮件内容）两个部分，然后加上语言，
譬如：`@fecshop/services/email/views/customer/newsletter`下面有
`subject_en.php`和`body_en.php`两个文件，代表英文语言的邮件标题和邮件内容，
你可以添加subject_fr.php和body_fr.php两个文件，代表
法文状态下的邮件标题和邮件内容。

如果您想要得到法文的邮件，但是没有subject_fr.php 和 body_fr.php
文件，那么，系统会使用默认语言的邮件，也就是subject_en.php
和body_en.php



### 邮件重写


> 如果您想重写邮件的内容，那么您在后台配置部分重新指定`viewPath`和`widget`
> 的值，在路径中重新写`subject`和`body`文件即可。


譬如重写登录发送邮件的模板:

您可以新建一个`widget` 继承`fecshop\services\email\widgets\customer\account\login\Body`,
来实现`widget`的重写。

对于view文件，可以新建一个`viewPath`，然后把
`@fecshop/services/email/views/customer/account/login` 里面的所有文件复制
到本地的`viewPath`中，然后重写即可。








































