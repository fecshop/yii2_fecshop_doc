Fecshop 后台配置
================

> fecshop 是通过配置文件的方式进行配置的，更改成后台配置也是可行的，
> 下面对于出思路（fecshop并没有实现这个）

###1. 配置写入数据库

在index.php文件中可以得打$config数组，那么，我们可以把这些值写入到
数据库中，在数据库中检查相应的key是否存在，如果不存在则写入（数组的key
和value都写入），
如果存在，则不写入，这样就实现了将所有配置写入数据库中。

由于fecshop的config是多维数组的方式，所以，需要想办法解决两个问题：1.把
多维数据写入到数据库中，2将数据从数据库中取出来还原成原来的配置数组。
实现思路：1.使用多维结构数据库mongodb等类型数据库，这种比较容易一些
2.使用关系型数据库，使用一定的方式存储，在组织起来，这种比较复杂一些。


###2. 从数据库取出来配置。

在index.php 文件中，数组$config部分从数据库取出来数据。
当然，为了加速，您可以先同步到redis，从redis中取出来，
或者您数据库的配置输出到单配置文件，然后从单配置文件中取出来数据。
对于单配置文件的知识可以参看：[fecshop 配置加速](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_config_speed.html)


上面的是实现思路，fecshop并未实现。只实现了[fecshop 配置加速](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_config_speed.html)
，如果有这方面的需求可以采取上面的思路来实现。
这种需求一般配置操作比较频繁才会这样搞，
不过，也可以搞一个折中的方案，部分经常修改数据使用数据库配置，
部分不常修改使用文件配置等等。



























