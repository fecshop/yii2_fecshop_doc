Fecmall Request Url初始化
==================

> 这里讲述的是在fecmall初始化的过程中，Request Url部分的初始化


当我们访问 `https://fecshop.appfront.fancyecommerce.com/raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122`,

这是一个伪静态的url，为了seo，下面我们说一下具体的实现过程

需要seo的入口，只有appfont  apphtml5这两个入口，对于appserver，appapi等入口
是不需要的，因此这个配置是在入口中的配置加载
，下面以appfront入口为例介绍

3.1、request component config

yii2的url的初始化是在 request component 中，打开文件：
@fecshop/app/appfront/config/appfront.php配置文件可以看到：

```
'request' => [
    'class' => 'fecshop\yii\web\Request',
    ...
]
```

我们打开这个文件： `@fecshop\yii\web\Request.php`,
可以看到该文件将`\yii\web\Request` 的`resolveRequestUri()`
方法进行了重写，在86行可以看到代码：
`Yii::$service->url->getOriginUrl($urlKey);` ，指的是通过url services
的getOriginUrl()方法，得到原来的urlkey，也就是将 `https://fecshop.appfront.fancyecommerce.com/raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122`,
，解析出来urlKey:`raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122`
然后通过`Yii::$service->url->getOriginUrl($urlKey);`，去数据库中查询出来原来的
urlkey，也就是，去mongodb数据库（默认是放到mongodb里面），
url_rewrite表中查询：

```
{
 "custom_url_key": "/raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122"
}
```

得到的结果为：

```
 {
   "_id": ObjectId("580835d0f656f240742f0b7d"),
   "created_at": NumberLong(1476933072),
   "updated_at": NumberInt(1512465616),
   "type": "system",
   "custom_url_key": "/raglan-sleeves-letter-printed-crew-neck-sweatshirt-53386451-77774122",
   "origin_url": "/catalog/product/index?_id=580835d0f656f240742f0b7c"
}	
```

查询得到结果为： `/catalog/product/index?_id=580835d0f656f240742f0b7c`

这样就找到了原来的url。

对于`Yii::$service->url`,对应的class文件：`@fecshop/services/Url.php`的
`actionGetOriginUrl($urlKey)`方法

```
 protected function actionGetOriginUrl($urlKey)
    {
        return Yii::$service->url->rewrite->getOriginUrl($urlKey);
    }
```

进而执行的是 `@fecshop/services/url/Rewrite.php`

进而执行的是 `@fecshop/services/url/rewrite/RewriteMongodb.php`

```
public function getOriginUrl($urlKey)
{
    $UrlData = $this->_urlRewriteModel->find()->where([
        'custom_url_key' => $urlKey,
    ])->asArray()->one();
    if ($UrlData['custom_url_key']) {
        return $UrlData['origin_url'];
    }
}
```