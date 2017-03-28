Fecshop Url重写
==============

> fecshop url 重写，属于自定义的方式重写，定义的重写会被保存到mongodb中。

### 1. 重写原理

1.1 在数据库的产品或分类保存的时候，会有一个唯一的url_key字符串，和真实的yii2的
`url key`对应，譬如`/xxxxxxx` 对应 `/catalog/product/index?id=xxxx`

1.2当一个url访问的时候，会到数据库(mongodb)中查询，该url是否在数据库中存在，如果存在，
则会使用对应的真实的yii2的url路径，譬如上面的`/catalog/product/index`

1.3 执行相应的模块

关于重写的原理详细参看：[yii2 Url 自定义 伪静态url](http://www.fancyecommerce.com/2016/05/18/yii2-url-%E8%87%AA%E5%AE%9A%E4%B9%89-%E4%BC%AA%E9%9D%99%E6%80%81url/)


### 2. 重写的url类型

2.1 page页面

2.2 category分类页面

2.3 product产品页面

在上述页面保存的时候，如果填写url_key就会使用填写的url_key，如果不填写
就会使用名字生成。

如果生成的url在数据库中存在，那么会在后面加入一组随机数字，如果随机数字还存在，
那么就会使用另外一组随机数字，直到唯一为止。

Url自定义（Url 重写）是为了seo，让网页中的关键字，标题，在url中也出现。

### 3.fecshop实现重写的文件

文件为：`@fecshop/yii/web/Request.php` 
，重写了`@yii/web/Request`的一部分方法实现的。






















