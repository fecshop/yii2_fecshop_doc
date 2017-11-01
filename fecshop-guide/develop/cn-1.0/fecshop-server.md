Fecshop 服务端说明
============

> fecshop server 是和app类客户端 对接的部分，
> fecshop提供了服务端的api，以及用vue做的客户端，
> ，您可以使用fecshop的appserver api，开发您的app（terry 不会做ios 安卓app），
> 当然，如果您使用vue，可以使用fecshop vue的。

demo地址： http://demo.fancyecommerce.com/#/

github地址： https://github.com/fecshop/vue_fecshop_appserver



### 1.实现类似session的功能

客户端请求数据后，如果在response headers中存在 `fecshop-uuid` （Yii::$service->session中的常量UUID），
则客户端需要保存`fecshop-uuid`的值（如果和客户端上次存储的值不同，则需要更新值），

然后在后面的每次请求中，
request headers都需要带上参数 `fecshop-uuid`，

`fecshop-uuid`:这个是用户的唯一key
,是在 `Yii::$service->session->getUUID()`中生成，用来标示用户，
fecshop实现了一个类似session的功能，提供给appserver使用，
因为有一些功能需要使用到类似session的功能，譬如验证码的存储，无登录用户的购物车数据等存储。



`@fecshop/config/services/Session.php` 中设置: 超时时间 ， 更新创建时间 ， 以及存储引擎的设置

```
// 【对phpsession 无效】设置session超时时间, 
'timeout' => 3600,
// 【对phpsession 无效】当过期时间+session创建时间 - 当前事件 < $updateTimeLimit ,则更新session创建时间
'updateTimeLimit' => 600,
// 【不可以设置phpsession】默认为php session，只有当 \Yii::$app->user->enableSession == false时，下面的设置才有效。
// 存储引擎  mongodb mysqldb redis
'storageEngine' => 'mysqldb',
```


### 2.获取登录 access-token

通过访问`/customer/login`来获取 `access-token` ，如果request headers 里面存在`access-token`，则会验证 `access-token` 的有效性，
有效则返回该 `access-token`

如果没有，则会从 request post中获取 `email` 和 `password`，验证成功后，
生成`access-token`返回json格式


另外，服务端还需要做一部分用户登录的其他事情，譬如购物车合并等操作。

### 3.【登录用户】访问

用户在上面哪一步获取`access-token`成功后，每次请求都需要在request headers里面加上`access-token`，
这个作为用户登录的`access-token`.

作为服务端appserver，需要用户登录验证的部分，
controller都需要继承
`@fecshop/app/appserver/modules/AppserverTokenController.php`
，在这个controller的behaviors()中已经加入了用户登录的验证，如果用户
没有登录，将会返回json报错信息


### 4.登录用户的 过期时间 和 速度控制

在 `@fecshop/app/appserver/config/appserver.php` 里面设置

```
// access-token 过期时间。
'accessTokenTimeout'    => 86400,
// 速度控制[120,60] 代表  60秒内最大访问120次，
'rateLimit'             => [120, 60],
```

### 5. 客户端存储

客户端需要做的事情：

#### 5.1用户唯一识别存储：

如果服务端response headers中含有参数`fecshop-uuid`，那么需要把这个值存储
起来，如果本地已经存储过一次，那么检查是否一致，如果不一致，把当前
的`fecshop-uuid`覆盖 之前存储`fecshop-uuid`。

后面的客户端的每次请求，在request headers中都需要带上`fecshop-uuid`

#### 5.2客户端用户登录：

用户访问api `/customer/login`来获取 `access-token` ，获取后需要
在客户端进行存储。

后面的客户端的每次请求，在request headers中都需要带上`access-token`


### 6. 服务端的页面类型。

1.无状态页面：不需要验证的页面，譬如首页，产品页，都是无状态的

2.需要`uuid`页面：譬如注册页面的验证码，无登录用户把产品加入购物车

3.需要`access-token`页面：譬如用户中心，下单页面。

当然存在一些页面，`uuid` 和 `access-token` 都需要。









