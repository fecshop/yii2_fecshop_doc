Fecshop 模板view文件嵌套引用原理
===================


> Fecshop 模板view文件嵌套，指的是在view文件中调用子view，以及在子view中继续调用其他的子view的方式，
> 下面会说明这样设计，是为了解决那些问题，以及实现的原理。



首先，你先了解一下fecshop的模板原理：http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_theme.html

### 为了解决那些问题

1.首先，对于mvc结构，在yii2框架中，视图部分是由`layout` 和具体的`view`文件组成，也就是两个文件，
layout文件没有问题，非常简洁，代码不会很多，而对于`view`部分，html代码量还是非常大的，
譬如产品页面的样式全部写到一个`view`文件里面，还是很庞大的，因此将view文件打碎成多个文件，这样会更好一些

2.另外，会存在某些块公用的调用，譬如头部和尾部，或者产品页面和分类页面都可以显示一个`tab栏目`，也就是各个页面的公用块，如果将这些公用快做成一个独立的方式，通过某个函数调取就可以顺利的引入，这样就会非常的方便，就像工厂生产出来，哪里用就哪里调用

3.对于一个独立块，麻雀虽小，五脏俱全，就像一个完整页面一样，需要动态计算数据`class`部分，
也需要展示`view`部分，因此，这个部分是由2部分组成，`数据提供部分`和`视图部分`，
对于这个，可以参看一下：[fecshop小部件](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_widget.html)
,fecshop小部件，是一种预定义的方式，主要用于头部和尾部等公用的部分，
并自带`cache`缓存功能，详细的参看文档:[fecshop小部件](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_widget.html)


4.当然，也有一种，是不需要在配置文件中预定义，而是在使用的时候直接引入即可，下面找一个例子讲解，


4.1打开文件：https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/theme/base/front/catalog/product/index.php

这个文件是产品页面的`view`部分，可以看到价格部分的调用，32行

```
<div class="price_info">
<?php # 价格部分
	$priceView = [
		'view'	=> 'catalog/product/index/price.php'
	];
	$priceParam = [
		'price_info' => $price_info,
	];
?>
<?= Yii::$service->page->widget->render($priceView,$priceParam); ?>

</div>
```

`view`部分对应的是：https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/theme/base/front/catalog/product/index/price.php

上面的`$priceView`，代表是配置部分，上面只配置了`view`部分，没有class文件配置，说明不需要动态数据部分，
对于存在`class`的例子可以查看该文件的61行，这个在view文件中引入的custom_optopn`子view`是存在`class`的

下来来看`Yii::$service->page->widget->render($priceView,$priceParam);`
，也就是文件：https://github.com/fecshop/yii2_fecshop/blob/master/services/page/Widget.php
，查看方法 `  protected function actionRender($configKey, $parentThis = '')`

在这个方法中，你可以看到首先从配置文件中查看是否有预定义的小部件，如果没有，那么就使用当前
传递的参数，然后调用`protected function actionRenderContent($configKey, $config, $parentThis = '')`

对于`actionRenderContent`方法，有一部分从配置中取出来数据，是否支持`cache`，如果
存在`cache`的配置，并且`cache`有效，就会从`cache`中取出来，而不需要class计算数据

最终都是调用`actionRenderContentHtml`渲染出来页面



对于有的开发者，会注意到，在子view文件中有一个`$parentThis`参数，不知道从何而来

譬如：https://github.com/fecshop/yii2_fecshop/blob/master/app/appfront/theme/base/front/catalog/product/index/price.php
的代码`<?php  $price_info = $parentThis['price_info'];   ?>`
就是在引入的地方传递的参数，也就是4.1部分的：

```
$priceParam = [
    'price_info' => $price_info,
];
```

下面说一下`$parentThis`是怎么传递过去的


上面代码调用传递的参数 `$priceParam`,被`Yii::$service->page->widget->render($priceView,$priceParam);`
函数的参数`$parentThis`接收，

你会发现这个参数在后面并没有被使用，而是在各个子函数中传递，最终被函数
`protected function actionRenderContentHtml($configKey, $config, $parentThis = '')`,
接收，在代码99行（上面的文件：https://github.com/fecshop/yii2_fecshop/blob/master/services/page/Widget.php）处可以看到

```
if ($parentThis) {
	$params['parentThis'] = $parentThis;
}
 return Yii::$app->view->renderFile($viewFile, $params);
```

这里，你应该就明白了，将前面传递的 `$priceParam`作为 `$params['parentThis'] `，
对于方法`Yii::$app->view->renderFile($viewFile, $params)`,这个是yii2的方法，和controller里面结尾处的render类似，也就是把数据里面每个数据，作为一个变量，在view中可以直接使用，
因此，对于

```
$priceParam = [
    'price_info' => $price_info,
];
```

就可以在view中使用 `$parentThis['price_info']`,也就是上面传递的值

可能你对Yii2不熟悉，对于`Yii::$app->view->renderFile($viewFile, $params)`不了解，这个我之前整理了一个文章：
[yii2 通过 render ， views页面生成显示html的原理](http://www.fancyecommerce.com/2016/05/23/yii2-views%E9%A1%B5%E9%9D%A2%E7%94%9F%E6%88%90%E6%98%BE%E7%A4%BAhtml%E7%9A%84%E5%8E%9F%E7%90%86/)


