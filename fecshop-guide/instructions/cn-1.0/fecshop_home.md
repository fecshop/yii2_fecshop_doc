fecshop 首页
=============

> fecshop 首页，也就是home页，属于进入网站的主页面

### 1.配置

打开配置文件 `@fecshop/app/appfront/config/appfront.php`
，可以看到如下的代码：

```
// 首页对应的url key
        'urlManager' => [
            'rules' => [
                '' => 'cms/home/index',
            ],
        ],
```        
        
这是Yii2的rules配置，配置` '' => 'cms/home/index',`，
这个配置代表的是首页地址对应 `cms/home/index`，
也就是cms模块下面的HomeController里面的actionIndex()方法，
也就是文件 `@fecshop\app\appfront\modules\Cms\controllers\HomeController.php`
里面的actionIndex()方法，

对于Yii2 controller的知识，可以参看：http://www.yiichina.com/doc/guide/2.0/structure-controllers

对于Yii2模块，可以参看：http://www.yiichina.com/doc/guide/2.0/structure-modules

url routing 可以参看：http://www.yiichina.com/doc/guide/2.0/runtime-routing
 
        
        
        
        
        
        
        
        
        
        
        
        