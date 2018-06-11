Fecshop 如何更改首页，如何找到首页的文件？ 
=======================================

 

> 阅读前提：安装完成fecshop，并顺了一遍`开发文档`和`帮助文档`，然后想开手修改fecshop功能和文件的开发者

> 下面的文档，是从代码文件的层面一步一步的做代码解析,建议仔细阅读每一个文字步骤


对于首页，你看不到`url key`，因此，你不清楚是那个`url key`，进而也不清楚对应的是那个模块的那个controller部分

fecshop的首页的url 是通过Yii2的 `urlManager`组件来实现的

打开文件 `@fecshop/app/appfront/config/appfront.php` 文件， 可以看到配置：

> @fecshop 这个是yii2里面的知识，此代表的文件路径为  vendor/fancyecommerce/fecshop

```
// 首页对应的url key
        'urlManager' => [
            'rules' => [
                '' => 'cms/home/index',
            ],
        ],
```

也就是对应的是 `cms/home/index` 

1.如果你想重写首页的`url key`，譬如改成 `xxxx/yyyy/zzzz`，你可以在 @appfront/config/fecshop_local.php 中的 components 更改配置

```
// 组件
$components = [
	'urlManager' => [
		'rules' => [
			'' => 'xxxx/yyyy/zzzz',
		],
	],
];
```

然后新建xxxx模块，新建相应的controller 就好

2.上面的方式，初学者建议不要改动，先顺着fecshop的代码走，下面是通过`cms/home/index`去找相应的模块controller文件

`cms/home/index` 
就是 `cms` 模块  `HomeController` 下面的 `actionIndex()`方法
,也就是文件  `@fecshop/app/appfront/modules/Cms/controllers/HomeController.php`文件的

```
 // 网站信息管理
    public function actionIndex()
    {
        $data = $this->getBlock()->getLastData();

        return $this->render($this->action->id, $data);
    }
```

3.寻找block

在上面的actionIndex()的第一行代码`$this->getBlock()`，这个是controller相应的block，block的文件路径，是和`url key`对应起来的，
对应的是文件`@fecshop/app/appfront/modules/Cms/block/home/Index.php` 文件
因此就是这个文件里面的 `getLastData()` 返回的数据，进入这个文件查看

```
public function getLastData()
    {
        $this->initHead();
        // change current layout File.
        //Yii::$service->page->theme->layoutFile = 'home.php';
        return [
            'bestFeaturedProducts'     => $this->getFeaturedProduct(),
            'bestSellerProducts'    => $this->getBestSellerProducts(),
        ];
    }
```

第一行代码，调用了 `$this->initHead();` 找到这个方法，56行文件处

```
public function initHead()
    {
        $home_title = Yii::$app->controller->module->params['home_title'];
        $home_meta_keywords = Yii::$app->controller->module->params['home_meta_keywords'];
        $home_meta_description = Yii::$app->controller->module->params['home_meta_description'];

        Yii::$app->view->registerMetaTag([
            'name' => 'keywords',
            'content' => Yii::$service->store->getStoreAttrVal($home_meta_keywords, 'home_meta_keywords'),
        ]);

        Yii::$app->view->registerMetaTag([
            'name' => 'description',
            'content' => Yii::$service->store->getStoreAttrVal($home_meta_description, 'home_meta_description'),
        ]);
        Yii::$app->view->title = Yii::$service->store->getStoreAttrVal($home_title, 'home_title');
    }
```

代码分析：

`Yii::$app->controller->module->params['home_title'];`这个是Yii2的知识，`Yii::$app->controller->module`代表的找到当前的模块，也就是cms模块，然后找到模块的配置
，我们找到cms模块的配置文件

`@fecshop/app/appfront/config/modules/Cms.php`里面的配置，打开后你看到配置文件被注释掉了，说明是在别的地方进行的配置（fecshop是多配置文件，在初始化的时候，这些配置文件会合并,如果想了解fecshop的配置结果，可以参看：[Fecshop 配置结构](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-init-config-construction.html)）

打开配置文件：@appfront/config/fecshop_local_modules/Cms.php

> @appfront 这个是yii2里面的知识，此代表的文件路径为  appfront

可以看到 `home_title` 的配置。

`Yii::$app->controller->module->params['home_title']` 就是这个配置文件取出来的值

然后继续看:

`Yii::$app->view->registerMetaTag`:这个是用来注册当前页面的meta信息

`Yii::$app->view->title`:是设置当前页面的title

