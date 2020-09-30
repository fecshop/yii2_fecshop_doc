Fecmall开发环境切换成生产环境
==================


### 关于开发环境和生产环境

他们的差别在于log日志和errorHanndler的处理

`开发环境`：`dev`模式（develop），会将报错信息全部暴漏出来，适合开发环境

`生产环境`：`prod`模式（product），也就是线上环境，该环境下，会将报错信息隐藏,
但是可以报出错误号，然后通过错误号可以在后台查看
譬如：`{"code":500,"error_no":"5a43620fd70d7d1edc00320b"}`,
关于errorHanndler ，详细参看：http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_error_handler.html



### 切换开发环境和线上环境

需要进行切换的入口有：appfront | apphtml5 | appapi | appserver ， 下面以@app代之这些入口。

1.将`生产环境`切换成`开发环境`（将 `prod` 改成 `dev` ）

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

2.将`开发环境`切换成`生产环境`（将 `dev` 改成 `prod` ）



```
defined('YII_DEBUG') or define('YII_DEBUG', true);
defined('YII_ENV') or define('YII_ENV', 'dev');
```
改成

```
defined('YII_DEBUG') or define('YII_DEBUG', false);
defined('YII_ENV') or define('YII_ENV', 'prod');
```

对于本地开发环境，进行线上发版，已经要将dev环境切换成prod环境



如果您还有其他问题，可以在这里发帖子：http://www.fecmall.com/topic/515

























