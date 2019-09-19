Fecmall 如何只保留中文语言，去掉其他的所有语言？
==========================================

> 对于Fecmall是多语言的站点，默认的基础语言为英文，对于某些开发者，想要做中文网站，
因此只要中文的语言，其他的统统去掉，也就是单纯的中文站点

下面说一下具体的配置，仅仅以`appfront`入口为例，其他的入口设置参考这个

1.设置语言，将中文外的语言全部去掉，设置默认语言为中文


1.1打开文件`@common/config/fecshop_local_services/FecshopLang.php`,去掉其他语言，设置基础语言为中文,修改完成后的配置文件如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 *
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
return [
    'fecshoplang' => [
        //'class' => 'fecshop\services\FecshopLang',
        //  mongoSearchLangName 在各个语言下字段参考资料如下：（不支持中文）
        //  https://docs.mongodb.com/manual/reference/text-search-languages/#text-search-languages
        'allLangCode' => [
            // 'en_US' 是标准语言简码  code对应的值en取 “标准语言简码”的前两位字符，
            // 该值设置后，进行了产品分类数据的添加后，不能修改，否则会出现部分翻译语言丢失。
            
            'zh_CN' => [
                'code'                    => 'zh',
            ],
        ],
        // 默认语言。
        'defaultLangCode' => 'zh',

    ],
];
```

1.2因为上面设置的`common`部分的配置，根据配置优先级覆盖原则，appfront的`FecshopLang`里面的配置会覆盖common的配置，因此我们需要打开文件 `@appfront/config/fecshop_local_services/FecshopLang.php`
，将默认语言修改为中文，修改完的文件内容如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 *
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
return [
    // 在@common/config/fecshop_local_services中已经进行了全局配置
    // 当然，您可以将上面里面的配置清空，在每一个app里面单独配置。
    'fecshoplang' => [
        'defaultLangCode' => 'zh',
    ],
];
```

1.3打开配置文件：`@appfront/config/fecshop_local_services/FecshopLang.php`。没有改动的配置文件内容是下面的，如果您没有改动，则不需要改动，我的配置文件内容如下：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 *
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
return [
    'fecshoplang' => [
        //'class' => 'fecshop\services\FecshopLang',
        /*
        'allLangCode' => [
            'en_US' => 'en',
            'fr_FR' => 'fr',
            'de_DE' => 'de',
            'es_ES' => 'es',
            'ru_RU' => 'ru',
            'pt_PT' => 'pt',
            'zh_CN' => 'zh',
        ],
        'defaultLangCode' => 'en',
        */
    ],
];
```

2.设置store的默认语言，打开`@appfront/config/fecshop_local_services/Store.php`

我的域名是：`fecshop.appfront.fancyecommerce.com`，其他的语言统统不要，只要中文的，我的配置如下：

```
<?php
   return [
   'store' => [
        'class'  => 'fecshop\services\Store',
        'stores' => [
            // store key：域名去掉http部分，作为key，这个必须这样定义。
            'fecshop.appfront.fancyecommerce.com' => [
                'language'         => 'zh_CN',        // 语言简码需要在@common/config/fecshop_local_services/FecshopLang.php 中定义。
                'languageName'     => '中文',    // 语言简码对应的文字名称，将会出现在语言切换列表中显示。
                'localThemeDir'    => '@appfront/theme/terry/theme01', // 设置当前store对应的模板路径。关于多模板的方面的知识，您可以参看fecshop多模板的知识。
                'thirdThemeDir'    => [ // 第三方模板路径，数组，可以多个路径
                    
                ],  
                'currency'         => 'USD', // 当前store的默认货币,这个货币简码，必须在货币配置中配置
                /*
                 * 当设备满足什么条件的时候，进行跳转。
                 * 这种方式不怎么高效，最好的方式是在nginx中配置。
                 */
                'mobile'        => [
                    'enable'            => false,
                    'condition'         => ['phone', 'tablet'], // phone 代表手机，tablet代表平板，当都填写，代表手机和平板都会进行跳转
                    'redirectDomain'    => 'fecshop.apphtml5.fancyecommerce.com',    // 如果是移动设备访问进行域名跳转，这里填写的值为store key
                    'https'             => false,  // 手机端url是否支持https,如果支持，设置https为true，如果不支持，设置为false
                ],
                // 第三方账号登录配置
                'thirdLogin' => [
                    // facebook账号登录
                    'facebook' => [       //fb api配置 ，fb可以一个app设置pc和手机web两个域名
                        'facebook_app_id'     => '108618299786621',
                        'facebook_app_secret' => '420b56da4f4664a4d1065a1d31e5ec73',
                    ],
                    // google账号登录
                    'google' => [       //谷歌api visit https://code.google.com/apis/console to generate your google api
                        'CLIENT_ID'      => '380372364773-qdj1seag9bh2n0pgrhcv2r5uoc58ltp3.apps.googleusercontent.com',
                        'CLIENT_SECRET'  => 'ei8RaoCDoAlIeh1nHYm0rrwO',
                    ],
                ],
                // 用于sitemap生成中域名。
                'https'            => true,
                // sitemap的路径。
                'sitemapDir' => '@appfront/web/sitemap.xml',
            ],
            
        ],

    ],

];
```

上面的修改大致做了3件事情， 把其他的语言的store去掉，然后修改参数 `language` 和 `languageName`的值对应中文的参数 即可。

3.我们开始测试添加产品

打开后台，添加产品

![](https://i.loli.net/2018/04/06/5ac6ce7762075.png)

![](https://i.loli.net/2018/04/06/5ac6ce845ab51.png)


保存成功后，访问产品，我测试的产品：http://fecshop.appfront.fancyecommerce.com/cn/23777565

因为我测试完后，把多语言还原回来了，因此这个产品的url的中文是有一个后缀`/cn`的.



