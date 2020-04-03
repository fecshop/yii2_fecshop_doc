Fecmall 如何隐藏后台（appadmin）的菜单
===============


> 对于fecmall后台的菜单，某些原有的菜单进行隐藏


### Fecmall后台菜单


对于fecmall后台的菜单，是通过配置文件实现的，您可以通过配置的方式在原有的基础上进行菜单的累加，
但是，有时候对fecmall进行改造，需要将原有的一些菜单进行隐藏，本章文档着重解说如何隐藏


1.关于fecmall后台菜单配置文件

配置文件：https://github.com/fecshop/yii2_fecshop/blob/master/config/services/Admin.php#L72


2.新增后台菜单

关于新增后台菜单，这里有讲述：[Fecmall 后台菜单RBAC](http://www.fecmall.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_admin_rbac.html)


3.隐藏菜单

您可以在配置文件重加入 配置  `'active' => false,`

譬如，我想将产品部分的菜单隐藏

```
'menuConfig' => [
                    // 一级大类
                    'catalog' => [
                        'label' => 'Category & Prodcut',
                        'active' => false,
                        'child' => [
                            // 二级类
                            'product_manager' => [
                            
                            ......


```

在菜单配置加入 `'active' => false,`，即可隐藏掉



4.隐藏菜单原理实现

实现原理参看：https://github.com/fecshop/yii2_fecshop/blob/master/services/admin/Menu.php#L52






































