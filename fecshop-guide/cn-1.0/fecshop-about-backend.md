Fecshop 关于后台部分
====================


页面缓存指的是在服务器端缓存整个页面的内容。随后当同一个页面被请求时，内容将从缓存中取出，而不是重新生成。

页面缓存由 [[yii\filters\PageCache]] 类提供支持，该类是一个[过滤器](structure-filters.md)。它可以像这样在控制器类中使用：

```php
public function behaviors()
{
    return [
        [
            'class' => 'yii\filters\PageCache',
            'only' => ['index'],
            'duration' => 60,
            'variations' => [
                \Yii::$app->language,
            ],
            'dependency' => [
                'class' => 'yii\caching\DbDependency',
                'sql' => 'SELECT COUNT(*) FROM post',
            ],
        ],
    ];
}
```
