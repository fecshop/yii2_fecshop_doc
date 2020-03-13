Fecmall验证码
============

> 在注册账户，登录，找回密码等表单提交的地方需要验证码，
> 您可以通过配置的方式决定是否开启验证码。


### fecmall验证码设置


验证码的开启在`后台`各个部分进行配置，

### 二开功能加入验证码

如果您想在自己的一些功能中加入验证码可以使用（appfront和apphtml5端）

1.显示验证码图片,以及填写验证码的input框，刷新验证码的图标等

```
<div class="field">
    <label for="captcha" class="required"><em>*</em><?= Yii::$service->page->translate->__('Captcha'); ?></label>
    <div class="input-box register-captcha">
        <input type="text" name="editForm[captcha]" value="" size=10 class="login-captcha-input"> 
        <img class="login-captcha-img"  title="click refresh" src="<?= Yii::$service->url->getUrl('site/helper/captcha'); ?>?<?php echo md5(time() . mt_rand(1,10000));?>" align="absbottom" onclick="this.src='<?= Yii::$service->url->getUrl('site/helper/captcha'); ?>?'+Math.random();"></img>
        <i class="refresh-icon"></i>
    </div>
    <script>
    <?php $this->beginBlock('register_captcha_onclick_refulsh') ?>  
    $(document).ready(function(){
        $(".refresh-icon").click(function(){
            $(this).parent().find("img").click();
        });
    });
    <?php $this->endBlock(); ?>  
    </script>  
    <?php $this->registerJs($this->blocks['register_captcha_onclick_refulsh'],\yii\web\View::POS_END);//将编写的js代码注册到页面底部 ?>
</div>
```

2.前端提交的验证码，服务端接收后，需要验证：

```
Yii::$service->helper->captcha->validateCaptcha($captcha)
```


### Appserver入口的验证码 - 原理解析

1.fecmall-2版本，默认不需要安装redis，session默认存储在磁盘文件里面

2.对于微信小程序，vue等部分，是基于api的应用，对于api的应用类型，是没有session机制的，
因此需要实现一个类似于session的功能，fecmall的appserver使用redis来实现的，原理如下：

2.1用户第一次访问vue入口，vue调用fecmall appserver的api进行数据获取,进行数据请求

2.2fecmall appserver接收到请求后，会检测`request header`里面是否存在 `fecshop-uuid`,如果不存在，系统会生成一个`fecshop-uuid`，然后再`Reponse header`中返回`fecshop-uuid`的值

2.3vue接收到api的返回数据，从`Reponse header`中获取`fecshop-uuid`的值，保存到本地

2.4vue下一次请求fecmall的时候，会从本地读取`fecshop-uuid`的值，   ajax请求的`request header`里面中加入 `fecshop-uuid`

2.5因此，`fecshop-uuid`就作为用户的唯一标识，验证码也是通过此标识，对应存储到redis中。

3.代码分析

3.1vue部分的代码是在src/main.js中

```

Vue.prototype.saveReponseHeader = function (response){
     //fecshop-uuid
    var fecshop_uuid = response.getResponseHeader('fecshop-uuid');
    if(fecshop_uuid){
        var local_fecshop_uuid = window.localStorage.getItem("fecshop-uuid");
        if(local_fecshop_uuid != fecshop_uuid){
            window.localStorage.setItem("fecshop-uuid",fecshop_uuid);
            console.log('save header [fecshop-uuid] ######' + fecshop_uuid);
       }
    }
    //access-token
    var access_token = response.getResponseHeader('access-token');
    if(access_token){
        console.log('save header [access-token1]' );
        var local_access_token = window.localStorage.getItem("access-token");
        console.log('save header [access-token2]' );
        if(local_access_token != access_token){
            console.log('save header [access-token3] ######' + access_token);
            window.localStorage.setItem("access-token",access_token);
            
        }
    }
    // lang
    var fecshop_lang = response.getResponseHeader('fecshop-lang');
    if(fecshop_lang){
        var local_fecshop_lang = window.localStorage.getItem("fecshop-lang");
        if(local_fecshop_lang != fecshop_lang){
            window.localStorage.setItem("fecshop-lang",fecshop_lang);
            console.log('save header [fecshop-lang] ######' + fecshop_lang);
        }
    }
    // currency
    var fecshop_currency = response.getResponseHeader('fecshop-currency');
    if(fecshop_currency){
        var local_fecshop_currency = window.localStorage.getItem("fecshop-currency");
        if(local_fecshop_currency != fecshop_currency){
            window.localStorage.setItem("fecshop-currency",fecshop_currency);
            console.log('save header [fecshop-currency] ######' + fecshop_currency);
        }
    }
}
```

