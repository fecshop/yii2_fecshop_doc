Fecmall-应用配置文件Config.php配置详解
==============


> 从应用配置文件config.php，对应用开发进行详细说明


### config文件例子


在扩展插件目录的`config.php`文件，是fecmall初始化加载插件的配置内容，无论您重写fecmall的类文件，
还是开发新的功能类文件，都需要在`config.php`文件中进行配置，下面详细阐述`config.php`文件的配置数组语法。

```


<?php
/**
 * Fect File
 * @author terry
 */

/**
 * 这里设置namespace，也就是该应用的namespace，
 * addons: 是应用安装的文件包
 * fecmall： 开发者的package包名，这个是在开发者资质申请的时候填写的
 * furnilife_theme： 应用文件夹名，这个是在应用市场，添加应用的时候填写的
 */
Yii::setAlias('@fectfurnilife', dirname(dirname(dirname(__DIR__))).'/addons/fecmall/furnilife_theme/');

return [
    // 插件信息，下面是一些描述信息没有太多的用处
    'info'  => [
        'name' => 'theme_furnilife',
        'title' => 'furnilife theme',
        'description' => 'furnilife theme',
        'author' => 'terry',
    ],
    // 插件管理部分
    'administer' => [
        /**
         * 应用的安装部分配置，也就是应用在下载zip文件，解压后，进行安装步骤调用的函数，
         * 您可以在该函数中进行数据库的初始化，文件的复制等等初始化操作
         */
        'install' => [
            'class' => 'fectfurnilife\administer\Install',
            // 其他引入的属性，类似yii2组件的方式写入即可
            'test' => 'test_data',
        ],
        /**
         * 应用的升级部分配置，当您的应用需要进行升级，那么升级部分写道这里
         * 如果应用有多个升级版本，那么在用户第一次安装的时候，先执行install, 然后执行upgrade，最后就是最新版本了
         */
        'upgrade' => [
            'class' => 'fectfurnilife\administer\Upgrade',
        ],
         /**
         * 应用的卸载部分，您可以在这里写上数据库的删除，以及文件的删除等等
         */
        'uninstall' => [
            'class' => 'fectfurnilife\administer\Uninstall',
        ],
    ], 
    // 各个入口的配置
    'app' => [
        // 1.appfront层
        'appfront' => [
            // appfront入口的开关，如果false，则会失效
            'enable' => true,
            'config' => [
                
                // yii class rewrite map，也就是 yiiClassMap 的配置写道这里
                'yiiClassMap' => [
                    
                ],
                // 重写model和block的部分写到这里
                'fecRewriteMap' => [
                    '\fecshop\app\appfront\modules\Cms\block\home\Index'  => '\fectfurnilife\app\appfront\modules\Cms\block\home\Index',
                    '\fecshop\app\appfront\modules\Customer\block\address\Edit'  => '\fectfurnilife\app\appfront\modules\Customer\block\address\Edit',
                ],
                // 模块的配置
                'modules' => [
                    'catalog' => [
                        /**
                         * Yii2 controllerMap 重写机制。
                         */
                        'params'=> [
                            //##############################
                            //# 		Product部分设置		 ##
                            //##############################
                            // 产品页面图片的设置
                            'productImgSize' => [
                            ],
                        ],
                    ],
                    
                    'checkout' => [
                        'controllerMap' => [
                            'cartinfo' => 'fectfurnilife\app\appfront\modules\Checkout\controllers\CartInfoController',          
                        ],
                    ],
                    
                    'cms' => [
                        'controllerMap' => [
                            'home' => 'fectfurnilife\app\appfront\modules\Cms\controllers\HomeController',                  
                        ],
                        'params' => [
                        
                    ],
                
                ],
            
            ],
        ],
        // 您可以在这里继续写appadmin,  apphtml5等其他入口的配置
        
        // 如果是公用部分，写道common里面
        'common' => [
            // 在公用层的开关，设置成false后，公用层的配置将失效
            'enable' => true,
            // 公用层的具体配置下载下面
            'config' => [
                'services' => [
                    'cart' => [
                        'class' => 'fecshop\rediscart\services\Cart',
                        // 子服务
                        'childService' => [
                            'quote' => [
                                'class' => 'fecshop\rediscart\services\cart\Quote',
                            ],
                            'quoteItem' => [
                                'class' => 'fecshop\rediscart\services\cart\QuoteItem',
                            ],
                        ]
                    ]
                ],
                'modules' => [
                    
                ],
            ]
        ],
    ],
    
    
];



```

