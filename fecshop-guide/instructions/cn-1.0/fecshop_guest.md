Fecshop 游客
===========

> Fecshop 游客 指的是未登录账户的用户部分。

1. 游客下单

购物车跳转到下单页面，判断用户是否登录，如果没有登录，
则跳转到登录页面的设置：

配置文件为：

./vendor/fancyecommerce/fecshop/app/appfront/config/modules/Checkout.php

./vendor/fancyecommerce/fecshop/app/apphtml5/config/modules/Checkout.php

./vendor/fancyecommerce/fecshop/app/appserver/config/modules/Checkout.php


```
/**
 * 模块内部的params配置。
 */
'params'=> [
    'guestOrder' => true, // 是否支持游客下单
],
```

默认支持游客下单，如果想必须登录后才能下单，
那么把true改成false 即可。

您可以在本地路径更改配置，来覆盖掉Fecshop的默认配置



