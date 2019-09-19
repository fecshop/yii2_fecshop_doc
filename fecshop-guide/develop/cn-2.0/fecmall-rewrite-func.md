Fecmall 重写功能
================

> 主要讲述的为：在不修改原有文件(vendor/fancyecommerce下面的所有文件)
的前提下，修改任意功能,fecshop 的重写详细如下：



###1. 组件（Yii2 component）重写

这个属于Yii2的范畴，一般通过配置的方式更改Yii2的组件(composer)
，譬如：

```
'components' => [
        'db' => [ 
            'class' => 'yii\db\Connection',
            'dsn' => 'mysql:host=localhost;dbname=fecshop',
            'username' => 'root',
            'password' => 'fd#Ed49lpafdfgeaFs2$d',
            'charset' => 'utf8',
        ],
```

我可以先写一个php文件继承`yii\db\Connection`，
然后将`class`对应的文件指向我自己重写后的php文件，即可实现重写该
Yii2组件。相信这个大家基本都知道。

Yii2组件的更多知识，可以参看[Yii2 组件](http://www.yiichina.com/doc/guide/2.0/structure-application-components)

###2. 重写模块（Yii2 module）

`module`是Yii2框架里面的一个概念，
譬如文件：`@fecshop/app/appfront/config/modules/Customer.php`文件，即可实现重写该

```
return [
	'customer' => [
		'class' => '\fecshop\app\appfront\modules\Customer\Module',
		'params'=> [
			'register' => [
				# 账号注册成功后，是否自动登录
				'successAutoLogin' => true, 
				# 注册登录成功后，跳转的url
				'loginSuccessRedirectUrlKey' => 'customer/account', 
				# 注册页面的验证码是否开启
				'registerPageCaptcha' => true, 
				
			],
			...
		],
	],
];
```

上面是模块的配置，如果你想要重构整个模块（module），
那么您可以通过上面进行配置`class`，指向您重写的文件。

对于Yii2 modules的更多知识可以参看 [Yii2 modules](http://www.yiichina.com/doc/guide/2.0/structure-modules)

### 3. 重写Services（fecshop 服务）

service的重写和组件的重写类似，譬如文件：

`@fecshop/config/services/Category.php`文件


```
return [
	'category' => [
		'class' => 'fecshop\services\Category',
		# 子服务
		'childService' => [
			'product' => [
				'class' => 'fecshop\services\category\Product',
			],
			'menu' => [
				'class' => 'fecshop\services\category\Menu',
				//'rootCategoryId' => 0,
			],
	...
```

您新建一个`class`继承`fecshop\services\Category`
，然后在`class`指向您新建的文件，在您新建的class做函数
重写即可。

### 4. 重写fecshop的模板（view js css等）

`fecmall模板原理`：对于用户来说想要二开appfront的模板，需要修改才能满足自己的需求，
但是对fecmall就比较难办，因为fecmall升级，难免也要修改view css js也要改动
等文件，这些文件不同于php类文件的重写机制，无法通过继承重写函数
的方式进行二开模板文件，
因此就带来了矛盾冲突，fecmall参考了magento的多模板机制，
设置二开的高优先级模板路径,譬如，fecshop想要找view文件
`/category/product/index.php`,首先会在二开模板路径里面找，如果
找到，就不会使用fecshop的模板路径下面的`/category/product/index.php`
因此通过这种方式实现的模板重写。

fecmall的模板部分，以入口进行区分（appfront apphtml5等）的同时，
每一个store又是可以单独选择模板的。

模板的重写原理是通过模板路径优先级来，也就是有好几个
模板路径，分别为fecshop的模板路径【低优先级】，第三方的模板路径【中优先级】，
用户二开（二次开发）的模板路径【高优先级】，fecshop的模板路径的文件最为
全面（优先级最低），然后用户想要重写某个文件，只需要把这个文件路径复制到
二开模板路径下（包括相对文件夹路径），即可完成重写，因为
用户二开模板路径优先级最高。


下面以appfront（pc端）进行举例
说明：

appfront入口的模板路径的配置是在：

`@fecshop/app/appfront/config/params.php`

```
'appfrontBaseTheme' 	=> '@fecshop/app/appfront/theme/base/front',
```

也就是默认所有的store都是使用这里的模板，

`用户二开的模板路径`，和`第三方模板的路径`，可以在后台设置

![](images/p51.png)

重写模板详细举例：
fecshop模板路径为：`@fecshop/app/appfront/theme/base/default`，
我想要重写这个view文件:
@fecshop/app/appfront/theme/base/default/catalog/category/index.php


我本地store设置的模板路径为:
`appfront/theme/terry/theme01`

因此，我创建文件

`appfront/theme/terry/theme01/catalog/category/index.php`

然后把`@fecshop/app/appfront/theme/base/default/catalog/category/index.php`
文件的内容复制到`@appfront/theme/terry/theme01/catalog/category/index.php`
中，然后修改这个文件，就完成了该文件的重写。

是不是很easy呢？

原理还是有一点小复杂，有兴趣可以参看资料：

[yii2 多模板路径优先级加载view方式下- js和css 的解决](http://www.fancyecommerce.com/2016/07/06/yii2-%e5%a4%9a%e6%a8%a1%e6%9d%bf%e8%b7%af%e5%be%84%e4%bc%98%e5%85%88%e7%ba%a7%e5%8a%a0%e8%bd%bdview%e6%96%b9%e5%bc%8f%e4%b8%8b-js%e5%92%8ccss-%e7%9a%84%e8%a7%a3%e5%86%b3/)

[yii2 fecmall 多模板的介绍](http://www.fancyecommerce.com/2016/06/30/yii2-fecshop-%e5%a4%9a%e6%a8%a1%e6%9d%bf%e7%9a%84%e4%bb%8b%e7%bb%8d/)


### 5.翻译文件重写

Yii2本身是有多语言翻译功能，但是缺少重写机制，我进行了扩展，

对于fecshop的翻译，您可以重写fecshop原有的文件翻译：
（目前后台是没有翻译的），下面以appfront进行举例：

打开文件：

`fecshop/app/appfront/config/appfront.php`

您可以看到如下配置：

```
'components' => [
		# language config.
		'i18n' => [
			'translations' => [
				'appfront' => [
					//'class' => 'yii\i18n\PhpMessageSource',
					'class' => 'fecshop\yii\i18n\PhpMessageSource',
					'basePaths' => [
						'@fecshop/app/appfront/languages',
					],
				],
			],
		],
```

首先将Yii2 `i18n` 组件进行了重写，您可以看到`class`改成
了fecshop的`class`
，另外设置了翻译文件的路径 `basePaths`。

打开 `@fecshop/app/appfront/languages` ，您可以看到有很多语言的包，

打开 @fecshop/app/appfront/languages/zh_CN/appfront.php
你就会看到是一个大的配置数组，这里是fecshop的appfront
的原有的配置，下面我们来看重写的步骤：

打开文件：`@appfront/config/main.php`

你会看到如下：

```
'i18n' => [
			'translations' => [
				'appfront' => [
					'basePaths' => [
						'@appfront/languages',
					],
					'sourceLanguage' => 'en_US', # 如果 en_US 也想翻译，那么可以改成en_XX。
				],
			],
		],
```

该配置设置了本地翻译语言的路径为`@appfront/languages`，
并且设置了基础语言为：`en_US`。

然后就可以打开 `@appfront/languages/zh_CN/appfront.php`进行重写
翻译内容了

> 注意: 模板的重写是文件的替换，翻译文件的重写是文件内容合并，相当于两个数组合并（merge）
> 如果相同的key，本地的翻译会覆盖fecshop的翻译。

### 6.邮件重写

详情参看：[fecshop邮件](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_email.html)

可以通过配置的方式重写邮件模板。

### 7.重写yii2框架的class（classMap的方式，fecmall功能重写基本不会用到）

> 对于Yii2框架的一些框架内部class，如果您想重写，可以用classMap
> ,但是classMap也有他的缺陷，classMap指向新文件class是不能继承原来的class
> ,因此，Yii2框架的class如果更新了，重新指向的class文件也需要更新，这种通过classMap
> 进行重写的方式，有一定的局限性，一般不推荐用这种。

该重写是通过Yii2的`classMap`机制实现的，关于classMap可以参看
[类映射表Class Map](http://www.yiichina.com/doc/guide/2.0/concept-autoloading#class-map)

我整理的一篇关于classMap的原理文章：
[通过配置的方式重写某个Yii2 文件 或第三方扩展文件](http://www.fancyecommerce.com/2016/10/13/%e9%80%9a%e8%bf%87%e9%85%8d%e7%bd%ae%e7%9a%84%e6%96%b9%e5%bc%8f%e9%87%8d%e5%86%99%e6%9f%90%e4%b8%aayii2-%e6%96%87%e4%bb%b6-%e6%88%96%e7%ac%ac%e4%b8%89%e6%96%b9%e6%89%a9%e5%b1%95%e6%96%87%e4%bb%b6/)

看完了上面的文章，您应该就会明白`classMap`是个啥玩意，下面
说一下fecmall中的使用。还是以appfront举例：

`@appfront/config/YiiClassMap.php`文件：

```
<?php
return [
	//'fecshop\app\appfront\helper\test\My' => '@appfront/helper/My.php',   
	
];
```

在代码中，我们会通过use加载其他的类，
`use fecshop\app\appfront\helper\test\My`,
默认回去找文件 `@fecshop/app/appfront/helper/test/My.php`

但是如果我在classMap中进行了配置
`'fecshop\app\appfront\helper\test\My' => '@appfront/helper/My.php'`,
那么当我在调用My类 `use fecshop\app\appfront\helper\test\My`，
use的类就变成了 `@appfront/helper/My.php`，而不是`@fecshop/app/appfront/helper/test/My.php`，
到这里您应该明白了吧。

另外，重写后的文件的namespace要和重写的文件的namespace一致，因此，
`@appfront/helper/My.php`文件的namespace是`fecshop\app\appfront\helper\test\My`，

在使用过程中如果报错：`Exception (Unknown Class) 'yii\base\UnknownClassException' with message 'Unable to find 'xxxxxx' in file: xxxx.php. Namespace missing?' `，可以参看一下这位朋友的报错：http://www.fecshop.com/topic/135

> classMap 在fecshop中，很少用到，通过fecshop的重写机制
> 基本可以满足功能的重写。

### 8.通过rewriteMap进行重写Block Model 层

> 对于block层，model层，可以通过rewriteMap进行配置
> ,进行重新指向，这是一种推荐的重写方式，比classMap要好很多，
> 重写后的class是可以继承被重写的class的，这样对于升级会好很多。


打开 @common/config/YiiRewriteMap.php ，您可以通过配置

```
return [
    /**
     * \fecshop\models\mongodb\Category 为原来的类
     * \appfront\local\local_models\mongodb\Category 为重写后的类
     * 重写后的类可以继承原来的类。
     */
    //'\fecshop\models\mongodb\Category'  => '\appfront\local\local_models\mongodb\Category',
];
```

`\fecshop\models\mongodb\Category` : fecshop 核心包的类文件

`\appfront\local\local_models\mongodb\Category` : 本地重写后的类文件。

下面查看本地重写后的类文件的内容。

```
<?php
namespace appfront\local\local_models\mongodb;

use yii\mongodb\ActiveRecord;

class Category extends \fecshop\models\mongodb\Category
{
    // 重写您想要重写的方法
}
```

可以看到，是可以继承原来的类的。我们只需要按照我们的要求，重写
相应的方法即可。因此这种方式比Yii2的classMap要好很多。
Yii2的classMap是不能继承原来的类的。

因此，使用这种方式，只需要做一个配置指向，然后实现相应的类就可以了。

### 9. 通过Yii2 的 controllerMap 重写controller

[Yii2 ControllerMap](http://www.yiichina.com/doc/guide/2.0/structure-applications#controllerMap)
是Yii2 的一种重写ControllerMap的机制。

fecshop module 里面的controller的重写也是通过这个机制进行的，
下面是一种重写的例子：

我们想要重写appfront的catalog模块的CategoryController,下面是详细步骤：

fecshop系统的controller: `@fecshop\app\appfront\modules\Catalog\controllers\CategoryController`

本地重写的Controller: `@appfront\local\local_modules\Catalog\controllers\CategoryController`

1.新建本地的controller:

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace appfront\local\local_modules\Catalog\controllers;

use fecshop\app\appfront\modules\AppfrontController;
use Yii;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class CategoryController extends \fecshop\app\appfront\modules\Catalog\controllers\CategoryController
{
    // 重写相应的controller action方法
}
```

2.在配置中添加classMap

打开配置文件 `@appfront/config/fecshop_local_modules/Catalog.php`

添加如下配置：

```
return [
    'catalog' => [
        /**
         * Yii2 controllerMap 重写机制。
         */
        'controllerMap' => [
            'category' => 'appfront\local\local_modules\Catalog\controllers\CategoryController',          
        ],
        ...
    ]
    ...
]
```

完成上面的步骤后，如果访问分类页面，执行的是
重写后的controller文件，也就是：`@appfront\local\local_modules\Catalog\controllers\CategoryController`
,您可以在这个文件里面重写原来的action方法。



### 10. 在已有模块（module）下新增controller 和 block

> 有时候，我们想基于原有的module进行扩展，增加新的controller 和block ，theme等

10.1新增controller

可以参考上面的第9部分，通过`controllerMap`新增controller

10.2新增block

在controller中获取block是通过getBlock()方法实现的

```
public $blockNamespace;

    /**
     * @param $blockName | String
     * get current block
     * 这个函数的controller中得到block文件，譬如：
     * cms模块的ArticleController的actinIndex()方法中使用$this->getBlock()->getLastData()方法，
     * 对应的是cms/block/article/Index.php里面的getLastData()，
     * 也就是说，这个block文件路径和controller的路径有一定的对应关系
     * 这个思想来自于magento的block。
     */
    public function getBlock($blockName = '')
    {
        if (!$blockName) {
            $blockName = $this->action->id;
        }
        if (!$this->blockNamespace) {
            $this->blockNamespace = Yii::$app->controller->module->blockNamespace;
        }
        if (!$this->blockNamespace) {
            throw new \yii\web\HttpException(406, 'blockNamespace is empty , you should config it in module->blockNamespace or controller blockNamespace ');
        }
        $viewId = $this->id;
        $viewId = str_replace('/', '\\', $viewId);
        $relativeFile = '\\'.$this->blockNamespace;
        $relativeFile .= '\\'.$viewId.'\\'.ucfirst($blockName);
        //查找是否在rewriteMap中存在重写
        $relativeFile = Yii::mapGetName($relativeFile);
        
        return new $relativeFile();
    }
```

可以看到类变量`blockNamespace`，这个就是用来设置查找block文件的，如果不填写，那么默认使用的是当前modules的文件路径，您可以设置这个类变量的值。

因此可以在controller中设置类变量，譬如：

```
public $blockNamespace = 'fbbcbase\\app\\appadmin\\modules\\Sales\\block';
```

然后再上面对应的路径中新建block文件就可以了。

