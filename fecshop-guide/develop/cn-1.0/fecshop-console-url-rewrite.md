url rewrite:生成脚本
=========================

> 为了网站的seo考虑，我们需要在url中出现我们页面的关键字，因此，就需要自定义url，
> 也就是伪静态自定义url，我们需要为数据生成唯一的url_key，然后写入到url_rewrite表中，
> 在产品，分类编辑保存的时候，就会把这些数据保存到url_rewrite，详细可以去查看save()方法中
> 执行的具体代码，当产品和分类删除的时候，也会在url_rewrite中做相应的删除操作，
> 关于Fecshop的url rewrite功能，可以参看 [Fecshop Url重写](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_url_rewrite.html)



### 脚本

> sh脚本只能在类unix（linux）系统中执行，在window mac，自行搜索解决（可以搜索：windows执行shell脚本）

`路径`：`@fecshop/shell/urlRewrite.sh`

`执行`：进入到文件路径，直接执行

```
cd vendor/fancyecommercefecshop/shell/
sh urlRewrite.sh
```

执行log:

```
[root@iZ942k2d5ezZ shell]# sh urlRewrite.sh 
There are 49 products to process
There are 1 products pages to process
##############ALL BEGINING###############
Page 1 done
There are 31 categorys to process
There are 1 categorys pages to process
##############ALL BEGINING###############
Page 1 done
##############ALL COMPLETE###############
[root@iZ942k2d5ezZ shell]# sh urlRewrite.sh 
There are 48 products to process
There are 1 products pages to process
##############ALL BEGINING###############
Page 1 done
There are 31 categorys to process
There are 1 categorys pages to process
##############ALL BEGINING###############
Page 1 done
##############ALL COMPLETE###############
[root@iZ942k2d5ezZ shell]# 
```

执行，就会遍历所有产品和分类，将其url_key写入到url_write表中。














