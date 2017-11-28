Fecshop 多语言
================

> fecshop 支持多语言翻译，可以通过多个途径进行语言的切换，一共分为四个大部分：
> 数据库数据的翻译，网页内容数据的翻译，网站提示和报错等信息的翻译，邮件内容的
> 语言翻译，当您为一个store指定了语言，那么就会按照上面四种途径进行相应的语言翻译，
> ,进而形成对应语言的翻译语言。

一：语言的配置
--------------


在fecshop FecshopLang 服务 中可以配置语言选项，你可以在
`@common/config/fecshop_local_services/FecshopLang.php` 中进行配置语言项，譬如：

```
'fecshoplang' => [
	//'class' => 'fecshop\services\FecshopLang',
	//  mongoSearchLangName 在各个语言下字段参考资料如下：（不支持中文）
	//  https://docs.mongodb.com/manual/reference/text-search-languages/#text-search-languages
	'allLangCode' => [
		# 'en_US' 是标准语言简码  code对应的值en取 “标准语言简码”的前两位字符，
		# 该值设置后，进行了产品分类数据的添加后，不能修改，否则会出现部分翻译语言丢失。
		'en_US' => [
			'code' 					=> 'en',
		],
		'fr_FR' => [
			'code' 					=> 'fr',
		],
		'de_DE' => [
			'code' 					=> 'de',
		],
		'es_ES' => [
			'code' 					=> 'es',
		],
		'ru_RU' => [
			'code' 					=> 'ru',
		],
		'pt_PT' => [
			'code' 					=> 'pt',
		],
		'zh_CN' => [
			'code' 					=> 'zh',
		],
	],
	# 默认语言。
	'defaultLangCode' => 'en',
	
],

```

上面是fecshop默认的几个语言配置，您可以根据自己的业务需求进行语言的设置和添加。

fecshop的每个store设置的不同语言，以及对应的产品搜索(mongodb full search需要根据语言进行切词)，都要依赖上面的配置。

