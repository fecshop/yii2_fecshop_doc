Fecshop breadcrumbs
====================

> Fecshop breadcrumbs指的是面包屑导航，也就是在分类，
> 产品页面的菜单栏下面，显示当前的路径，譬如：
> Home > women dress > summer lady beautiful red dress

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

2.产品页面没有实现，您可以在
`fecshop\app\appfront\modules\Catalog\block\product\Index.php`
中自己实现，或者，过段时间我写一下这个。


面包屑导航对seo有 一定效果，不过也会弄的页面比较丑，
另外，手机web端，面包屑导航已经不要了，取而代之的就是一个回退箭头。



看自己取舍了。















