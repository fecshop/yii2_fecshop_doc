FecShop 产品评论
================

> fecshop的产品评论，目前，只要是登录用户，就可以进行评论，和淘宝京东不同。前端添加
> 的评论，后台需要审核



是否只显示当前语言的评论？可以通过配置覆盖

`@fecshop/config/services/Product.php` 文件中的配置：

```	
'review' => [
	'class' => 'fecshop\services\product\Review',
    'filterByLang'    => false,    // 是否通过语言进行评论过滤？
    // true：代表用户购物过的产品才能评论，false：代表用户没有购买的产品也可以评论
    'reviewOnlyOrderedProduct' => true,
    // 订单创建后，多久内可以进行评论，
    // 超过这个期限将不能评论产品（单位为月）, 当 reviewOnlyOrderedProduct 设置为true时有效。
    'reviewMonth' => 6,
],
```

`filterByLang`: 改成true，只会显示当前语言下的评论。

1.3.3.0版本更新下面的两个属性：

`reviewOnlyOrderedProduct`: `true`代表用户购物过的产品才能评论，`false`代表用户没有购买的产品也可以评论

`reviewMonth`: 订单创建后x个月内可以进行评论，超过这个期限将不能评论产品（单位月）,当`reviewOnlyOrderedProduct`设置为`true`时有效。













