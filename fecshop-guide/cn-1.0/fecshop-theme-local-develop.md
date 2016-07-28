Fecshop 本地模板开发
===================

设置当前store的本地模板路径。

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

也就是添加到上面的[[localThemeDir]]数组中即可，
然后就可以在这个路径下面开发模板了。

对于js和css的重写，参考：[Fecshop js和css的重写](fecshop-theme-js-and-css.md)

对于view和layout的重写，参考：[Fecshop layout和view文件的重写](fecshop-theme-view-and-layout.md)

对于翻译，参考: [Fecshop 文字翻译](fecshop-feature-mutil-languages.md)

这样，第三方就可以扩展相应的模板了。

### 对于模板路径下面的文件的介绍

**widgets文件夹**：Head，Header，Footer，Menu等在里面
，其他的widgets也是在模板路径下的widgets里面

**assets文件夹**：js和css在里面

**layouts文件夹**：layouts文件。

**其他**：一般是模块对应的content部分的view文件。
