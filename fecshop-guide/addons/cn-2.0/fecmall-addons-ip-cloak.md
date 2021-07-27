Fecmall扩展-Ip屏蔽国家访问扩展
=================

> 用户访问网站，获取用户的Ip，通过Ip得到国家（通过`www.maxmind.com`提供的`Ip`数据库，进行查询），然后`屏蔽`相关国家用户的访问

### Ip屏蔽国家访问扩展

该扩展对Ip的检测以及屏蔽，是在`Yii2`框架初始化之前，`Yii2 Service Application`初始化的时候执行的

通过fecmall event `event_service_application_init`, 添加event，
也就是 `@fecipcloak\event\Fecipcloak`的`addServiceApplicationInit()`方法

加入cookie机制，由于用户每次访问都去查Ip库，会比较耗费资源，因此，当用户第一次访问通过Ip
验证后，就会加入cookie，让用户第二次访问商城的其他页面，则不会继续查Ip库，
当Cookie过期后，就会重新验证Ip，然后重新写入`cookie`


### 安装扩展

1.fecmall应用市场地址：http://addons.fecmall.com/87548438

2.如何应用市场`安装`应用，请参看文档：[Fecmall安装应用](https://www.fecmall.com/doc/fecshop-guide/addons/cn-2.0/guide-fecmall-addons-install.html)

3.Ip数据库下载


Ip库用的`GeoLite2-City`，这个在官网可以下载，您可以去官网下载，官网地址：https://www.maxmind.com/

Q群文件下载`GeoLite2-City_20201215.tar.gz` （QQ群：`782387676`，入群验证：`fecmall`）

为什么插件没有默认集成这个库？因为这个库文件太大了，压缩包30MB+，因此您自己下载即可

下载完成后，文件路径 `./common/lib/GeoLite2-City/GeoLite2-City.mmdb` （需要您自己上传）


4.由于该部分的触发比较靠前，因此，您只能通过配置文件进行设置参数


打开配置文件：`./addons/fecmall/fecipcloak/config.php`


找到配置部分

```
'services' => [
    'ipcloak' => [
        'class' => 'fecipcloak\services\Ipcloak',
        /**
         * 由于ip检测发生在非常靠前的部分，因此，很多yii2的组件不能使用，因此，需要通过配置文件进行配置
         */
        // IpCloak？数据库路径，您需要到fecmall官方群文件里面下载该文件路，然后按照下面的配置放到相应的文件夹中。
        'geoLite2CityMmdb' => '@common/lib/GeoLite2-City/GeoLite2-City.mmdb',
        // 是否开启IpCloak？【默认开启】
        'ipCloakEnable' => true,
        // ip被屏蔽后，进入404页面还是home首页？  您可以填写值   404  or  home
        'ipCloakRedirect' => '404',
        // IpCloak是否开启cookie检测？【默认开启】，当用户没有被ip屏蔽，开启后，将会写入cookie，用户下次访问，直接检查cookie就可以了，不需要通过ip继续查库，节省资源
        'cookieCheckEnable' => true,
        // cookie 过期天数
        'cookieTimeoutDays' => 7,
        // Ip屏蔽的国家简码，多个国家用英文逗号隔开，注意，必须用大写，譬如： ['CN','US','FR']
        'cloakCountryCodes' => ['CN','US','FR'],
        
    ],
],
```

您可以根据这里的注释说明，添加相应的配置


5.然后您就可以测试了。


### 二开扩展


`GeoLite2-City`是支持国家，省，市查询的，如果您屏蔽的维度要求细致，需要精确到城市，那么可以自己进行开发。






