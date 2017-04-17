Fecshop 模板（theme）
==============

> fecshop theme也就是多模板机制，详细参看
[fecshop 模板](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-rewrite-func.html#4-fecshopview-js-css)
这里不做详细的叙述。

这里说一下模板的构造，其实就是yii2的模板知识。

打开`@fecshop/appfront/theme/base/default`就进入了模板路径：

`assets` :是 css js img存放的文件路径
`layouts` :是 页面主体部分，也就是从<html>标签开始，进入打开main.php
就可以看到，里面设置了如何添加css js等等。

`widgets` :是fecshop的小部件存放的view部分

`其他文件夹`：是fecshop的view部分，view部分作为content的一部分，
在上面的`main.php`种你可以看到如下的代码：

```
<?= $content; ?>
```

这个就是`view`文件部分内容，最终放到`layout`的html内容的位置。


对于yii2er，对这些并不会太陌生，只要了解了fecshop的模板重写机制就可以了。


多模板机制，详细参看
[fecshop 模板](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-rewrite-func.html#4-fecshopview-js-css)
这里不做详细的叙述。






















