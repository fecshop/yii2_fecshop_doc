Fecshop 多语言特性
==================

> Fecshop支持多语言特性，是基于多store来实现的，也就是一个store一种语言
> 通过不同的store的切换，进行语言的转换
> 对于多个入口，目前appadmin暂时不支持多语言，appadmin还没有store的概念，只有一个中文后台。

### 多语言分为两个部分：
- 数据库数据：这个是数据库提供的数据，譬如产品的名字，这部分是
依靠数据库提供的数据和当前的语言，进行自动加载对应语言的数据

- html页面语言，譬如页面底部的条款文件，以及其他的一些描述文字，
这些文件是在文件中的，需要使用文件进行语言的配置，和使用函数
进行语言的转换

#### 数据库数据的多语言切换


#### 页面文字的多语言切换

1.初始化当前语言，这个是在Store Bootstrap中设置。
在文件 @fecshop\services\Store 的bootstrap方法中可以看到如下的代码：

```php
Yii::$service->page->translate->setLanguage($store['language']);
```

这个代码是设置当前的语言，也就是在初始化bootstrap的时候就进行语言的初始化设置。

> 在appfront的配置文件（@appfront/config/fecshop_local.php）中，你可以看到有这个一个配置：[['bootstrap' => ['store'],]]，
> 这个配置的作用是，在bootstrap初始化的时候，执行store组件的bootstrap方法。这样就执行了语言的初始化配置。

2.初始化当前的i18n的category，这个在base controller中被设置
在appfront，所有的controller都是继承 @fecshop\app\appfront\modules\AppfrontController;
,在这个base controller的init方法执行了代码：

```php
Yii::$service->page->translate->category = 'appfront';
```

我们appfront的controller都必须继承于[[@fecshop\app\appfront\modules\AppfrontController]],
这样appfront里面的所有controller在初始化的时候都会执行
上面的代码，这样，在使用 __() 函数翻译的时候，默认都使用appfront作为i18n的category。当然我们的翻译文件的名字也是appfront.php
，这个还是要对应好的，不然会找不到文件。

3.另外我们需要进行配置。
在vendor\fancyecommerce\fecshop\app\appfront\config\appfront.php
中进行了配置：

```php
# language config.
	'components' => [
		'i18n' => [
			'translations' => [
				'appfront' => [
					//'class' => 'yii\i18n\PhpMessageSource',
					'class' => 'fecshop\yii\i18n\PhpMessageSource',
					'basePaths' => [
						'@fecshop/app/appfront/languages',
						'@appfront/languages',
					],
					'sourceLanguage' => 'en_US', # 如果 en_US 也想翻译，那么可以改成en_XX。

				],
			],
		],
	],
```

由于 [[yii\i18n\PhpMessageSource]],是不支持多个basePath的，为了让二次开发者和fecshop
都有各自的basePath，二次开发者的翻译配置可以覆盖fecshop的翻译配置，
这样用户就可以重写fecshop的翻译文件，于是，我对fecshop的
翻译功能进行了重写，让basePath可以支持多个路径，在basePaths数组中，下面的路径的翻译配置可以覆盖上面的路径翻译配置，
重写后的地址为：[[@fecshop\yii\i18n\PhpMessageSource]]
这样可以支持多个basePath,譬如上面的配置[[@appfront/languages]]的配置会覆盖[[@fecshop/app/appfront/languages]]
的配置，这样，用户可以在[[@appfront/languages]]中重写
fecshop的翻译了。


4.上面的步骤，都是在解说fecshop的翻译原理，其实我们在使用的过程中
，按照下面的操作使用即可：
我们可以通过下面的语法使用翻译：

```php
echo Yii::$service->page->translate->__('fecshop,{username}', ['username' => 'terry']);

```

如果我们的当前语言是fr_FR，那么，我们需要在
@appfront/languages 或者
@fecshop/app/appfront/languages中建立文件夹fr_FR，
然后在这个文件夹中新建appfront.php文件。
在这个文件中加入

```php
<?php
return [
 'fecshop'  => 'fr_FR fecshop',
 'fecshop,{username}' =>  'fr_FR fecshop,{username}',
];
```

5.执行翻译：

```
echo Yii::$service->page->translate->__('fecshop,{username}', ['username' => 'terry']);
```

可以看到输出：

```
fr_FR fecshop,terry 
```

6.上面是多语言实现的整个流程，
如果仅仅是使用，譬如在appfront中使用，我们只需要做两件事情
- 在翻译文件中加入翻译：
@appfront/languages/fr_FR/appfront.php文件中加入个数组的配置：

```php
'fecshop,{username}' =>  'fr_FR fecshop,{username}',
```

- 然后，通过下面的方法即可调用：

```php
echo Yii::$service->page->translate->__('fecshop,{username}', ['username' => 'terry']);
```

- 如果当前的store的语言为：fr_FR，那么就会被按照语言文件
那样被翻译。






















