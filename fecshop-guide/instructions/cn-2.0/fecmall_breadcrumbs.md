Fecmall breadcrumbs
====================

> Fecmall breadcrumbs指的是面包屑导航，也就是在分类，
> 产品页面的菜单栏下面，显示当前的路径，譬如：
> Home > women dress > summer lady beautiful red dress


面包屑导航，都在后台配置，产品，分类，购物车，下单页面的面包屑导航，可以在后台进行配置



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

大多数的面包屑导航改成了后台配置开启和关闭，还有一少部分的，还保留在文件配置中

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
            

### fecmall 面包屑导航使用

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



面包屑导航对seo有 一定效果，可以根据自己的需要进行开启和关闭
另外，手机web端，面包屑导航已经不要了，取而代之的就是一个回退箭头。
















