Fecshop 模板- Melani
================

> Fecshop 模板- Melani，付费出售的模板，下面关于该模板的介绍


### 介绍

`演示地址`：http://fecshop.appfront.fancyecommerce.com/it

`风格`：简洁风格模板，适合`服装风格`的模板，


`设备`：基于bootstrap开发的模板，`pc`端模板，自适应`手机`，`平板`等移动设备web

`价格`：￥1500.00

`安装，配置`：￥1999.00

`联系`：http://www.fecshop.com/contacts

### 安装

1.首先需要安装Fecshop成功后，再安装模板，
fecshop的安装参看文档：[Fecshop商城安装](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-about-hand-install.html)

> Fecshop版本>= 1.7.1.0

2.付费购买模板后，将模板解压到Fecshop根目录，解压后的文件

模板文件路径：`./feepackage/fect/melani_theme`

配置文件路径：`./common/config/fecshop_third_extensions/fecshop_theme_fect_melani.php`

模板的图片文件路径：`./appimage/appfront/media/fect/melani`

3.将`./feepackage/fect/melani_theme/app/appfront/config/YiiRewriteMap.php`,里面的内容复制到
@appfront/config/YiiRewriteMap.php中，添加文件重写配置。

4.配置store，设置模板为该模板，store添加模板配置

在@appfront/config/fecshop_local_services/Store.php 文件中的 thirdThemeDir 添加模板路径

'@fectmelani/app/appfront/theme/melani',

添加完成的样子为：

'thirdThemeDir'    => [
    '@fectmelani/app/appfront/theme/melani',
],

如果appfront下面所有的store都想使用该模板，
那么，您需要在每一个store配置中的 'thirdThemeDir'添加模板路径配置

5.刷新缓存，访问即可



### 内容修改

为了方便安装和维护，这些内容都是在模板文件里面，如果您想
在后台维护这些cms方面的东西，您可以在后台cms->static block里面添加静态块，将identify设置为
`home-xxxx`, 然后可以使用下面的代码将后台设置的部分调用。

```
<?=  Yii::$service->cms->staticblock->getStoreContentByIdentify('home-xxxx','appfront') ?>
```

### 1.首页走马灯大图

![xxx](images/fee/melani_1.jpg)

`./feepackage/fect/melani_theme/app/appfront/theme/melani/cms/home/index.php`
12行代码处。

![xxx](images/fee/melani_2.jpg)

`./feepackage/fect/melani_theme/app/appfront/theme/melani/cms/home/index.php`
45行代码处。

![xxx](images/fee/melani_3.jpg)

`@common/config/fecshop_third_extensions/fecshop_theme_fect_melani.php`
配置
`homeFeaturedSku`对应的数组

如果配置没有生效，可能您在appfront/config/fecshop_local_modules/Cms.php
配置文件中进行了配置，将该配置文件的`homeFeaturedSku`对应的数组，清除即可。



![xxx](images/fee/melani_4.jpg)

`./feepackage/fect/melani_theme/app/appfront/theme/melani/cms/home/index.php`
105行代码处。

![xxx](images/fee/melani_5.jpg)

`@common/config/fecshop_third_extensions/fecshop_theme_fect_melani.php`
配置

onsale：对应的配置参数 `home_onsale_products`

featured： 对应的配置参数 `home_featured_products`

bestseller： 对应的配置参数 homeBestSellerSku

如果配置没有生效，可能您在appfront/config/fecshop_local_modules/Cms.php
配置文件中进行了配置，将该配置文件的`homeFeaturedSku`对应的数组，清除即可。


![xxx](images/fee/melani_6.jpg)

`./feepackage/fect/melani_theme/app/appfront/theme/melani/cms/home/index.php`
220行代码处。


![xxx](images/fee/melani_7.jpg)

`./feepackage/fect/melani_theme/app/appfront/theme/melani/widgets/footer.php`


![xxx](images/fee/melani_8.jpg)

`./feepackage/fect/melani_theme/app/appfront/theme/melani/catalog/product/index/payment.php`

###  回馈

模板问题在帖子回馈：http://www.fecshop.com/topic/1734











