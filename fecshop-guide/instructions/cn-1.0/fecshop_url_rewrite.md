Fecshop Url重写
==============

> fecshop url 重写，属于自定义的方式重写，定义的重写会被保存到mongodb中。

### 1.去掉index.php

对于url: https://fecshop.appfront.fancyecommerce.com/index.php/special-occasion
为了seo的考虑，我们希望把index.php/去掉，下面是设置方法。


找到文件 `@appfront/config/fecshop_local_services/Url.php`
,内容如下：

```
return [
	'url' => [
		'showScriptName'=> false, # if is show index.php in url.  if set false ,you must config nginx rewrite 
	],
];

```

`showScriptName`：`true`代表url中显示index.php
,`false`代表url中不显示index.php

当设置了`false`，也就是不显示index.php，需要在nginx设置重写
，具体可以搜索这个(用bing.com搜索就不错，不需要翻墙，也可以
切换英文搜索)。






### 2. 重写原理

2.1 在数据库的产品或分类保存的时候，会有一个唯一的url_key字符串，和真实的yii2的
`url key`对应，譬如`/xxxxxxx` 对应 `/catalog/product/index?id=xxxx`

2.2当一个url访问的时候，会到数据库(mongodb)中查询，该url是否在数据库中存在，如果存在，
则会使用对应的真实的yii2的url路径，譬如上面的`/catalog/product/index`

2.3 执行相应的模块

关于重写的原理详细参看：[yii2 Url 自定义 伪静态url](http://www.fancyecommerce.com/2016/05/18/yii2-url-%E8%87%AA%E5%AE%9A%E4%B9%89-%E4%BC%AA%E9%9D%99%E6%80%81url/)


### 3. 重写的url类型

3.1 page页面

3.2 category分类页面

3.3 product产品页面

在上述页面保存的时候，如果填写url_key就会使用填写的url_key，如果不填写
就会使用名字生成。

如果生成的url在数据库中存在，那么会在后面加入一组随机数字，如果随机数字还存在，
那么就会使用另外一组随机数字，直到唯一为止。

Url自定义（Url 重写）是为了seo，让网页中的关键字，标题，在url中也出现。

### 4.fecshop实现重写的文件

文件为：`@fecshop/yii/web/Request.php` 
，重写了`@yii/web/Request`的一部分方法实现的。
具体的实现方法，你可以参看文件`@fecshop/yii/web/Request.php`的内容






















