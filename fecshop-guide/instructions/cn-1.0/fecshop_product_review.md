FecShop 产品评论
================

> fecshop的产品评论，目前，只要是登录用户，就可以进行评论，和淘宝京东不同。前端添加
> 的评论，后台需要审核



是否只显示当前语言的评论？可以通过配置覆盖

`@fecshop/config/services/Product.php` 文件中的配置：

```	
'review' => [
	'class' => 'fecshop\services\product\Review',
	'filterByLang'	=> false,	# 是否通过语言进行评论过滤？
],
```

`filterByLang` 改成true，只会显示当前语言下的评论。