然后继续往下顺代码

4.找到函数

```
public function getProductBySkus($skus)
    {
        if (is_array($skus) && !empty($skus)) {
            $filter['select'] = [
                'sku', 'spu', 'name', 'image',
                'price', 'special_price',
                'special_from', 'special_to',
                'url_key', 'score',
            ];
            $filter['where'] = ['in', 'sku', $skus];
            $products = Yii::$service->product->getProducts($filter);
            //var_dump($products);
            $products = Yii::$service->category->product->convertToCategoryInfo($products);

            return $products;
        }
    }
```

代码：`Yii::$service->product->getProducts($filter);`,是通过过滤条件，找到产品
这个是product services方法，对应的文件为@fecshop/services/Product.php

```
/**
     * 通过where条件 和 查找的select 字段信息，得到产品的列表信息，
     * 这里一般是用于前台的区块性的不分页的产品查找。
     * 结果数据没有进行进一步处理，需要前端获取数据后在处理。
     */
    protected function actionGetProducts($filter)
    {
        return $this->_product->getProducts($filter);
    }
```

对于 `$this->_product` 是在

```
public function init()
    {
        parent::init();
        $currentService = $this->getStorageService($this);
        $this->_product = new $currentService();
    }
```

这里初始化的，对于 `$this->getStorageService`对应的是父类 `@fecshop/services/Service.php`中的方法，代码逻辑这里不一一解释
，上面大致的结果为：

4.1、查看当前类变量`$storage`, 当前的这个值为`public $storage     = 'ProductMongodb';`,

4.2、上面的方法`$currentService = $this->getStorageService($this);`基于类变量`$storage`，进行一些列的逻辑处理，最后$this->_product的值就是：`@fecshop\services\product\ProductMongodb.php`这个类生成的对象。

上面的这个实现方式，是为了方便日后重构，您可以重新来开发一个新的product services，然后在配置文件更改配置`$storage`（配置会在services初始化的时候注入到类变量中），就可以实现product 底层的更改，这也是fecshop架构的一大特色

5.下面打开`@fecshop\services\product\ProductMongodb.php` 查看
`Yii::$service->product->getProducts($filter);`对应的方法

```
/**
     * 通过where条件 和 查找的select 字段信息，得到产品的列表信息，
     * 这里一般是用于前台的区块性的不分页的产品查找。
     * 结果数据没有进行进一步处理，需要前端获取数据后在处理。
     */
    public function getProducts($filter)
    {
        $where = $filter['where'];
        if (empty($where)) {
            return [];
        }
        $select = $filter['select'];
        $query = $this->_productModel->find()->asArray();
        $query->where($where);
        $query->andWhere(['status' => $this->getEnableStatus()]);
        if (is_array($select) && !empty($select)) {
            $query->select($select);
        }

        return $query->all();
    }
```

这个就是Yii2的知识了，也就是Yii2的ActiveRecord的查询

`$this->_productModel` 在`init()`方法中被初始化，对应的是 `@fecshop\models\mongodb\Product.php`,
这个model，model就是Yii2框架中的model,具体的知识查看Yii2框架

这样就找到查询了，最后出来结果范围给controller文件，我们返回到controller文件

`@fecshop/app/appfront/modules/Cms/controllers/HomeController.php`文件的

```
 // 网站信息管理
    public function actionIndex()
    {
         $data 数组里面的每一个子项，就会变成view（theme）文件中的一个变量
		 
		 
		 = $this->getBlock()->getLastData();

        return $this->render($this->action->id, $data);
    }
```

通过上面block，返回的值赋值给`$data`，下面就会传递给`render`函数，对于`render`函数，这个也是Yii2的，
不过，fecshop在此基础上进行了更改加入了`多模板机制`，也即是`view`文件和`css js`的多模板重写机制，这个在文档里面有，自行查阅

