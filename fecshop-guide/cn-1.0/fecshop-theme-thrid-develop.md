Fecshop模板第三方制作
====================

第三方，可以通过yii2扩展的方式制作模板，制作完成后，
发布版本到包管理器，然后用户可以通过
安装的方式，加载第三方开发的模板或者库包，
当然，用户也可以通过手动安装的方式安装相应的文件。
安装后，用户需要store中设置第三方模板的路径：

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
```

也就是添加到上面的[[thirdThemeDir]]数组中即可。

对于js和css的重写，参考：[Fecshop js和css的重写](fecshop-theme-js-and-css.md)

对于view和layout的重写，参考：[Fecshop layout和view文件的重写](fecshop-theme-view-and-layout.md)

这样，第三方就可以扩展相应的模板了。

### 对于模板路径下面的文件的介绍

**widgets文件夹**：Head，Header，Footer，Menu等在里面
，其他的widgets也是在模板路径下的widgets里面

**assets文件夹**：js和css在里面

**layouts文件夹**：layouts文件。

**其他**：一般是模块对应的content部分的view文件。








