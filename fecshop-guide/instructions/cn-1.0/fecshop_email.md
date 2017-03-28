Fecshop 邮件
============

> 当用户注册邮箱，下单，忘记密码等，都会给用户发送一封邮件，邮件部分
> 支持多语言。

### SMTP配置文件为：

`@common/config/fecshop_local_services/Email.php`

配置如下：

```
return [
	'email' => [
		'mailerConfig' => [
			# 默认通用配置
			'default' => [
				'class' => 'yii\swiftmailer\Mailer',
				'transport' => [
					'class' => 'Swift_SmtpTransport',
					'host' => 'smtp.qq.com',			#SMTP Host
					'username' => '372716335@qq.com',   #SMTP 账号
					'password' => 'wffmbummgnhhcbbj',	#SMTP 密码
					'port' => '587',					#SMTP 端口
					'encryption' => 'tls',
				],
				'messageConfig'=>[  
				   'charset'=>'UTF-8',  
				], 
			],
        ],
	],
];
```

对于上面配置中的的 `mailerConfig`，除了`default`，您还可以继续添加其他的SMTP
配置，

您只要配置完上面的文件，就把smtp配置好了。

### 邮件模板配置

fecshop的配置文件为：`@fecshop/config/services/Email.php`

在邮件模板里面可以指定使用上面配置文件中的mailerConfig里面的
`数组key`，譬如`default`。


以`Yii::$service->email->customer`为例，里面的`mailerConfig`
可以使用上面配置的值，譬如下面配置中使用的`'mailerConfig'  => 'default'`



```
'customer' => [
	'class' => 'fecshop\services\email\Customer',
	
	# 各个邮件的模板部分：
	'emailTheme' => [
		# 注册账户发送的邮件的模板配置
		'register' => [
			'enable' => true,
			# 邮件内容的动态数据提供部分
			'widget'		=> 'fecshop\services\email\widgets\customer\account\register\Body',
			# 邮件内容的view部分
			'viewPath' 		=> '@fecshop/services/email/views/customer/account/register',
			/**
			 * 1.默认是default，譬如下面的 'mailerConfig'  => 'default',你可以不填写，因为默认就是default
			 * 2.您可以使用上面email服务的配置项mailerConfig中的设置的各个项，譬如填写default 或者 login等。
			 * 3.您还可以直接填写数组的配置（完整配置），譬如：
			 * 'register' => [
			 *		'class' => 'yii\swiftmailer\Mailer',
			 *		'transport' => [
			 *			'class' => 'Swift_SmtpTransport',
			 *			'host' => 'smtp.qq.com',
			 *			'username' => '372716335@qq.com',
			 *			'password' => 'wffmbummgnhhcbbj',
			 *			'port' => '587',
			 *			'encryption' => 'tls',
			 *		],
			 *		'messageConfig'=>[  
			 *		   'charset'=>'UTF-8',  
			 *		], 
			 *		
			 *	],
			 */
			'mailerConfig'  => 'default',
		],
		# 登录用户发送邮件的模板的设置。
		'login' => [
			'enable' => true,
			# 邮件内容的动态数据提供部分
			'widget'		=> 'fecshop\services\email\widgets\customer\account\login\Body',
			# 邮件内容的view部分
			'viewPath' 	=> '@fecshop/services/email/views/customer/account/login',
			# 如果不定义 mailerConfig，则会使用email service里面的默认配置
			'mailerConfig'  => 'default',
		],
		# 忘记密码发送邮件的模板的设置
		'forgotPassword' => [
			'enable' => true,
			'widget'		=> 'fecshop\services\email\widgets\customer\account\forgotpassword\Body',
			# 邮件内容的view部分
			'viewPath' 	=> '@fecshop/services/email/views/customer/account/forgotpassword',
			#忘记密码邮件发送后的超时时间。
			'passwordResetTokenExpire' => 86400, # 3600*24*1, # 一天
			# 如果不定义 mailerConfig，则会使用email service里面的默认配置
			# 通过邮箱找回密码，发送的resetToken过期的秒数
			'mailerConfig'  => 'default',
		],
		# 联系我们发送的邮件模板
		'contacts' => [
			'enable' => true,
			# 联系我们的邮箱地址
			
			# widget  邮件动态数据提供部分。
			'widget'		=> 'fecshop\services\email\widgets\customer\contacts\Body',
			# 邮件内容的view部分
			'viewPath' 	=> '@fecshop/services/email/views/customer/contacts',
			'address'	=> '2358269014@qq.com',
			# 如果不定义 mailerConfig，则会使用email service里面的默认配置
			//'mailerConfig'  => 'default',
		],
		# 订阅newsletter后发送的邮件模板。
		'newsletter' => [
			# 订阅邮件成功后，是否发送邮件给用户
			'enable'	=> true,
			# widget  邮件动态数据提供部分。
			'widget'		=> 'fecshop\services\email\widgets\customer\newsletter\Body',
			# 邮件内容的view部分
			'viewPath' 	=> '@fecshop/services/email/views/customer/newsletter',
			# 如果不定义 mailerConfig，则会使用email service里面的默认配置
			'mailerConfig'  => 'default',
		],
	],
],
```

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

如果您想重写邮件的内容，那么您在配置中重新指定`viewPath`和`widget`
的值，在路径中重新写`subject`和`body`文件即可。











































