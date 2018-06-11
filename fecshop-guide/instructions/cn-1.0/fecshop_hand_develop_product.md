Fecshop 生产模式 product 更改成 开发模式 develop
=======================


在安装fecshop的时候，composer安装完成所有的文件，在执行 `./init`的时候，有一个模式选择，
`product` 还是 `develop`,

安装的时候建议选择 `develop` ， 他们的差别在于log日志和errorHanndler的处理，
因为生产环境，报错信息不能报出，但是可以报出错误号，然后通过错误号可以在后台查看
譬如：`{"code":500,"error_no":"5a43620fd70d7d1edc00320b"}`,
关于errorHanndler ，详细参看：http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_error_handler.html

如果您安装的时候选择的是`product`，可以将 `product` 改成 `develop` 

打开@app/web/index.php （app代表入口，appfront | apphtml5 | appapi | appserver）

将 

```
defined('YII_DEBUG') or define('YII_DEBUG', false);
defined('YII_ENV') or define('YII_ENV', 'prod');
```

改成

```
defined('YII_DEBUG') or define('YII_DEBUG', true);
defined('YII_ENV') or define('YII_ENV', 'dev');
```

如果您想将 `develop`  改成  `product` ，可以



```
defined('YII_DEBUG') or define('YII_DEBUG', true);
defined('YII_ENV') or define('YII_ENV', 'dev');
```
改成

```
defined('YII_DEBUG') or define('YII_DEBUG', false);
defined('YII_ENV') or define('YII_ENV', 'prod');
```












