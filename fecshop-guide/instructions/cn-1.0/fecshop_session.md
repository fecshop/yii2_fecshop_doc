Fecshop Session
===============

> Fecshop 各个入口的Session的设置以及原理


### 关于Session

1.session 配置

Session是为了记录状态，和前端用户交互的，目前有三个端口，Appfront，Apphtml5，
Appserver三个入口，其中Appfront，Apphtml5是基于`php session`实现，
Appserver是基于`access-token`

### Appfront，Apphtml5 Session设置

这两个入口是基于Php Session，Fecshop使用的是Yii2的Session组件，因此，您设置Yii2 Session组件
的参数即可，您可以在 `@app/config/main.php`中看到`session`组件的配置

```
'session' => [
    /*
     * // use mongodb for session.
     * 'class' => 'yii\mongodb\Session',
     * 'db' => 'mongodb',
     * 'sessionCollection' => 'session',
     */
    'timeout' => 86400 * 7,
    'keyPrefix' => 'appfront_session',
    'redis' => [
        'database' => 5,
    ],
],
```

上面的 `timeout` 参数就可以配置`session`的超时时间

2.user组件的配置

对于用户登录部分，Yii2提供了user组件，支持cookie自动登录，关于cookie自动登录的原理，
您可以参看之前我整理的文章：[Yii2 User cookie 登录原理](http://www.fancyecommerce.com/2017/01/17/yii2-user-%E7%99%BB%E5%BD%95%E5%8E%9F%E7%90%86/)
和 [Yii2 User cookie 登录原理 2](http://www.fancyecommerce.com/2017/01/17/yii2-user-cookie-%E7%99%BB%E5%BD%95%E5%8E%9F%E7%90%86-2/)

设置登录用户是否cookie登录：

在`@fecshop/app/appfront/config/appfront.php` 配置文件里面可以看到user组件的配置

```
        'user' => [
            'class'            => 'fecshop\yii\web\User',
            'identityClass'    => 'fecshop\models\mysqldb\Customer',
            // 是否cookie 登录。
            /*
             * @var boolean whether to enable cookie-based login. Defaults to false.
             * Note that this property will be ignored if [[enableSession]] is false.
             * 设置为true的好处为，当浏览器关掉在打开，可以自动登录。
             */
            'enableAutoLogin'    => true,

            /*
             * authTimeout => 56666,
             * 这里请不要设置authTimeout，为了让customer账户session
             * 和cart的session保持一致，设置超时时间请统一在session组件
             * 中设置超时时间。
             */
            //'authTimeout' 		=> 56666,
        ],
```

设置参数 `enableAutoLogin`为 `true`  即可。

当然，您不能在这里直接修改，您将上面的配置代码复制到 `@app/config/main.php`配置文件中的
`components`配置数组中，通过配置文件优先级的方式覆盖fecshop的默认配置即可。

### Appserver Session配置

严格的说，Appserver部分，不能算session，因为是基于`access-token`的，但是为了方便，fecshop将`php session`
和`access-token`进行了封装，您可以无感知的使用session services里面的方法，
因此文件的命名也是用的session名称。


打开文件`@fecshop/config/services/Session.php`

```
//  实现了一个类似session的功能，供appserver端使用
// 【对phpsession 无效】设置session过期时间,
//  对于 appfront  apphtml5部分的session的设置，您需要到 @app/config/main.php 中设置 session 组件 的timeout时间
'timeout' => 3600,
// 【对phpsession 无效】更新access_token_created_at值的阈值
// 当满足条件：`access_token_created_at`（token创建时间）+ `timeout(过期时间)` <= `time`（当前时间） + updateTimeLimit (更新access_token_created_at值的阈值)
// 则会将用户在数据库表中的  `access_token_created_at` 的值设置成当前时间，这样可以在access_token快要过期的时候，更新 `access_token_created_at`,
// 同时避免了每次访问都更新 `access_token_created_at` 的开销。
'updateTimeLimit' => 600,

```

上面两个参数是对`过期时间`的配置，以及如何更新`access_token_created_at`（token创建时间），下面是关于这个配置部分
的相应代码实现, 参看文件：@fecshop/services/Customer.php

```
    /** AppServer 部分使用的函数
     * @property $type | null or  Object
     * 从request headers中获取access-token，然后执行登录
     * 如果登录成功，然后验证时间是否过期
     * 如果不过期，则返回identity
     * ** 该方法为appserver用户通过access-token验证需要执行的函数。
     */
    protected function actionLoginByAccessToken($type = null){
        $header = Yii::$app->request->getHeaders();
        if(isset($header['access-token']) && $header['access-token']){
            $accessToken = $header['access-token'];
        }
        if($accessToken){
            $identity = Yii::$app->user->loginByAccessToken($accessToken, $type);
            if ($identity !== null) {
                $access_token_created_at = $identity->access_token_created_at;
                $timeout = Yii::$service->session->timeout;
                // 如果时间没有过期，则返回identity
                if($access_token_created_at + $timeout > time()){
                    //如果时间没有过期，但是快要过期了，在过$updateTimeLimit段时间就要过期，那么更新access_token_created_at。
                    $updateTimeLimit = Yii::$service->session->updateTimeLimit;
                    if($access_token_created_at + $timeout <= (time() + $updateTimeLimit )){
                        $identity->access_token_created_at = time();
                        $identity->save();
                    }
                    
                    return $identity;
                }else{
                    $this->logoutByAccessToken();
                    return false;
                }
            }
        }
    }
```

### 总结

对于Appfront，Apphtml5在session实现上都是基于Yii2的Session组件，
对于Appserver，是Fecshop自己封装的，除了上面的一些对过期的参数配置上的不同外（当然还有其他的不同），在使用session的时候都是相同的，
打开session service文件： `@fecshop/service/Session.php` 可以看到`session`的`get()`,`set()`,`remove()`等方法

譬如设置session 

```
Yii::$service->set('SESSION_KEY','my session key')
```

取出来Session的值


```
Yii::$service->get('SESSION_KEY')
```

上面的封装，对三个入口 `Appfront`，`Apphtml5`，`Appserver` 都是透明使用的，
其他的具体的详细，您可以一步一步的参看源码。
















