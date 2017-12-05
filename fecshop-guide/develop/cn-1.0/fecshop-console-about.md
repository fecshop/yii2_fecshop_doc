Fecshop console 介绍和配置
=========================

> 关于该入口的描述和说明


### console 介绍

console 是fecshop其中的一个入口，作为脚本执行端，
处理的都是在后台跑的脚本，以命令行的方式执行，大致分为2种：

1.周期性跑的脚本，需要在cron中进行设置，譬如：

```
05 * * * * /bin/bash /www/web/fecshop/vendor/fancyecommerce/fecshop/shell/urlRewrite.sh  >> /www/web_logs/fecshop/urlRewrite.log 2>&1
```

说明：

`05 * * * *` : cron 设置周期的部分，具体详细自行搜索

`/bin/bash` : 跑shell脚本执行的命令

`/www/web/fecshop/vendor/fancyecommerce/fecshop/shell/urlRewrite.sh` : shell 文件的路径，这个文件要设置成可执行权限，可以设置成755

`>> /www/web_logs/fecshop/urlRewrite.log 2>&1` ：  脚本的输出，写入到log文件中，此文件要设置可写权限，可以设置成777  （chmod 777 /www/web_logs/fecshop/urlRewrite.log）

设置完后，就可以周期性的执行脚本了

2.手动执行的脚本，也就是只有在用到的时候才会手动执行，并不需要
在计划任务中设置。

### console 说明

关于Yii2的命令执行，可以参看文档：[Yii2 console](http://www.yiichina.com/doc/guide/2.0/tutorial-console)

fecshop 安装时使用的migrate，也是console执行命令方式进行的。

在fecshop根目录，打开 `./yii` 文件，就可以看到入口文件（对于web
执行的端口，是index.php文件）。打开后，可以看到里面的内容：

```
$application = new yii\console\Application($config);

$exitCode = $application->run();
exit($exitCode);
```

除了上面的代码部分和其他的入口的index.php 不一样，其他的内容大致一样
（当然，除了头部的 `#!/usr/bin/env php`）,
也就是，执行的对象是`yii\console\Application($config)`

console 入口本地配置文件在 `@console/config/` 下面，可以在这里进行配置
，就像和其他端口一样。

### console 开发

> 除了fecshop提供的脚本，您可以写一些新的脚本满足自己的需求，
> 在写之前，您需要了解一下Yii2 console机制。

和其他入口的写法类似，写`module`，以及里面的`controller`，
不同的是执行的方式不同，譬如：

您建立的module：`mycustomer`，controller：`MyaccountController`，
action：`actionMylogin($email,$password)`,
那么您执行的命令为：

```
./yii mycustomer/myaccount/mylogin 2358qq.com 111111
```

即可执行该controller对应的action方法，
参数 `2358qq.com` 将赋值到action方法的`$email`参数，
`111111`将赋值到action方法的`$password`参数,
然后您就可以在action方法中写您的实现了


另外，对于大数据批处理分页，如果使用php循环查询计算，如果百万数据
会使内存溢出，因此，可以通过shell的方式控制，譬如：

```
#!/bin/sh
# 得到数据的总页数
pageCount=`./yii customer/order/getpagecount`
echo "There are $pageCount pages to Sync"
for (( i=1; i<=$pageCount; i++ ))
do
# 按照页数循环，开启php进程进行处理
   ./yii customer/order/list  $i   
   echo "Page $i done"
done
echo "foreach component"

```

我们在Customer模块中的`OrderController`中新建方法
`actionList($page)`，`$page` 就是上面脚本传递的参数 `$i` ,
这样我们就可以处理一页的数据，进程退出，
然后下一个循环另起新的php进程，即使几亿的数据遍历，
php也不会内存溢出。














