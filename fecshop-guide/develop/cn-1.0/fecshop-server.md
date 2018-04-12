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



### 2.获取登录 access-token

用户登录，访问的是` @fecshop/app/appserver/modules/Customer/controllers/LoginController.php`
的 `actionAccount()` Action方法，查看这个方法里面的代码，你可以看到代码行
：`$identity = Yii::$service->customer->loginByAccessToken(get_class($this));`

我们打开这个方法`@fecshop/services/Customer.php`文件的`loginByAccessToken`方法
,代码如下：

```
protected function actionLoginAndGetAccessToken($email,$password){
        $header = Yii::$app->request->getHeaders();
        if(isset($header['access-token']) && $header['access-token']){
            $accessToken = $header['access-token'];
        }   
        // 如果request header中有access-token，则查看这个 access-token 是否有效
        if($accessToken){
            $identity = Yii::$app->user->loginByAccessToken($accessToken);
            if ($identity !== null) {
                $access_token_created_at = $identity->access_token_created_at;
                $timeout = Yii::$service->session->timeout;
                if($access_token_created_at + $timeout > time()){
                    return $accessToken;
                } 
            }
        }
        // 如果上面access-token不存在
        $data = [
            'email'     => $email,
            'password'  => $password,
        ];
        
        if(Yii::$service->customer->login($data)){
            $identity = Yii::$app->user->identity;
            $identity->generateAccessToken();
            $identity->access_token_created_at = time();
            $identity->save();
            # 执行购物车合并等操作。
            Yii::$service->cart->mergeCartAfterUserLogin();
            $this->setHeaderAccessToken($identity->access_token);
            return $identity->access_token;
            
        }
    }
```

首先从 request header取`access-token`，如果取出来，则直接使用该`access-token`，如果有效，直接返回该`access-token`

如果request header不存在`access-token`，或者`access-token`过期，则进行登录，登录成功后，你会看到代码
`$this->setHeaderAccessToken($identity->access_token);`, 这个函数是将登录成功后
生成的access-token这是到response header中，我们查看这个方法：

```
protected function actionSetHeaderAccessToken($accessToken){
    if($accessToken){
        Yii::$app->response->getHeaders()->set('access-token',$accessToken);
        return true;
    }
}

```

将生成的access-token设置到response headers中。完成

### 登录用户访问 access-token 验证

如果用户登录后，每次访问都会在request headers中含有`access-token`（vue端的ajax需要
在请求的header中带上`access-token`），appserver根据该值进行验证，
验证合法性通过后，就会登录，实现原理如下：

