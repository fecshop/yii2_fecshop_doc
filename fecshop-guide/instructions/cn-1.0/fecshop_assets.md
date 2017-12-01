Fecshop Assets
=============

> assets 管理的是css  js  以及css中出现的img等静态资源

### 原理

这个可以参看帖子：http://www.fecshop.com/topic/432

### 设置

对于后台`appadmin`，因为不会涉及到jscss的重构等，因此使用的是Yii2原声的asset。

而`apphtml5`  `appfront`涉及到多模板机制，因此fecshop进行了封装，
使用的是`page asset services`，打开文件

@appfront/config/fecshop_local_services/Page.php

就可以看到配置

```
'asset' => [
    'class' => 'fecshop\services\page\Asset',
    // 在js后面加一个v参数，修改js后，更改v参数，否则，浏览器会使用缓存。
    // /assets/dbdba3fa/js/js.js?v=2
    'jsVersion'        => 1,
    'cssVersion'       => 1,
    /**
     * @var string the root directory string the published asset files.
     * 设置: js和css的发布路径
     * 譬如设置为：'@appimage/assets'，也可以将 @appimage 换成绝对路径
     */
    'basePath' => '@webroot/assets',
    /**
     * @var string the base URL through which the published asset files can be accessed.
     * 设置: js和css的URL路径
     * 可以将 @web 换成域名 ， 譬如  `http:://www/fecshop.com/assets`
     * 这样就可以将js和css文件使用独立的域名了【把域名对应的地址对应到$basePath】。
     */
    'baseUrl' => '@web/assets',
    // 是否每次访问都强制复制css js img等文件到发布地址，true代表每次访问都发布
    // 一般开发环境用true，线上用false。当线上更新jscss文件，可以清空assets发布路径下的文件的方式来更新
    'forceCopy' => true,
],
```

如果你想对`js` `css`使用独立的域名，
那么，您可以设置如下： 

```
'basePath' => '@appimage/assets',   //如果没有这个路径请新建该路径
'baseUrl' => 'http://yourdomain.com/assets',   // 将这个域名解析到@appimage
```

如果您想要使用cdn，那么，您可以把 `@appimage/assets`文件上传到`cdn`
，然后更改`baseUrl`做指向即可.

       
       
因为fecshop的assets是基于yii2的asssets，因此，您可以了解一下yii2 assets：
http://www.yiichina.com/doc/guide/2.0/structure-assets
