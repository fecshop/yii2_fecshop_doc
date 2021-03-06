Fecshop breadcrumbs
====================

> Fecshop breadcrumbs指的是面包屑导航，也就是在分类，
> 产品页面的菜单栏下面，显示当前的路径，譬如：
> Home > women dress > summer lady beautiful red dress


Fecshop-2.x更新说明
-------------

2版本更新后台配置

产品，分类，购物车，下单页面的面包屑导航，可以在后台进行配置

Fecshop-1.x
-------------


### 配置：

配置文件是：

```
@fecshop/config/services/Page.php
```


1.您可以在 `@app/config/fecshop_local_services/Page.php` 添加
配置，覆盖掉fecshop默认的配置.

2.`homeName`: 默认是Home，如果为空，则在面包屑导航中不显示。

`ifAddHomeUrl`:代表首页是否添加链接，false代表是文本，ture代表添加
上首页的链接


### 开启 （仅限于appfront入口）

> 1.7.1.0 添加了面包屑导航通过配置的方式选择开启和关闭

Fecshop默认的配置文件地址如下，您可以在@appfront/config/fecshop_local_modules/下面
的模块配置中进行重写：

@fecshop/app/appfront/config/modules/Catalog.php

`'category_breadcrumbs' => true`: 分类页面面包屑配置，true代表开启

`'product_breadcrumbs' => true`: 产品页面面包屑配置，true代表开启
            
@fecshop/app/appfront/config/modules/Catalogsearch.php

`'search_breadcrumbs'        => true`: 搜索页面面包屑配置，true代表开启

@fecshop/app/appfront/config/modules/Checkout.php


`'checkout_cart_breadcrumbs' => false`: 购物车页面面包屑配置，true代表开启

`'checkout_onepage_breadcrumbs' => false`: 下单页面面包屑配置，true代表开启


@fecshop/app/appfront/config/modules/Customer.php


`'login_breadcrumbs' => true`: 账户中心-登陆页面面包屑配置，true代表开启

`'register_breadcrumbs' => true`: 账户中心-注册页面面包屑配置，true代表开启

`'forgot_password_breadcrumbs' => true`: 账户中心-忘记密码页面面包屑配置，true代表开启

`'forgot_reset_password_breadcrumbs' => true`: 下单页面面包屑配置，true代表开启

`'forgot_reset_password_success_breadcrumbs' => true`: 账户中心-重置密码成功页面面包屑配置，true代表开启

`'forgot_reset_password_submit_breadcrumbs' => true`: 账户中心-重置密码提交页面面包屑配置，true代表开启

`'account_center_breadcrumbs' => true`: 账户中心-账户中心页面面包屑配置，true代表开启

`'account_information_breadcrumbs' => true`: 账户中心-账户信息页面面包屑配置，true代表开启

`'customer_address_breadcrumbs' => true`: 账户中心-用户地址页面面包屑配置，true代表开启

`'customer_address_edit_breadcrumbs' => true`: 账户中心-用户地址编辑页面面包屑配置，true代表开启

`'customer_order_breadcrumbs' => true`: 账户中心-订单列表页面面包屑配置，true代表开启

`'customer_order_info_breadcrumbs' => true`: 账户中心-订单详细页面面包屑配置，true代表开启

`'customer_product_review_breadcrumbs' => true`: 账户中心-产品评论页面面包屑配置，true代表开启

`'customer_product_favorite_breadcrumbs' => true`: 账户中心-产品收藏页面面包屑配置，true代表开启
            

### 使用

1.面包屑导航使用，您可以通过下面的代码添加项到breadcrumbs中

```
Yii::$service->page->breadcrumbs->addItems($items)
```


源码：您可以在`@fecshop\services\page\Breadcrumbs.php`里面找到
找到看到如下代码：

```
/**
 * property $items|Array. add $items to $this->_items.
 * $items format example. 将各个部分的链接加入到面包屑导航中
 * $items = ['name'=>'fashion handbag','url'=>'http://www.xxx.com'];.
 */
protected function actionAddItems($items)
{
    if ($this->active) {
        $this->_items[] = $items;
    }
}
```

2.将添加到breadcumbs中的子项调用出来


```
Yii::$service->page->breadcrumbs->getItems();
```


### 例子分析：


1.@appfront-category-breadcrumbs 部分：

如果在appfront 入口，您想打开分类页面部分的breadcrumbs
，您可以在
`@appfront/config/fecshop_local_modules/Catalog.php` 设置

`'category_breadcrumbs' => true,`

设置完，就可以看到分类页面的面包屑导航出来了

![](images/711.png)

2.产品页面

如果在appfront 入口，您想打开分类页面部分的breadcrumbs
，您可以在
`@appfront/config/fecshop_local_modules/Catalog.php` 设置

`'product_breadcrumbs' => true,`

3.search 页面

`@appfront/config/fecshop_local_modules/Catalogsearch.php` 设置

`'search_breadcrumbs' => true,`


面包屑导航对seo有 一定效果，可以根据自己的需要进行开启和关闭
另外，手机web端，面包屑导航已经不要了，取而代之的就是一个回退箭头。
















