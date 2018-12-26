fecshop 配置加速
================

> fecshop配置加速的将fecshop的N个配置文件合并成一个配置文件，
> 进而减少了使用merge合并数组耗费的时间，
> 在并发不高的网站不需要做这个配置加速，影响不大，并发量高
> 的网站推荐使用

### 1.开启方法

1.1生成`单配置文件`

在web（@app/web/）目录下会发现文件index-merge-config.php ，
访问执行：www.domain.com/index-merge-config.php ，就会
把所有的配置合并并写入 @app/merge_config.php中

> 注意，线上系统，就将这个文件的访问进行限制，通过nginx设置密码访问，或者特定ip访问，
等等，让该地址只能自己人访问，生成配置文件。

1.2开启使用单配置文件

打开文件  @app/web/index.php 找到代码行
`$use_merge_config_file = false; `
改成true，即可。

### 2.注意

如果您的配置文件进行了更新，更新后，您需要重新执行一下
www.domain.com/index-merge-config.php ，
否则@app/merge_config.php中的配置还是原来的，
造成配置没有生效。

### 3.帮助

关于单文件配置的原理可以参看文章：[yii2 配置加速 – N个配置文件生成一个配置文件](http://www.fancyecommerce.com/2017/04/10/yii2-%e9%85%8d%e7%bd%ae%e5%8a%a0%e9%80%9f-n%e4%b8%aa%e9%85%8d%e7%bd%ae%e6%96%87%e4%bb%b6%e7%94%9f%e6%88%90%e4%b8%80%e4%b8%aa%e9%85%8d%e7%bd%ae%e6%96%87%e4%bb%b6/)














