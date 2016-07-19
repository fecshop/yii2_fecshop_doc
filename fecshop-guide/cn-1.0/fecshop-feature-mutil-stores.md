Fecshop 多store特性
==================

> Fecshop 的多store，是和域名，或者域名下的某个文件夹绑定的，
> store key为唯一标示，每个store下面可以设置不同的语言，默认货币，模板等

### 如何添加一个store

添加一个store，可以通过三种方式：
- 通过不同的域名进行添加，譬如：www.aaa.com ,www.bbb.com ,  www.ccc.com
- 同一域名下的不同子域名，譬如：www.aaa.com ,en.aaa.com,cn.aaa.com, de.aaa.com等，这种好处是：由于是同一个域名，可以购物车共享，当然您也
可以设置购物车不共享。
- 同一个子域名下的不同路径，譬如：www.aaa.com, www.aaa.com/en , www.aaa.com/cn , www.aaa.com/de , www.aaa.com/es 等

下面详细介绍各种方式对应的设置

### 1.通过不同的域名进行添加.

在文件：@app/config/fecshop_local_services/Store.php
中配置

```
<?php
   return [
   'store' => [
		'class' => 'fecshop\services\Store',
		'stores' => [
			# store_code ,define by domain and fold.
			'www.aaa.com' => [
				'language' 		=> 'en_US',
				'languageName' 		=> 'English',
				'themePackage'	=> 'default',
				'theme'	=> 'default',
				'currency' => 'USD',
			],
			'www.bbb.com' => [
				'language' 		=> 'fr_FR',
				'languageName' 		=> 'Français',
				'themePackage'	=> 'default',
				'theme'	=> 'default',
				'currency' => 'RMB',
			],
			'www.ccc.com' => [
				'language' 		=> 'es_ES',
				'languageName' 		=> 'Español',
				'themePackage'	=> 'default',
				'theme'	=> 'default',
				'currency' => 'USD',
			],
			
		],
		
	],
			
];

```

参数：[[stores]]: 在的数组配置中，必须用域名作为数组的key，譬如上面的值为：www.ccc.com。

参数：[[language]]： 为当前store的语言，它通常是由语言 ID 和区域 ID 组成。 
例如，ID [[en-US]] 代表英语和美国的语言环境。为了保持一致性， 所有区域 ID 应该规范化为 ll-CC， 其中 ll 是根据两个或三个字母的小写字母语言代码 ISO-639 和 CC 是两个字母的国别代码 ISO-3166。
 有关区域设置的更多细节可以看 ICU 项目文档。
 
参数：[[languageName]]: 为按照当前store的语言的名称，譬如www.ccc.com是西班牙语，Español是西班牙的语言，代表西班牙语

参数：[[themePackage]]: 代表当前store 对应的模板包名，这个和模板设置有关

参数：[[theme]]: 代表当前store对应的模板名，这个和模板设置有关。

参数：[[currency]]: 这个是当前store的默认货币。

如果想要添加一个多域名方式的store，除了在上面添加域名，
还需要在nginx里面设置一下，让域名指向app/web下面，另外如果
不同的域名要有不同的robots.php可以通过nginx做设置。

### 2.通过不同的子域名做设置

类似不同域名，基本步骤类似，只需要将相应的域名改成子域名即可。

### 3.同一子域名下的不同的路径：

这个需要在app/web/下面建立文件夹，然后在这个文件夹下面新建index.php文件和assets文件夹

譬如：我们的配置如下：

```php
<?php
   return [
   'store' => [
		'class' => 'fecshop\services\Store',
		'stores' => [
			# store_code ,define by domain and fold.
			'fecshop.appfront.fancyecommerce.com' => [
				'language' 		=> 'en_US',
				'languageName' 		=> 'English',
				'themePackage'	=> 'default',
				'theme'	=> 'default',
				'currency' => 'USD',
			],
			'fecshop.appfront.fancyecommerce.com/fr' => [
				'language' 		=> 'fr_FR',
				'languageName' 		=> 'Français',
				'themePackage'	=> 'default',
				'theme'	=> 'default',
				'currency' => 'RMB',
			],
			'fecshop.appfront.fancyecommerce.com/es' => [
				'language' 		=> 'es_ES',
				'languageName' 		=> 'Español',
				'themePackage'	=> 'default',
				'theme'	=> 'default',
				'currency' => 'USD',
			],
			'fecshop.appfront.fancyecommerce.com/cn' => [
				'language' 		=> 'zh_CN',
				'languageName' 		=> '中文',
				'themePackage'	=> 'default',
				'theme'	=> 'default',
				'currency' => 'RMB',
			],
		],
		
	],
			
];

```

那么我需要在app/web下面建立

```
./cn/
./cn/index.php
./cn/robots.txt
./cn/asset/  # 设置可写

./es/
./es/index.php
./es/robots.txt
./es/asset/  # 设置可写

./de/
./de/index.php
./de/robots.txt
./de/asset/  # 设置可写

./fr/
./fr/index.php
./fr/robots.txt
./fr/asset/  # 设置可写

```

然后需要进行nginx添加设置：

```
location /fr/ {
		index index.php;
		if (!-e $request_filename){
				rewrite . /fr/index.php last;
		}
}
 location /es/ {
		index index.php;
		if (!-e $request_filename){
				rewrite . /es/index.php last;
		}
}

 location /cn/ {
		index index.php;
		if (!-e $request_filename){
				rewrite . /cn/index.php last;
		}
}

 location /de/ {
		index index.php;
		if (!-e $request_filename){
				rewrite . /de/index.php last;
		}
}

```

然后就可以了。

这里需要注意的是上面配置[[stores]]数组的key，
是域名+子文件夹，譬如

```
'fecshop.appfront.fancyecommerce.com/cn' => [
	'language' 		=> 'zh_CN',
	'languageName' 		=> '中文',
	'themePackage'	=> 'default',
	'theme'	=> 'default',
	'currency' => 'RMB',
],
```

 fecshop.appfront.fancyecommerce.com/cn
就是这个store对应的key，这个store下面的所有url都以这个当做base url。

> 注意 ： 这里说的域名，要去掉http部分，不包括这个。
> store里面的各个参数的具体作用，请参考步骤一，这些参数对应的值都是一致的。

到这里，多store的配置就已经完成。重启nginx就应该可以生效了，
如果您添加了新的语言，还需要添加翻译文件和翻译数据。