```

Vue.prototype.getRequestHeader = function (){
    var headers = {};
    var fecshop_uuid = window.localStorage.getItem("fecshop-uuid");
    if(fecshop_uuid){
        console.log('fecshop uuid ######' + fecshop_uuid);
        headers['fecshop-uuid'] = fecshop_uuid;
    }
    
    var fecshop_lang = window.localStorage.getItem("fecshop-lang");
    if(fecshop_lang){
        console.log('fecshop lang ######' + fecshop_lang);
        headers['fecshop-lang'] = fecshop_lang;
    }
    var fecshop_currency = window.localStorage.getItem("fecshop-currency");
    if(fecshop_currency){
        console.log('fecshop currency ######' + fecshop_currency);
        headers['fecshop-currency'] = fecshop_currency;
    }
    var access_token = window.localStorage.getItem("access-token");
    if(access_token){
        console.log('fecshop access-token ######' + access_token);
        headers['access-token'] = access_token;
    }
    return headers;
    //console.log('get header ####');
}

```

通过这2个函数，进行请求的时候将 `fecshop-uuid` 写入`request header`，以及， `reponse header`中接收 `fecshop-uuid` ，保存到本地


3.2fecmall部分代码解析


3.2.1文件：`@fecshop/services/session/SessionRedis`可以看到代码：


```
public function getSessionKey($key)
    {
        $uuid = Yii::$service->session->getUUID();
        return $uuid.'###^^###'.$key;
    }
```


3.2.2文件：`@fecshop/services/Session`

```
public function getUUID()
    {
        if (!$this->_uuid) {
            $header = Yii::$app->request->getHeaders();
            $uuidName = $this->fecshop_uuid;
            // 1.从requestheader里面获取uuid，
            if (isset($header[$uuidName]) && !empty($header[$uuidName])) {
                $this->_uuid = $header[$uuidName];
            } else { // 2.如果获取不到uuid，就生成uuid
                $uuid1 = Uuid::uuid1();
                $this->_uuid = $uuid1->toString();
            }
            // 3.把 $this->_uuid 写入到 response 的header里面
            Yii::$app->response->getHeaders()->set($uuidName, $this->_uuid);
        }
        return $this->_uuid;
    }
```

可以看到，先从`request header`里面读取，如果读取不到，就生成uuid，并写入`response header`中。






### appserver 验证码 - 实现


了解了上面的原理，我们来实现appserver的验证码功能

1.安装redis，并且启动


2.文件`@common/config/main-local.php` 中，可以看到
`cache`, `session`, `redis`的配置
，以及在下面会看到一个注释掉的配置,如下代码块

```
/** 
         * 如果你想使用redis sesson 和 redis cache，那么使用下面的配置
         * 1.设置redis组件的配置
         * 2.将上面cache和session组件配置部分注释掉，使用下面的cache 和 session组件
         * 3.
		'redis' => [
            'class' => 'yii\redis\Connection',
            'hostname' => '127.0.0.1',    // redis的host
            'port' => 6379,               // redis的端口     
			'password'  => 'dfa@#dsfaerfwFqa', // redis的密码
            'database' => 0,    // redis的库，此处不要改动
        ],
        
        'cache' => [
            'class'     => 'yii\redis\Cache',  // 'class' => 'yii\caching\FileCache',
            // 缓存配置独立的redis，如何和redis 组件一致，则不需要单独配置。
            //'redis' => [
            //    'hostname' => '127.0.0.1',   // redis的host
            //    'port' => 6379,              // redis的端口   
            //    'password'  => 'dfa@#dsfaerfwFqa', // redis的密码
            //],
        ],
        
        
        'session' => [
            'class'   => 'yii\redis\Session',
            // session过期时间，1天过期
            'timeout' => 86400 * 1, 
            // 缓存配置独立的redis，如何和redis 组件一致，则不需要单独配置。
            //'redis' => [
            //    'hostname' => '127.0.0.1', // redis的host
            //    'port' => 6379,            // redis的端口   
            //    'password'  => 'dfa@#dsfaerfwFqa', // redis的密码
            //],
        ],
        */
```


