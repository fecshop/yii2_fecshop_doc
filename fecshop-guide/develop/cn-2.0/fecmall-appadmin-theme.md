Fecshop Admin 模板Theme
======================

> 本部分介绍的是appadmin后台部分，模板方面的知识


### Appadmin theme

1.遵循fecshop的多模板机制

可以在本地的模板路径：`@appadmin/theme/local/theme01`下面添加view文件，
添加的view文件，将覆盖fecshop默认的view文件

2.设置当前模板：

`@appadmin/config/params.php` 文件下设置

```
'localThemeDir' => '@appadmin/theme/local/theme01',
```

3.如何添加js css文件

在`@appadmin/theme/local/theme01/assets `文件路径下增加`css` 和`js`文件，
譬如：我们新增`@appadmin/theme/local/theme01/assets/css/my.css`
和
`@appadmin/theme/local/theme01/assets/js/my.js`

然后在配置文件中添加js和css的配置，我们可以打开配置文件 `@appadmin/config/fecshop_local_services/Page.php`

```
'asset' => [
    // js 版本号，当更改了js，将这里的版本号+1，生成的js链接就会更改为  xxx.js?v=2 ,
    // 这样做的好处是，js的链接url改变了，可以防止浏览器继续使用缓存，而不是重新加载js文件的问题。
    'jsVersion'        => 1,
    // css 版本号，原理同js
    // 关于版本号更多的信息，请参看：http://www.fancyecommerce.com/2017/04/17/css-js-%E5%90%8E%E9%9D%A2%E5%8A%A0%E7%89%88%E6%9C%AC%E5%8F%B7%E7%9A%84%E5%8E%9F%E5%9B%A0%E5%92%8C%E6%96%B9%E5%BC%8F/
    'cssVersion'    => 1,
    // 是否每次刷新，强制发布js css到web目录（@app/web/assets）？ 开发环境设置为true，正式环境设置为false（你也可以设置为true，但是每次页面的访问（刷新）都会复制js和css文件到@app/web/assets/下面，耗费资源）
    // 线上设置成false，每次访问不会强制复制js和css到发布环境，可以节省资源，但是，当css和js更新后，
    // 需要去@app/web/assets/ 路径下，手动清空所有的文件夹和文件，当assets路径下找不到文件，就会重新复制库包里的js和css到web环境，
    // 这是属于Yii2的知识范畴。
    'forceCopy' => true,
    // js and css config example:
    'jsOptions'	=> [
        # js config 1
        [
            'options' => [
                'position' =>  'POS_END',
            //	'condition'=> 'lt IE 9',
            ],
            'js'	=>[
                'js/my.js',
            ],
        ],
        # js config 2
        //[
        //    'options' => [
        //        'condition'=> 'lt IE 9',
        //    ],
        //    'js'	=>[
        //        'js/ie9js.js'
        //    ],
        //],
    ],
    # css config
    'cssOptions'	=> [
        # css config 1.
        [
            'css'	=>[
                'css/my.css',
            ],
        ],

        # css config 2.
        //[
        //    'options' => [
        //        'condition'=> 'lt IE 9',
        //    ],
        //    'css'	=>[
        //        'css/ltie9.css',
        //    ],
        //],
    ],
    
],
```

按照上面的示例，在 `jsOptions中` 添加js文件配置，
`cssOptions`中添加css文件配置，您可以添加多个js和css文件，譬如上面添加的
是 `'js/my.js',` 和  `css/my.css`，
对应的文件为
`@appadmin/theme/local/theme01/assets/css/my.css`
和
`@appadmin/theme/local/theme01/assets/js/my.js`
文件，其中：

`@appadmin/theme/local/theme01/` ： 为模板路径

`assets`：为js和css存放文件夹

刷新首页，查看源代码，我们可以看到css和js都加载了

```
<link href="/assets/2be7122d/css/my.css?v=1" rel="stylesheet">

...

<script src="/assets/2be7122d/js/my.js?v=1"></script>
```

如果您需要添加新的js和css文件，您可以参考上面的步骤，把您的js和css文件加载进来。


最后，需要注意的是appadmin是`ajax框架`，登录成功后的页面是一个初始页面，
也就是在这个页面加入js 和 css文件。
当您点击左侧菜单的时候，执行的是ajax，只刷新内容部分的内容，因此，这些ajax
就不需要加载js和css了

注意：dwz是没有使用`frame`的,因此，ajax刷新的内容是可以使用首次加载的js文件的。

更多的关于js和css的信息，可以参看: [fecshop 二次扩展 - theme js and css](fecshop-js-css.md)






