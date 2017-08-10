Fecshop Facebook Google登录
============================

> Facebook Google 登录，指的是用户可以直接使用Facebook Google 账号登录
> fecshop，而不需要注册账户

### 1、配置

在store的配置文件：@app/config/fecshop_local_services/Store.php 
中可以看到，每一个store都可以独立配置相应的facebook
和google登录，配置代码如下：

```
// 第三方账号登录配置
'thirdLogin' => [
    // facebook账号登录
    'facebook' => [       //fb api配置 ，fb可以一个app设置pc和手机web两个域名
        'facebook_app_id'     => '108618299786621',
        'facebook_app_secret' => '420b56da4f4664a4d1065a1d31e5ec73',
    ],
    // google账号登录
    'google' => [       //谷歌api visit https://code.google.com/apis/console to generate your google api
        'CLIENT_ID'      => '380372364773-qdj1seag9bh2n0pgrhcv2r5uoc58ltp3.apps.googleusercontent.com',
        'CLIENT_SECRET'  => 'ei8RaoCDoAlIeh1nHYm0rrwO',
    ],
],
```

上面的app_id 和 secret是google 和facebook授权的，
这些信息，您需要到官方登录得到授权信息。

[facebook login 申请 app_id 和 app_secret](http://www.fecshop.com/topic/164)

[google login api 申请 CLIENT_SECRET 和 CLIENT_SECRET ](http://blog.csdn.net/terry_water/article/details/55095209)

按照上面的文章的步骤设置好，然后将授权信息填写到相应的store中即可。

注意：每一个store都需要填写，除非你不想该store支持Facebook Google 登录




