对于需要验证用户登录状态的api，都继承@fecshop/app/appserver/modules/AppserverTokenController.php，
在`behaviors()` 里面可以看到：（关于Yii2的behaviors，参看[Yii2行为](http://www.yiichina.com/doc/guide/2.0/concept-behaviors)）


```
use fecshop\yii\filters\auth\QueryParamAuth; 

...

        $behaviors['authenticator'] = [  
            'class' => CompositeAuth::className(),  
            'authMethods' => [  
                # 下面是三种验证access_token方式  
                //HttpBasicAuth::className(),  
                //HttpBearerAuth::className(),  
                # 这是GET参数验证的方式  
                # http://10.10.10.252:600/user/index/index?access-token=xxxxxxxxxxxxxxxxxxxx  
                QueryParamAuth::className(),  
            ],  
          
        ];  
```

上面的代码部分，是Yii2的行为原理，每次执行都会执行里面的代码，打开：`@fecshop\yii\filters\auth\QueryParamAuth.php`

```
    /**
     * 重写该方法。该方法从request header中读取access-token。
     */
    public function authenticate($user, $request, $response)
    {   
        $identity = Yii::$service->customer->loginByAccessToken(get_class($this));
        if($identity){
            return $identity;
        }else{
            $fecshop_uuid = Yii::$service->session->fecshop_uuid;
            $cors_allow_headers = [$fecshop_uuid,'fecshop-lang','fecshop-currency','access-token'];
            
            header('Access-Control-Allow-Origin: *');
            header("Access-Control-Allow-Headers: Origin, X-Requested-With, Content-Type, Accept, ".implode(', ',$cors_allow_headers));
            header('Access-Control-Allow-Methods: GET, POST, PUT,DELETE');
            $code = Yii::$service->helper->appserver->account_no_login_or_login_token_timeout;
            $result = [ 'code' => $code,'message' => 'token is time out'];
            Yii::$app->response->data = $result;
            Yii::$app->response->send();
            Yii::$app->end();
            
            
        }
    }
    
```

从request header里面取出来access-token，登录的代码：`$identity = Yii::$service->customer->loginByAccessToken(get_class($this));`

后面的就不一一叙述了，您自己看把。



### 4.登录用户的 速度控制 和 过期时间  

4.1速度控制

4.1.1、在 `@fecshop/app/appserver/config/appserver.php` 里面设置

```
        'rateLimit'             => [
            'enable'=> false,   # 是否开启？默认不开启速度控制。
            'limit' => [120, 60],
        ]
```

> @fecshop 指的是 vendor/fancyecommerce/fecshop 文件夹, 关于 @符号，在安装配置fecshop文档部分已经介绍

同样，你无权修改vendor下的文件，您可以在@appserver/config/params.php中添加如下配置，进行修改。

```
'params'  => [
        // 速度控制[120,60] 代表  60秒内最大访问120次，
        'rateLimit'             => [
            'enable'=> false,   # 是否开启？默认不开启速度控制。
            'limit' => [120, 60],
        ]
    ],
```

4.1.2、将User组件的`identityClass`设置成相应的model

@appserver/config/main.php

找到user组件配置的部分,更改成如下：

```
'user' => [
    // 'class'            => 'fecshop\yii\web\User',
    // 【默认】不开启速度限制的 User Model
    // 'identityClass'     => 'fecshop\models\mysqldb\Customer',
    // 开启速度限制的 User Model
    'identityClass'     => 'fecshop\models\mysqldb\customer\CustomerAccessToken',
    
],
```

更改完后，appserver端，api速度限制就开启了。


4.2过期时间

打开文件`@fecshop/config/services/Session.php`

```
//  实现了一个类似session的功能，供appserver端使用
// 【对phpsession 无效】设置session过期时间,
//  对于 appfront  apphtml5部分的session的设置，您需要到 @app/config/main.php 中设置 session 组件 的timeout时间
'timeout' => 3600,
// 【对phpsession 无效】更新access_token_created_at值的阈值
// 当满足条件：`access_token_created_at`（token创建时间）`timeout(过期时间)` <= `time`（当前时间） < updateTimeLimit (更新access_token_created_at值的阈值)
// 则会将用户在数据库表中的  `access_token_created_at` 的值设置成当前时间，这样可以在access_token快要过期的时候，更新 `access_token_created_at`,
// 同时避免了每次访问都更新 `access_token_created_at` 的开销。
'updateTimeLimit' => 600,

```

对于设置超时时间的2个参数，上面的注释已经说清楚，
您可以在 @appserver/config/fecshop_local_services/Session.php 里面添加配置（没有这个文件自行创建），内容如下：

```
return [
    'session' => [
        // 【下面的三个参数，在使用php session的时候无效】
        //  只有 \Yii::$app->user->enableSession == false的时候才有效。
        //  说的更明确点就是：这些参数的设置是给无状态api使用的。
        //  实现了一个类似session的功能，供appserver端使用
        // 【对phpsession 无效】设置session过期时间,
        //  对于 appfront  apphtml5部分的session的设置，您需要到 @app/config/main.php 中设置 session 组件 的timeout时间
        'timeout' => 3600,
        // 【对phpsession 无效】更新access_token_created_at值的阈值
        // 当满足条件：`access_token_created_at`（token创建时间）`timeout(过期时间)` <= `time`（当前时间） < updateTimeLimit (更新access_token_created_at值的阈值)
        // 则会将用户在数据库表中的  `access_token_created_at` 的值设置成当前时间，这样可以在access_token快要过期的时候，更新 `access_token_created_at`,
        // 同时避免了每次访问都更新 `access_token_created_at` 的开销。
        'updateTimeLimit' => 600,
    ],
];

```

修改配置即可。

对于Fecshop 的Session更详细的知识，可以参看文档 [Fecshop Session](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_session.html)





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









