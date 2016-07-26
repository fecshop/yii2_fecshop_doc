Fecshop view layout重写
=======================

> 在不修改重写fecshop的view和layout文件，
> 对于view layout 重写的原理，可以参考[Fecshop 多模板原理](fecshop-feature-mutil-themes.md)

### 1.多模板路径介绍。

多模板，针对的是前端应用，譬如appfront，下面就以appfront为例子。
对于前端，一般有多个入口，或者同一个入口，多个域名，最终
的体现，都是多个store，在store的配置文件中，配置了
当前store的 localThemeDir 和 thirdThemeDir，代码如下：


```
<?php
   return [
   'store' => [
		'class' => 'fecshop\services\Store',
		'stores' => [
			# store_code ,define by domain and fold.
			# 语言必须在fecshoplang中定义，否则将无法得到语言属性。
			# 在添加store的时候，必须查看 添加的语言在 fecshoplang中是否定义。
			'fecshop.appfront.fancyecommerce.com' => [
				'language' 		=> 'en_US',
				'languageName' 	=> 'English',
				
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'USD',
			],
			'fecshop.appfront.fancyecommerce.com/fr' => [
				'language' 		=> 'fr_FR',
				'languageName' 	=> 'Fran?ais',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'RMB',
			],
```

这样就有了各个优先级不同的多模板，对于多模板的细致原理，
参考 [fecshop多模板](fecshop-feature-mutil-themes.md),

首先，查看appfront应用 下 核心模板路径

fecshop\app\appfront\modules\AppfrontController

这个是appfront的base controller，所有的controller
都继承于它，在init方法中可以看到：

```
Yii::$service->page->theme->fecshopThemeDir = Yii::getAlias(CConfig::param('appfrontBaseTheme'));
```

在@fecshop\app\appfront\config\appfront.php中可以看到配置：

```
'appfrontBaseTheme' 	=> '@fecshop/app/appfront/theme/base/front',
```

因此，fecshop的模板路径为：@fecshop/app/appfront/theme/base/front
这个模板路径下面的文件是最全面的，但是优先级最低。


现在回去看上面的的store配置部分：

```
'fecshop.appfront.fancyecommerce.com' => [
				'language' 		=> 'en_US',
				'languageName' 	=> 'English',
				
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'USD',
			],
```


thirdThemeDir 代表你安装的（composer），也就是
别人开发的模板，你直接套用，可以在这里设置对应模板
的路径，这里是可以设置多个模板路径，
通过数组的方式添加进去。

localThemeDir 代表的是本地二次开发用户的模板路径
，有限级别最高。


### 2.重写fecshop的代码。

下面通过例子来说明：

@fecshop\app\appfront\theme\base\front\cms\home\index.php
这个文件是首页的view文件，我想要修改这个文件，那么

1.首先去@appfront\config\fecshop_local_services\Store.php文件中
，您想要修改的store的本地模板路径，例子代码如下：

```
'stores' => [
	# store_code ,define by domain and fold.
	# 语言必须在fecshoplang中定义，否则将无法得到语言属性。
	# 在添加store的时候，必须查看 添加的语言在 fecshoplang中是否定义。
	'fecshop.appfront.fancyecommerce.com' => [
		'language' 		=> 'en_US',
		'languageName' 	=> 'English',
		
		'localThemeDir'	=> '@appfront/theme/terry/theme01',
		'thirdThemeDir'	=> [],
		'currency' 		=> 'USD',
	],
	'fecshop.appfront.fancyecommerce.com/fr' => [
		'language' 		=> 'fr_FR',
		'languageName' 	=> 'Français',
		'localThemeDir'	=> '@appfront/theme/terry/theme01',
		'thirdThemeDir'	=> [],
		'currency' 		=> 'RMB',
	],
]		
```

如果我想要修改 fecshop.appfront.fancyecommerce.com 这个store的模板，我查看到
本地模板开发路径为：@appfront/theme/terry/theme01
，那么我去这个路径下面新建文件：
@appfront\theme\terry\theme01\cms\home\index.php ，
文件建立后，刷新（如果有缓存，则需要刷新缓存）store对应的url，
则会看到首页的内容部分变成了index.php的内容，
我们新建的index.php没有内容，会看到首页的content部分为空，
下面我们把 @fecshop\app\appfront\theme\base\front\cms\home\index.php
里面的内容复制到刚建立的文件 @appfront\theme\terry\theme01\cms\home\index.php
，然后进行修改即可。

通过上面的例子可以看到，我们只需要在高级别的模板路径，建立
相应的文件路径和文件即可完成对view和layout文件的重写。

对于第三方的view和layout文件，也是按照上面的方式添加相应路径
的文件的方式，来完成重写。






































