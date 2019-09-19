Fecmall-应用Config文件
==============





> 这是一个应用扩展config文件的例子




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