### Config文件创建

您不需要手动创建应用config文件，可以通过fecmall的gii工具，进行创建

[Fecmall-应用Gii初始化工具](http://www.fecmall.com/doc/fecshop-guide/addons/cn-2.0/guide-fecmall-addons-developer-init-tools.html)

### Config 文件语法解析

1.设置namespace命名空间

```
Yii::setAlias('@fectfurnilife', dirname(dirname(dirname(__DIR__))).'/addons/fecmall/furnilife_theme/');
```

设置`@fectfurnilife`对应到文件路径：`./addons/fecmall/furnilife_theme/`


2.应用扩展信息

```
'info'  => [
        'name' => 'theme_furnilife',
        'title' => 'furnilife theme',
        'description' => 'furnilife theme',
        'author' => 'terry',
    ],
```

 这个部分是扩展插件的描述信息，只是文字的描述，无其他任何作用。
 
 
 
 3.扩展插件安装部分
 
```
 // 插件管理部分
    'administer' => [
        /**
         * 应用的安装部分配置，也就是应用在下载zip文件，解压后，进行安装步骤调用的函数，
         * 您可以在该函数中进行数据库的初始化，文件的复制等等初始化操作
         */
        'install' => [
            'class' => 'fectfurnilife\administer\Install',
            // 其他引入的属性，类似yii2组件的方式写入即可
            'test' => 'test_data',
        ],
        /**
         * 应用的升级部分配置，当您的应用需要进行升级，那么升级部分写道这里
         * 如果应用有多个升级版本，那么在用户第一次安装的时候，先执行install, 然后执行upgrade，最后就是最新版本了
         */
        'upgrade' => [
            'class' => 'fectfurnilife\administer\Upgrade',
        ],
         /**
         * 应用的卸载部分，您可以在这里写上数据库的删除，以及文件的删除等等
         */
        'uninstall' => [
            'class' => 'fectfurnilife\administer\Uninstall',
        ],
    ], 
```

扩展插件安装，升级，卸载，需要执行的内容

当您使用Gii工具生成插件文件,：`fectfurnilife/administer/Install.php` ，`fectfurnilife/administer/Upgrade.php` ，
`fectfurnilife/administer/Uninstall.php`  

对于`install`, `upgrade`, `uninstall`，您可以在配置数组中，以注入的方式初始化类变量，
类似于
yii2组件


对于安装，升级，卸载对于的类，在安装的时候会默认执行里面的run()方法，您要做的事情都可以在这里面实现，
一般要做的事情，`sql安装`和`图片复制`


4.

```
'app' => [
    // 1.common层 ，公共部分，也就是下面的各个入口都加载的公用配置，一般model，services等，都是在common里面配置
    'appfront' => [],
    
    // 2.appfront层，pc入口部分，您可以把 appfront 入口的一些配置写到这里
    'appfront' => [],
        
    // 3.apphtml5层，html5入口部分，您可以把 apphtml5 入口的一些配置写到这里
    'apphtml5' => [],
    
    
    // 4.appadmin层，后台入口部分，您可以把 appadmin 入口的一些配置写到这里
    'appadmin' => [],
    
    // 5appbdmin层，多商户商家后台入口部分，您可以把 appbdmin 入口的一些配置写到这里
    'appbdmin' => [],
    
    
    
    // 6.appserver层，vue，微信小程序，app等，为其提供后台api的入口部分，您可以把 appserver 入口的一些配置写到这里
    'appserver' => [],
    
    // 7.appapi层，和第三方系统，譬如erp等进行数据对接的api入口部分，您可以把 appapi 入口的一些配置写到这里
    'appapi' => [],
    
    // 8.console层，console入口部分，一般用来实现一些后台离线脚本，譬如：数据同步，数据计算，数据统计等，您可以把 console 入口的一些配置写到这里
    'console' => [],
    
]


```

各个入口层具体做什么的，这里只是一个简单的说明，不做详细阐述。


5.入口内部配置


以appfront配置举例子

```

// 各个入口的配置
    'app' => [
        // 1.appfront层
        'appfront' => [
            // appfront入口的开关，如果false，则会失效
            'enable' => true,
            'config' => [
            
            ],
        ],
    ],

```

`enable`:配置生效开关，您可以通过设置`true`，`false`来进行开启和关闭某个入口的配置

`config`:配置的详细内容


6.`config`配置详细内容 - 详解

在各个入口里面的`config`数组子项，和普通的二次开发没有区别，是互通的
，您可以看一下fecmall的开发文档：[Fecmall重写功能](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-rewrite-func.html)

以及其他的一些fecmall的开发文档，下面进行一下详细说明


```
'config' => [
    // yii class rewrite map，也就是 yiiClassMap 的配置写道这里
    'yiiClassMap' => [
        
    ],
    // 重写model和block的部分写到这里
    'fecRewriteMap' => [
        '\fecshop\app\appfront\modules\Cms\block\home\Index'  => '\fectfurnilife\app\appfront\modules\Cms\block\home\Index',
        '\fecshop\app\appfront\modules\Customer\block\address\Edit'  => '\fectfurnilife\app\appfront\modules\Customer\block\address\Edit',
    ],
    // 模块的配置
    'modules' => [
        'checkout' => [
            'controllerMap' => [
                'cartinfo' => 'fectfurnilife\app\appfront\modules\Checkout\controllers\CartInfoController',          
            ],
        ],
    ],
    'components' => [
        'i18n' => [
            'translations' => [
                'appfront' => [
                    'basePaths' => [
                        '@fectfurnilife/app/appfront/languages',
                    ],
                ],
            ],
        ],
    ],
    'services' => [
        'customer' => [
            'class' => 'fectfurnilife\services\Customer',
            // 子服务
            'childService' => [
                'smscode' => [
                    'class' => 'fectfurnilife\services\customer\Smscode',
                ],
            ],
        ],
    ],
    
],
```

6.1`yiiClassMap`:该部分是通过yii class rewrite map原理进行重写的部分，这是yii2框架的一种方式，详细参看
:[重写yii2框架的class - classMap的方式](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-rewrite-func.html#7yii2classclassmapfecmall)

这种方式一般用不到，除非一些特殊情况


 6.2`fecRewriteMap`: 重写model和block的部分写到这里， 数组配置左边的key是fecmall的文件路径，
 右边的是重写后的文件路径，您可以将重写的类继承fecmall的原来的类，然后重写相应的函数即可
 
 
 6.3`modules`:模块配置部分，您可以新建新的模块，重写现有模块，
 或者通过`controllerMap`, 重写controller，或者，在当前模块中添加新的
 controller

6.4`components`:组件配置部分，此处的组件，就是yii2框架里面的组件，对于组件部分，一般在公共配置common里面配置
，这样各个入口都可以使用，不需要单独配置，维护也方便

关于组件开发，您可以参看：[Fecmall组件开发](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-develop-component.html)

6.5`services`:服务部分，service是fecmall的核心功能代码部分，此处可以重写已有的service，
也可以创建新的service

关于services开发，您可以参看：[Fecmall services开发](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-develop-services.html)

对于其他的一些细节的二开插件的内容，建议您下载`fecyo扩展`，然后仔细琢磨里面的一些实现，
来搞懂原理，多读源码会了解的更深入。

如果您遇到一些解决比较难的问题，可以论坛发帖，terry 100%回复。

fecmall的扩展插件的具体文件的开发，和本地二次开发的本质是一样的，不同的是加载的方式不一样，因此，在做fecmall扩展插件之前，您
需要先多做本地二次开发，了解语法结构，[fecmall二次开发文档](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-rewrite-func.html)

如果您没有接触过fecmall，建议先多读文档和源码，了解fecmall的机制，做一些简单的本地二次开发
，然后再进行扩展插件开发










