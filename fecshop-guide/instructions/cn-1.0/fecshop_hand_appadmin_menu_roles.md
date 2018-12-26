Fecshop 后台添加菜单，设置权限，并访问 （RBAC）
==========================

> Fecshop 1.6.0.0版本之后，改成了RBAC权限控制，下面的文档是针对1.6.0.0版本之后的。

对于后台增加菜单，参考文档：http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_admin_rbac.html


1.打开@appadmin/config/fecshop_local_services/Admin.php（没有这个文件则自行创建）

在里面添加admin的配置

```
<?php

return [
    'admin' => [
        // 子服务
        'childService' => [
            'urlKey' => [
                'urlKeyTags' => [
                    'blog_article' => 'Blog-Article',
                ],
            ],

            'menu' => [
                'menuConfig' => [
                    'blog' => [
                        'label' => 'Blog',
                        'child' => [
                            'article' => [
                                'label' => 'Article',
                                'child' => [
                                    'article_manager' => [
                                        'label' => 'Manager Article',
                                        'url_key' => '/blog/article/manager',
                                    ],
                                ],
                            ],
                        ],
                    ],

                ],
            ],
        ],
    ],
];
```

上面添加了资源tag `Blog-Article`，然后添加了一个菜单 Blog(一级菜单)-->Article(二级菜单) --> Manager Article（三级菜单）

这样我们在配置中添加完成


2.后台添加资源，权限组添加资源

2.1添加资源

![](https://i.loli.net/2018/12/21/5c1c4837aa732.png)

2.2权限组添加上面步骤创建的资源，点击菜单Manager Role

![](https://i.loli.net/2018/12/21/5c1c48575c5e7.png)

2.3刷新缓存

![](https://i.loli.net/2018/12/21/5c1c4889598ae.png)

然后浏览器刷新后台页面，就可以看到菜单了

3.鼠标放到菜单上面，可以看到url

![](https://i.loli.net/2018/12/21/5c1c48bf3304f.png)

点击后是404，这说明我们没有新建相应的controller

![](https://i.loli.net/2018/12/21/5c1c48d995e8c.png)

下面新建相应的controller就可以了


### 创建  blog/article/manager

也就是新建一个blog module，然后建立ArticleController文件，然后创建 actionManager()方法


1.创建模块配置文件：@appadmin/config/fecshop_local_modules/Blog.php ， 添加内容

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 * 这是一个例子模块，用于展示一下如何二次开发，非fecshop必要模块
 */
return [
    'blog' => [
        'class' => '\appadmin\local\local_modules\Blog\Module',
    ],
];

```

2.创建模块入口文件：@appadmin/local/local_modules/Blog/Module.php ， 内容如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace appadmin\local\local_modules\Blog;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class Module extends \fec\AdminModule
{
    public function init()
    {
        //echo 1;exit;
        // 以下代码必须指定
        $this->controllerNamespace = __NAMESPACE__ . '\\controllers';
        $this->_currentDir = __DIR__;
        $this->_currentNameSpace = __NAMESPACE__;

        // 指定默认的man文件
        $this->layout = '/main_ajax.php';
        parent::init();
    }
}


```


3.创建controller文件：2.创建模块入口文件：@appadmin/local/local_modules/Blog/controller

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace appadmin\local\local_modules\Blog\controllers;

use fecshop\app\appadmin\modules\AppadminController;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class ArticleController extends AppadminController
{
    public function actionManager()
    {
        echo 'blog article';
        //$data = $this->getBlock()->getLastData();

        //return $this->render($this->action->id, $data);
    }

}


```


后台访问，可以看到访问这个controller，可以访问了

![](https://i.loli.net/2018/12/21/5c1c4c05099e7.png)

这个菜单里面的其他的url，譬如编辑url，删除url，都需要去资源管理哪里添加资源，然后将资源添加到当前用户所在的权限组，刷新缓存才可以

基于rbac的权限控制，在权限方面可以做的很细粒度（比基于菜单的权限控制好很多），但是开发过程中就会复杂一些，需要做的步骤更多一些，不过理解了原理也是很轻松地
