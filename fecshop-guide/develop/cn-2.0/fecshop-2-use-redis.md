Fecmall-使用redis
============

> Fecmall默认是不需要redis的，您可以通过配置，使用redis

### 使用redis

Redis用于`Cache`， `Session`，`验证码部分`


1.安装redis

2.添加redis配置

打开文件：`@common/config/main-local.php`

 
```
/**
 * 默认的cache和session配置。
 */
'cache' => [
    'class' => 'yii\caching\FileCache',  // 默认为文件存储cache
    // 缓存配置独立的redis，您可以和上面的redis配置一致
],

'session' => [
    'class'   => 'yii\web\Session',
    // session过期时间，1天过期
    'timeout' => 86400 * 1, 
],

'redis' => [
    'class' => 'yii\redis\Connection',
],
/** 
 * 如果你想使用redis sesson 和 redis cache，那么使用下面的配置
 * 1.设置redis组件的配置
 * 2.将上面cache和session组件配置部分注释掉，使用下面的cache 和 session组件
 * 3.
'redis' => [
    'class' => 'yii\redis\Connection',
    'hostname' => '127.0.0.1',    // redis的host
    'port' => 6379,               // redis的端口     
    'password'  => 'dfa@#dsfaer99912EDFqa', // redis的密码
    'database' => 0,    // redis的库，此处不要改动
],

'cache' => [
    'class'     => 'yii\redis\Cache',  // 'class' => 'yii\caching\FileCache',
    // 缓存配置独立的redis，如何和redis 组件一致，则不需要单独配置。
    //'redis' => [
    //    'hostname' => '127.0.0.1',   // redis的host
    //    'port' => 6379,              // redis的端口   
    //    'password'  => 'dfa@#dsfaerfw666r12EDFqa', // redis的密码
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
    //    'password'  => 'dfa@#dsfae666r12EDFqa', // redis的密码
    //],
],
*/
```

将上面未注释的代码部分注释掉，将注释的代码的注释去掉

然后配置即可.


3.各个入口设置`keyPrefix`

使用redis session后，对应的class为` 'yii\redis\Session'`,
您需要为每个app入口设置`keyPrefix`，
打开@app/config/main.php文件，将下面的注释去掉  （@app指的是@appfront, @apphtml5 @appadmin 入口）

```
 'session' => [
    //'keyPrefix' => 'appfront_session',  如果您使用redis session，您需要去掉注释
],
```

有的童鞋会认为这个不设置也是可以的,查看：`yii\redis\Session`

```
if ($this->keyPrefix === null) {
    $this->keyPrefix = substr(md5(Yii::$app->id), 0, 5);
}
```

我认为设置一下比较稳妥，比较好维护一点,通过前缀`keyPrefix`直接知道这个session是那个app入口的的：























