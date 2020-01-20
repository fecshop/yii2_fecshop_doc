fecbbc 淘宝模式和JD模式产品
================

> fecmall默认是jd模式产品，也就是一个sku一行数据，对于规格属性比较少，而且对每个sku需要单独描述的商家，喜欢JD模式产品
> 但对于做服装类的多规格产品，编辑工作比较大，
> 因此，想要和淘宝类似的方式上传产品

更多的关于jd和淘宝的一些区别，可以参看：[Fecmall扩展-淘宝模式产品扩展](http://www.fecmall.com/doc/fecshop-guide/addons/cn-2.0/guide-fecmall-addons-taobao-product.html)
,fecbbc内置淘宝模式产品，因此默认是淘宝模式产品，如果您想使用jd模式产品，可以参看下面的操作

### fecbbc产品处理


1.默认是`淘宝模式产品`

2.如果您想使用`jd模式`产品，那么可以按照下面的操作

2.1appadmin入口设置

打开配置文件：./addons/fecmall/fecbbc/app/appadmin/config.php

**进行注释去除操作**

2.1.1将

```
'fecRewriteMap' => [
    // 默认淘宝产品编辑模式，如果您不想使用淘宝模式产品，那么请将下面的注释 '//'去掉
    //'\fecbbc\app\appadmin\modules\Catalog\block\productinfo\Index'  => '\fecbbc\app\appadmin\modules\Catalog\block\productinfo\Indexorigin',
    //'\fecbbc\app\appadmin\modules\Catalog\block\productinfo\Managerbatchedit'  => '\fecbbc\app\appadmin\modules\Catalog\block\productinfo\Managerbatcheditorigin',
    
],
```
改为：

```
'fecRewriteMap' => [
    // 默认淘宝产品编辑模式，如果您不想使用淘宝模式产品，那么请将下面的注释 '//'去掉
    '\fecbbc\app\appadmin\modules\Catalog\block\productinfo\Index'  => '\fecbbc\app\appadmin\modules\Catalog\block\productinfo\Indexorigin',
    '\fecbbc\app\appadmin\modules\Catalog\block\productinfo\Managerbatchedit'  => '\fecbbc\app\appadmin\modules\Catalog\block\productinfo\Managerbatcheditorigin',
    
],
```
 
 2.1.2将

```
'theme' => [
    // 默认淘宝产品编辑模式，如果您不想使用淘宝模式产品，那么请将下面的注释 '//'去掉
    'viewFileConfig' => [
    //    'catalog/productinfo/managerbatchedit' => '@fecbbc/app/appadmin/theme/fecbbc/catalog/productinfo/managerbatchedit_origin.php',
    ],
],
```

改为：


```
'theme' => [
    // 默认淘宝产品编辑模式，如果您不想使用淘宝模式产品，那么请将下面的注释 '//'去掉
    'viewFileConfig' => [
        'catalog/productinfo/managerbatchedit' => '@fecbbc/app/appadmin/theme/fecbbc/catalog/productinfo/managerbatchedit_origin.php',
    ],
],
```

2.2appbdmin入口设置


打开配置文件：./addons/fecmall/fecbbc/app/appbdmin/config.php

**进行注释去除操作**

2.1.1将

```
'fecRewriteMap' => [
    // 【默认淘宝产品编辑模式】，如果您不想使用淘宝模式产品，那么请将下面的注释 '//'去掉
    //'\fecbbc\app\appbdmin\modules\Catalog\block\productinfo\Index'  => '\fecbbc\app\appbdmin\modules\Catalog\block\productinfo\Indexorigin',
    //'\fecbbc\app\appbdmin\modules\Catalog\block\productinfo\Managerbatchedit'  => '\fecbbc\app\appbdmin\modules\Catalog\block\productinfo\Managerbatcheditorigin',
    
],
```

改为：

```
'fecRewriteMap' => [
    // 【默认淘宝产品编辑模式】，如果您不想使用淘宝模式产品，那么请将下面的注释 '//'去掉
    '\fecbbc\app\appbdmin\modules\Catalog\block\productinfo\Index'  => '\fecbbc\app\appbdmin\modules\Catalog\block\productinfo\Indexorigin',
    '\fecbbc\app\appbdmin\modules\Catalog\block\productinfo\Managerbatchedit'  => '\fecbbc\app\appbdmin\modules\Catalog\block\productinfo\Managerbatcheditorigin',
    
],
```



2.1.2将

```
'theme' => [
    // 【默认淘宝产品编辑模式】，如果您不想使用淘宝模式产品，那么请将下面的注释 '//'去掉
    'viewFileConfig' => [
    //    'catalog/productinfo/managerbatchedit' => '@fecbbc/app/appbdmin/theme/fecbbc/catalog/productinfo/managerbatchedit_origin.php',
    ],
],
```

改为：

```
'theme' => [
    // 【默认淘宝产品编辑模式】，如果您不想使用淘宝模式产品，那么请将下面的注释 '//'去掉
    'viewFileConfig' => [
        'catalog/productinfo/managerbatchedit' => '@fecbbc/app/appbdmin/theme/fecbbc/catalog/productinfo/managerbatchedit_origin.php',
    ],
],
```


