view文件也是和url key对应起来的， `cms/index/index` 对应的theme文件就是
`@fecshop/app/appfront/theme/base/front/cms/home/index.php`文件，
`$data` 数组里面的每一个子项，就会变成view（theme）文件中的一个变量，这个是Yii2 的实现，具体原理可以参看：[yii2 通过 render ， views页面生成显示html的原理](http://www.fancyecommerce.com/2016/05/23/yii2-views%E9%A1%B5%E9%9D%A2%E7%94%9F%E6%88%90%E6%98%BE%E7%A4%BAhtml%E7%9A%84%E5%8E%9F%E7%90%86/)

我们继续看这个view文件，`@fecshop/app/appfront/theme/base/front/cms/home/index.php`,也就是内容部分,会发现下面的代码：

```
<?php
				$parentThis['products'] = $bestSellerProducts;
				$parentThis['name'] = 'best-seller';
				$config = [
					'view'  		=> 'cms/home/index/product.php',
				];
				echo Yii::$service->page->widget->renderContent('category_product_price',$config,$parentThis);
			?>
```

这个是fecshop的小部件功能，详细原理参看 [Fecshop 小部件](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_widget.html)


大致就是通过数据和view，最后生成一个独立块，通过这种直接调用生成，因此，一个独立块写完后，在很多其他的地方都可以很方便的调用

其他的帖子回复 [Fecshop 小部件：fecshop模板中$parentThis变量是在哪里定义的，有什么用途？](http://www.fecshop.com/topic/1066）

明白了这个原理，就不难理解这些代码了

5.上面说的是theme部分的`content`部分的渲染，但是还有一个底层的渲染，也就是layout，layout相当于主体部分，theme的content嵌入到layout中，我们查看一下layout文件(css js的加载设置就是在layout中设置的)

打开文件 @fecshop/app/appfront/modules/Cms/Module.php文件，可以看到：
`Yii::$service->page->theme->layoutFile = 'home.php';`，这个是在cms模块的入口文件中设置当前的layout文件，设置后，模块中所有的部分都使用home这个layout，如果你想在某个controller中进行更改，那么在controller中执行上面的代码，然后更改`值`即可

下面，我们去找home这个layout文件，对应的文件为：

@fecshop/app/appfront/theme/base/front/layouts/home.php 文件，打开后，你可以看到一系列的css
和  js的配置


css和js的默认路径对应模板路径下的assets文件夹，也就是`@fecshop/app/appfront/theme/base/front/assets`

```
<?php
$jsOptions = [
	# js config 1
	[
		'options' => [
			'position' =>  'POS_END',
		//	'condition'=> 'lt IE 9',
		],
		'js'	=>[
			'js/jquery-3.0.0.min.js',
			'js/jquery.lazyload.min.js',
			'js/owl.carousel.min.js',
			'js/js.js',
		],
	],
];

# css config
$cssOptions = [
	# css config 1.
	[
		'css'	=>[
			'css/style.css',
			'css/owl.carousel.css',
		],
	],
];
\Yii::$service->page->asset->jsOptions 	= \yii\helpers\ArrayHelper::merge($jsOptions, \Yii::$service->page->asset->jsOptions);
\Yii::$service->page->asset->cssOptions = \yii\helpers\ArrayHelper::merge($cssOptions, \Yii::$service->page->asset->cssOptions);
\Yii::$service->page->asset->register($this);
?>
```

> 除了在layout中添加css和js文件，还可以在配置文件中添加，详细参看：http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-js-css.html

上面的yii2的asset功能，yii2进行了多模板机制的封装

这些文件最后会被复制到web路径下，也就是index.php文件的位置，也就是 `@appfront/web/`下面

对于开发环境下，我们希望每次都进行复制，因此每次访问页面都将这些css js文件复制到@webroot路径下，

打开文件`@appfront/config/main.php`，将注释去掉即可开启强制复制
```
// 请去page asset services中设置 forceCopy
//'assetManager' => [
//    'forceCopy' => true,
//],
```

对于线上，肯定要关闭，因为这个会带来额外的开销，只有更新theme css js文件的时候，才需要开启复制，
因此，线上，将其设置成false即可关闭复制

当线上更新了css 和js 文件，您可以去 @appfront/web/assets/ 文件夹下，清空里面的所有的子文件（rm 删除子文件，注意，assets文件夹不要删除）

如果你的网站访问量不大，设置`'forceCopy' => true,`也没啥问题，前期项目可以每次访问都强制复制


上面说了css 和 js，下面我们继续看
@fecshop/app/appfront/theme/base/front/layouts/home.php

`<?= Yii::$service->page->widget->render('head',$this); ?>`,这是fecshop的小部件功能，上面已经提起，您可以上去重温文档

下面你会看到这个代码 `<?= $content; ?>`, 这个就是上面说的 theme content部分，
也就是上面说的theme view文件：`@fecshop/app/appfront/theme/base/front/cms/home/index.php`，
就会嵌入到layout主体的这个位置。


这样首页的整个流程已经说完了，新手建议多看几遍。






