[语言简码表](http://blog.csdn.net/wed110/article/details/50886195)




二：翻译
---------

### 数据库数据

数据库中的数据，譬如产品表中的产品名字，产品描述等，分类表中的分类名字和分类描述，
在数据库表中都是保存了多份语言数据

![Alt text](images/11.jpg)

![Alt text](images/22.jpg)

在网站前台展示数据的时候，根据当前的store设置的语言，将相应语言的数据取出来展示即可。
如果相应语言的值在数据库中没有添加，那么将会把默认语言的值取出来作为当前语言的值。

### 网页内容语言的翻译

网站内容语言的翻译，是依靠的翻译文件，在实现方面依赖的`Yii::t()`函数，关于
Yii2多语言翻译的知识，可以参看地址 [Yii2多语言](http://www.yiichina.com/doc/guide/2.0/tutorial-i18n)

### Fecshop的翻译文件路径为：（举例appfront入口）

`@vendor/fancyecommerce/fecshop/app/appfront/languages/`，在这个文件夹下面可以看到
各个语言的文件包，进入相应语言，就可以看到翻译文件，譬如中文的翻译文件路径为
：`@vendor/fancyecommerce/fecshop/app/appfront/languages/zh_CN/appfront.php`
，在这个文件里面就可以看到所有的中文翻译内容，如果您想重写或者添加新
的翻译，可以到 `@appfront/languages/zh_CN/appfront.php` 中添加或者重写翻译
数组，注意，这里使用的是php的数组，需要按照相应格式填写，否则会报错。

在翻译文件中，您可能看到这样的带有**{}**的部分，譬如下面的 `{passwdMinLength}`,
这是一个动态变量，这个请不要翻译和做其他的任何改动，直接复制上去即可，譬如下面的
翻译，这个值是由php动态计算而来。

```
 'Password length must be greater than or equal to {passwdMinLength}'
								=> '密码长度必须大于或等于{passwdMinLength}',
 'Password length must be less than or equal to {passwdMaxLength}'	
								=> '密码长度必须小于或等于{passwdMaxLength}',
 'The passwords are inconsistent'	
								=> '密码不一致',
```

### 提示报错信息的翻译

在网站顶部，会出现一些提示信息和报错信息，譬如您注册邮箱的时候，会提示你的格式不正确等，
这些数据也是用翻译文件的方式，方法上上面类似，都是在一个同一个文件中
添加翻译内容,方法和方式同上。

### 邮件内容的翻译

邮件内容的模板，是在theme中，譬如appfront的邮件模板，是在
`@fecshop/app/appfront/theme/base/default/mailer`下面,其中,
`@fecshop/app/appfront/theme`是模板文件夹路径，`base`是模板包名，
`default`是模板名，`mailer`是邮件theme文件夹，在mailer路径下，打开
`customer/account/forgotpassword`,里面是用户忘记密码发送的邮件，
其中s`ubject_`开头的都是邮件的标题，`body_`开头的都是邮件的内容
`en`结尾的代表英文语言的邮件，`zh`结尾的代表中文语言的邮件，打开相应文件
从`en`复制一份到对应的语言，然后修改里面的语言即可，
有一些语言，里面没有对应的文件，您新建即可。

添加或者修改邮件内容，举例：

如果您想修改 `@fecshop/app/appfront/theme/base/default/mailer/customer/account/forgotpassword/body_zh.php`,
里面的内容，你可以在 `@appfront/theme/terry/theme01/里面新建文件 mailer/customer/account/forgotpassword/body_zh.php`（如果存在，则不需要创建）
然后将上面的文件内容复制到新建的文件中，进行修改即可，这样就完成了邮件内容的添加或者重写。


通过以上四种方式的翻译，我们就完成了整个fecshop多语言翻译的闭环。

**注意：** 如果您不添加翻译，则默认就会使用英语的翻译。

关于邮件更详细的介绍，可以参看：[Fecshop 邮件](fecshop_email.php)
 

三：各个入口的语言配置
--------------

> 当我们在上面的步骤中设置了语言，以及各个语言对应的翻译文件后，
> 我们需要为各个入口设置对应的默认语言


### 设置各个域名下面的默认语言

打开 @app/config/fecshop_local_services/Store.php

```
<?php
   return [
   'store' => [
        'class'  => 'fecshop\services\Store',
        'stores' => [
            // store key：域名去掉http部分，作为key，这个必须这样定义。
            'fecshop.appfront.fancyecommerce.com' => [
                'language'         => 'en_US',        // 语言简码需要在@common/config/fecshop_local_services/FecshopLang.php 中定义。
                'languageName'     => 'English',    // 语言简码对应的文字名称，将会出现在语言切换列表中显示。
                'localThemeDir'    => '@appfront/theme/terry/theme01', // 设置当前store对应的模板路径。关于多模板的方面的知识，您可以参看fecshop多模板的知识。
                'thirdThemeDir'    => [],  // 第三方模板路径，数组，可以多个路径
                'currency'         => 'USD', // 当前store的默认货币,这个货币简码，必须在货币配置中配置
                /*
                 * 当设备满足什么条件的时候，进行跳转。
                 * 这种方式不怎么高效，最好的方式是在nginx中配置。
                 */
                ...
```

设置：

`language` ：第一部分中， `@common/config/fecshop_local_services/FecshopLang.php` 中进行配置语言项，
这里填写的值，必须该配置文件中出现。

`languageName` 自定义语言label，这个会在前端显示出来具体的名字（因为简码，用户
是看不明白的），譬如在appfront端的顶部左侧显示的多语言切换列表，apphtml5端
首页底部显示的多语言切换列表

然后就可以访问查看了，当把该入口的各个域名对应的默认语言设置好后，
访问这个语言，就可以看到相应的语言了。




