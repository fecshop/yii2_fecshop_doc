Fecshop 如何开发插件扩展
====================

> 您可以以composer库包的方式发布您的插件扩展


### 1.如何发布composer库包

该部分知识可以参看:[Github  如何制作Composer包](fecshop-pkg-github-composer.md)

### 2.如何做插件，模板等扩展

通过上面的步骤，我们可以把github的项目打包成composer库包，
现在我们的库包，希望加入到fecshop的配置中。

2.1您的库包，需要做一个配置文件

譬如：
https://github.com/fecshop/yii2_fecshop_redis_cart/blob/master/config/fecshop_rediscart.php

在composer安装完成后，需要把这个文件复制到
`@common/config/fecshop_third_extensions/`文件夹下面，
复制到这个文件夹后，fecshop初始化的时候就会加载这个文件夹下面的配置，
下面说一下配置文件的语法

2.2配置文件的语法

打开文件:https://github.com/fecshop/yii2_fecshop_app_advanced/edit/master/common/config/fecshop_third_extensions/fecshop_example.php

代码如下：

```
return [
    /**
     * 下面是第三方扩展库包的配置方式
     */
    // 这个是扩展extensions的总开关，true代表打开
    'enable' => true, 
    // 各个入口的配置
    'app' => [
        // 1.公用层
        'common' => [
            // 在公用层的开关，设置成false后，公用层的配置将失效
            'enable' => true,
            // 公用层的具体配置下载下面
            'config' => [
                'services' => [
                    
                ],
                'modules' => [
                    
                ],
            ]
        ],
        // 2.pc层 ,如果不需要这个部分，可以去掉
        'appfront' => [
            // 在pc层的开关，设置成false后，pc层的配置将失效
            'enable' => true,
            // pc层的具体配置下载下面
            'config' => [
                'services' => [
                    //'cms' => [
                    //    'childService' => [
                    //        'article' => [
                    //            'class'            => 'fecshop\services\cms\Article',
                    //            'storage' => 'ArticleMongodb', // ArticleMysqldb or ArticleMongodb.
                    //        ],
                    //    ],
                    //],  
                ],
                'modules' => [
                    
                ],
            ]
        ],
        // 3.手机wap
        'apphtml5' => [
            'enable' => true,
            'config' => [
                'services' => [
                    
                ],
                'modules' => [
                    
                ],
            ]
        ],
        // 4.后台
        'appadmin' => [
            'enable' => true,
            'config' => [
                'services' => [
                    
                ],
                'modules' => [
                    
                ],
            ]
        ],
        // 5.和第三方系统对接的入口
        'appapi' => [
            'enable' => true,
            'config' => [
                'services' => [
                    
                ],
                'modules' => [
                    
                ],
            ]
        ],
        // 6.手机app VUE等api入口
        'appserver' => [
            'enable' => true,
            'config' => [
                'services' => [
                    
                ],
                'modules' => [
                    
                ],
            ]
        ],
        // 7.后台脚本入口
        'console' => [
            'enable' => true,
            'config' => [
                'services' => [
                    
                ],
                'modules' => [
                    
                ],
            ]
        ],
    ],
];

```

上面这个例子中，对各个参数都进行了说明，您可以细看上面的注释。

1.在外层做了一个总开关 `enable`，如果设置成`false`，则该文件的所有配置都失效

2.各个入口以及公用`common`的配置，如果是公用的部分，就写到`common`里面，如果是
某个入口的配置，那么就放到相应的部分下面即可

3.入口内部配置，`enable`是这个`入口`的配置，如果设置成`false`，则该`入口`的配置失效，
扩展的配置写入到`config`中，fecshop初始化的时候，会将
`config`对应的配置数组内容合并到fecshop的配置中，

4.这样您就可以通过配置的方式扩展功能，重写fecshop功能了。


有了这个规则，我们看一个例子，也就是redis 购物车插件的例子：

https://github.com/fecshop/yii2_fecshop_redis_cart/blob/master/config/fecshop_rediscart.php

```
<?php
/**
 * FecShop file.
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
return [
    /**
     * 下面是第三方扩展库包的配置方式
     */
    // 这个是扩展extensions的总开关，true代表打开
    'enable' => true, 
    // 各个入口的配置
    'app' => [
        // 1.公用层
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

其中下面的代码将会附加到fecshop的初始化中(common)

```
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
```

上面配置代表的是重写fecshop cart services部分的功能，改成redis存储
购物车信息。


### 优先级

1.各个库包是按照字母顺序加载的，然后通过`array_merge`函数合并配置,
后面的库包的优先级要高于前面的库包，
如果您想要某个库包的优先级最高，那么您可以在库包的名字加个`zzz`字母开头，让名字在
按照字母排序，排在最后。

2.本地开发配置  第三方开发配置  fecshop配置的优先级顺序为：

```
本地开发配置优先级 > 第三方开发配置 > fecshop配置
```

### 最后

这样，您就可以发布自己的库包，然后通过配置，扩展或者重写fecshop的
功能，来达到您的目的

插件列表：[Fecshop 官方扩展列表](fecshop-pkg-list.md)

您开发的fecshop可以发布出来，让大家方便的使用。



