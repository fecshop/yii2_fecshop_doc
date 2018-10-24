Fecshop 如何重写fecadmin库包layout文件
==================================

> 对于后台，大多数文件是在fecshop的appadmin部分里面，
而后台的实现依赖于fecadmin库包，如果有需求涉及到重写该部分，可以看本文的例子


对于fecshop的后台appadmin文件，是在：https://github.com/fecshop/yii2_fecshop/tree/master/app/appadmin

对于appadmin，有一些使用的是
https://github.com/fecshop/yii2_fec_admin/tree/master/views/layouts
这个库包下面的layout文件，本文讲述如何重写这些文件

详细讲解：


fecshop的库包yii2_fecshop 是依赖于 https://github.com/fecshop/yii2_fec_admin

在fecshop如何重写`fecadmin`库包里面的`layout`呢?

对于fecshop的`@appadmin`里面的`layout`文件，可以在本地theme里面新建相应的theme文件进行覆盖即可，
而对于`fecadmin`的layout文件, 有一部分已经被fecshop的`@appadmin`重写，在
https://github.com/fecshop/yii2_fec_admin/tree/master/views/layouts 下面
可以看到重写的一部分文件。

标注：对于 fecadmin的layout文件是在:https://github.com/fecshop/yii2_fec_admin/tree/master/views/layouts 下面
，fecshop已经重写了一部分：https://github.com/fecshop/yii2_fecshop/tree/master/app/appadmin/theme/base/default/layouts

因此，对于这部分，您在本地theme部分新建相应的文件就可以覆盖fecshop的layout文件，来实现重写

重写theme参看文档：http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-theme.html


2.对于header.php 等其他文件，存在于fecadmin的部分layout如何重写呢？

解析：对于 Header.php Footer.php 都是在主体layout文件中调用的，譬如在：
https://github.com/fecshop/yii2_fecshop/blob/master/app/appadmin/theme/base/default/layouts/login.php
和
https://github.com/fecshop/yii2_fecshop/blob/master/app/appadmin/theme/base/default/layouts/dashboard.php
进行了调用，代码如下：

```
use fecadmin\views\layouts\Header;

...

<?= Header::getContent();  ?>
```

我们你有两种方法重写，通过重写主体layout文件（譬如：dashboard.php）内容部分的方式 ， 和， classMap的方式。

下面以重写Header.php为例子，手把手：

2.1 本地theme新建 `layouts/login.php` 和 `layouts/dashboard.php`
然后 您在本地新建一个header文件，将`use fecadmin\views\layouts\Header;` 改成您自己的header即可

下面是详细步骤：


2.1.1新建文件：@appadmin/theme/local/theme01/layouts/Header.php文件
, 这个文件继承 \fecadmin\views\layouts\Header，内容如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
namespace appadmin\theme\local\theme01\layouts;
use Yii;
use fec\helpers\CUrl;
class Header extends \fecadmin\views\layouts\Header{
    public static function getContent(){
        return '<div class="headerNav">
				<a target="_blank" class="logo" href="http://www.fecshop.com">FECSHOP</a>

				<a style="color:#fff; display: block; height: 21px;position: absolute; right: 10px;top: 18px;z-index: 31;"
				href="'.CUrl::getUrl("fecadmin/logout").'">
					退出
				</a>
			</div>';

    }


}



?>
```
您想重写那个方法，就添加那个方法，这个就是您想要重写的Header.php部分的内容。

2.1.2重写dashboard.php和login.php的内容，更改调用，下面以`dashboard.php`为例子：

新建文件：@appadmin/theme/local/theme01/layouts/dashboard.php，将
@fecshop/app/appadmin/theme/base/default/layouts/dashboard.php的内容复制进去

然后将`layouts/dashboard.php`文件内容部分的 `use fecadmin\views\layouts\Header;` 更改成
`use appadmin\theme\local\theme01\layouts\Header;`,也就是上面新建的Header即可。

对于login.php也需要做类似的更改，因为目前主体layout只有dashboard.php和login.php两个，没有其他的
，因此，您可以参考更改`dashboard.php`的方式更改`login.php`。

这样就完成了`Header.php`文件的重写



2.2您可以通过yii2的classMap的方式重写`Header.php`

2.2.1添加classMap重写配置，打开文件：`appadmin/config/YiiClassMap.php`
，在配置数组中添加：

```
'fecadmin\views\layouts\Header' => '@appadmin/theme/local/theme01/layouts/Header.php',
```


2.2.1新建文件：@appadmin/theme/local/theme01/layouts/Header.php文件
, 将 @fecadmin/views/layouts/Header.php的内容全部复制进去.

> 通过classMap重写的方式，是不能使用继承的，因为这种方式是完全替换掉，
因此你需要将全部内容复制过来。

然后在文件 @appadmin/theme/local/theme01/layouts/Header.php文件 中修改您需要重写的代码函数即可。


使用classMap进行重写，参考资料：http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-rewrite-func.html#7yii2classclassmapfecshop
