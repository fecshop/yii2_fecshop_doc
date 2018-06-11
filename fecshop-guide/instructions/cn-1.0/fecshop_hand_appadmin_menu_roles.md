Fecshop 后台添加菜单，设置权限，并访问
==========================




fecshop后台是有默认的功能菜单，如果您想自己添加菜单，那么，可以遵循下面的方式

![](https://i.loli.net/2017/12/03/5a23e956d35f9.png)

![](https://i.loli.net/2017/12/03/5a23e9626024e.png)

![](https://i.loli.net/2017/12/03/5a23e96bec7d9.png)

图片上的红色的文字一定要仔细看，如果看不清楚，可以把浏览器放大一下，就会看清楚。

最后要**刷新缓存**，关于刷新缓存，可以参看文章：[FecShop 缓存](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_cache.html)

然后，你在fecshop的appadmin部分local中，加入相应的modules，然后新建controller即可。

如果在访问新建菜单的过程中，出现没有权限的问题，那么就有2中可能：

1.没有把菜单加入当前用户的用户组

2.加完后，没有`刷新缓存`。














