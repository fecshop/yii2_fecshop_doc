FecShop 产品评论
================

> fecshop的产品评论，目前，只要是登录用户，就可以进行评论，和淘宝京东不同。前端添加
> 的评论，后台需要审核

### 评论数据

产品的评论，是以`spu`为单位的，也就是该产品的spu对应的`所有sku`的`所有评论`。

### 是否只显示当前语言的评论？

可以通过配置覆盖
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

### 评论权限设置 - 用户下单后才有权限评论该产品的设置

1.3.3.0版本更新下面的两个属性：

`reviewOnlyOrderedProduct`: `true`代表用户购物过的产品才能评论，`false`代表用户没有购买的产品也可以评论

`reviewMonth`: 订单创建后x个月内可以进行评论，超过这个期限将不能评论产品（单位月）,当`reviewOnlyOrderedProduct`设置为`true`时有效。


### 评星汇总

在评论的头部，会对用户的评星进行汇总，如图：

![review start](images/66666.png)