将原来的`cache`, `session`, `redis`的配置注释，将这段注释掉的配置`去掉注释`，然后配置`redis`的连接参数

3.vue部分的配置，打开`src/main.js`
, 找到函数
`Vue.prototype.saveReponseHeader`   和 `Vue.prototype.getRequestHeader `，将这个函数进行更改，使用下面的代码块覆盖原来的这2个函数（就是将注释的fecshop_uuid部分，去掉注释）

```

Vue.prototype.saveReponseHeader = function (response){
     //fecshop-uuid
    var fecshop_uuid = response.getResponseHeader('fecshop-uuid');
    if(fecshop_uuid){
        var local_fecshop_uuid = window.localStorage.getItem("fecshop-uuid");
        if(local_fecshop_uuid != fecshop_uuid){
            window.localStorage.setItem("fecshop-uuid",fecshop_uuid);
            console.log('save header [fecshop-uuid] ######' + fecshop_uuid);
       }
    }
    //access-token
    var access_token = response.getResponseHeader('access-token');
    if(access_token){
        console.log('save header [access-token1]' );
        var local_access_token = window.localStorage.getItem("access-token");
        console.log('save header [access-token2]' );
        if(local_access_token != access_token){
            console.log('save header [access-token3] ######' + access_token);
            window.localStorage.setItem("access-token",access_token);
            
        }
    }
    // lang
    var fecshop_lang = response.getResponseHeader('fecshop-lang');
    if(fecshop_lang){
        var local_fecshop_lang = window.localStorage.getItem("fecshop-lang");
        if(local_fecshop_lang != fecshop_lang){
            window.localStorage.setItem("fecshop-lang",fecshop_lang);
            console.log('save header [fecshop-lang] ######' + fecshop_lang);
        }
    }
    // currency
    var fecshop_currency = response.getResponseHeader('fecshop-currency');
    if(fecshop_currency){
        var local_fecshop_currency = window.localStorage.getItem("fecshop-currency");
        if(local_fecshop_currency != fecshop_currency){
            window.localStorage.setItem("fecshop-currency",fecshop_currency);
            console.log('save header [fecshop-currency] ######' + fecshop_currency);
        }
    }
}



Vue.prototype.getRequestHeader = function (){
    var headers = {};
    var fecshop_uuid = window.localStorage.getItem("fecshop-uuid");
    if(fecshop_uuid){
        console.log('fecshop uuid ######' + fecshop_uuid);
        headers['fecshop-uuid'] = fecshop_uuid;
    }
    
    var fecshop_lang = window.localStorage.getItem("fecshop-lang");
    if(fecshop_lang){
        console.log('fecshop lang ######' + fecshop_lang);
        headers['fecshop-lang'] = fecshop_lang;
    }
    var fecshop_currency = window.localStorage.getItem("fecshop-currency");
    if(fecshop_currency){
        console.log('fecshop currency ######' + fecshop_currency);
        headers['fecshop-currency'] = fecshop_currency;
    }
    var access_token = window.localStorage.getItem("access-token");
    if(access_token){
        console.log('fecshop access-token ######' + access_token);
        headers['access-token'] = access_token;
    }
    return headers;
    //console.log('get header ####');
}
```

然后重新编译VUE。





4.然后就可以访问了。


注册的时候，可能发现时间比较长，这是因为注册账户发送邮件的原因（如果是可用的smtp就不会慢了）。
























