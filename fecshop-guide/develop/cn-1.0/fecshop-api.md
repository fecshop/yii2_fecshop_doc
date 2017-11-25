Fecshop Api 介绍和配置
===========

> fecshop api这个入口的定位是和第三方系统对接的api部分，譬如和ERP，
> 进行订单传递和产品刊登等，以及erp把订单的物流状态传递个fecshop网站
> 等等


### 配置：

fecshop appapi的配置文件为：`@fecshop/app/appapi/config/appapi.php`

本地appapi的配置文件路径为：`@appapi/config/fecshop_local.php`

**1.速度控制**

>  速度控制，只对需要token验证的api有效。


打开文件：`@appapi/config/fecshop_local.php`，
将下面的代码中的enable 的值改为`true`即可。

```
        'rateLimit'             => [
            'enable'=> false,   // 是否开启？默认不开启速度控制。
            'limit' => [120, 60], // 速度控制[120,60] 代表  60秒内最大访问120次，
        ]
```

速度控制，只对需要access-token的api有效，开启速度控制，访问api后，
在response header中可以发现如下参数：

`X-Rate-Limit-Limit`: 同一个时间段所允许的请求的最大数目;

`X-Rate-Limit-Remaining`: 在当前时间段内剩余的请求的数量;

`X-Rate-Limit-Reset`: 为了得到最大请求数所等待的秒数。

调用fecshop api的第三方系统，可以根据这些信息，来控制好访问
api的频率。

**2.api response header 参数介绍**

> 在访问列表类型的api时，在response header里面会有如下参数，譬如访问`/v1/article/list`
> 在response header里面就会看到下面4个X大头的参数。

`X-Pagination-Total-Count`: 资源所有数量;

`X-Pagination-Page-Count`: 页数;

`X-Pagination-Current-Page`: 当前页(从1开始);

`X-Pagination-Per-Page`: 每页资源数量;

`Link`: 允许客户端一页一页遍历资源的导航链接集合.


**3.设置token过期时间**

可以在本地配置文件：`@appapi/config/fecshop_local_services/Session.php` 中配置如下：

```
'timeout' => 3600,
// 【对phpsession 无效】当过期时间+session创建时间 - 当前事件 < $updateTimeLimit ,则更新session创建时间
'updateTimeLimit' => 600,
// 【不可以设置phpsession】默认为php session，只有当 \Yii::$app->user->enableSession == false时，下面的设置才有效。
// 存储引擎  mongodb mysqldb redis
'storage' => 'SessionMysqldb',
```

`timeout`: token的过期时间（秒），设置该参数即可设置token的过期时间

**4.开发方式**

> 如果您是推数据给第三方系统
> ，这种情况属于您调用第三方的接口，而不是提供，因此，您可以在console入口中写一个批处理
> 脚本，然后在linux cron中设置定时任务，进行定时推送数据相应的接口中
> ，如果您提供api给第三方系统使用，那么需要本入口提供api支持，可以参看下面的内容。

因为和第三方进行对接，有很多自定义的地方，因此，
除了fecshop默认提供的api之外，您可能要做自己二开的api


4.1 不需要用户安全认证，任何人都可以直接访问的接口

这种情况很少，一般都需要做用户登录认证，如果您有这种情况，
那么，您新建的controller可以继承
`fecshop\app\appapi\modules\AppapiController`，

譬如：登录账户获取token的接口：`@fecshop\app\appapi\modules\V1\controllers\AccountController`

4.2 需要用户安全认证，只有合法的用户才能访问该接口

一般和第三方系统交互，都需要用户做登录获取token后，然后通过token做合法性认证，
这类方面的需求，那么，您新建的controller可以继承
`fecshop\app\appapi\modules\AppapiTokenController`

继承后，访问您新建的controller里面的action方法，都需要token验证，
token验证不通过将不允许访问api。

关于token的获取和token的使用详细，可以参看文章：
[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)




