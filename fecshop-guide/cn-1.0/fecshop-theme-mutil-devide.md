Fecshop 多设备模板
==================

对于前台，不同的设备，对应不同的入口

pc: @appfront/web/index.php

手机web: @apphtml5/web/index.php

手机app: @appserver/web/index.php

当手机访问pc的域名，系统自动跳转到手机web中。
跳转是store组件的bootstrap()方法实现的，
首先，看store服务的配置：

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
				
				//'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'USD',
				'mobile'		=> [ # 当设备满足什么条件的时候，进行跳转。
					'enable'		=> true,
					'condition'		=> ['phone','tablet'],
					'redirectUrl' 	=> 'fecshop.apphtml5.fancyecommerce.com',	
				],
			],
```

mobile 的各个选项：

- [[enable]] 代表当前的store是否开启跳转
- [[condition]] 代表当设备为什么的时候跳转，phone代表
是手机，tablet代表平板。
- [[redirectUrl]] 是跳转的域名。

通过上面的设置就实现了多设备不同入口，
以及pc端跳转手机端的功能。



