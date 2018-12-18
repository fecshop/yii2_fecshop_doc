Fecshop 安全问题
===============


Fecshop已经在安全方面做了很多的工作，对于sql注入，xss，csrf等都进行了防御，
关于csrf的文章可以参看：http://www.fecshop.com/topic/1545

### 1.查看端口开放：

```
netstat -tln
```

譬如我的检测为：

```
[root@ip-172-31-30-214 ~]# netstat -tln
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address               Foreign Address             State      
tcp        0      0 127.0.0.1:9000              0.0.0.0:*                   LISTEN      
tcp        0      0 0.0.0.0:25672               0.0.0.0:*                   LISTEN      
tcp        0      0 127.0.0.1:27017             0.0.0.0:*                   LISTEN      
tcp        0      0 172.31.30.214:3690          0.0.0.0:*                   LISTEN      
tcp        0      0 127.0.0.1:6379              0.0.0.0:*                   LISTEN      
tcp        0      0 0.0.0.0:80                  0.0.0.0:*                   LISTEN      
tcp        0      0 0.0.0.0:4369                0.0.0.0:*                   LISTEN      
tcp        0      0 0.0.0.0:22                  0.0.0.0:*                   LISTEN      
tcp        0      0 0.0.0.0:15672               0.0.0.0:*                   LISTEN      
tcp        0      0 127.0.0.1:25                0.0.0.0:*                   LISTEN      
tcp        0      0 :::5672                     :::*                        LISTEN      
tcp        0      0 :::3306                     :::*                        LISTEN      
tcp        0      0 :::4369                     :::*                        LISTEN      
tcp        0      0 :::22                       :::*                        LISTEN      
tcp        0      0 ::1:25                      :::*                        LISTEN      

```

对于外网ip开放（也就是172.31.30.214）的端口要注意安全，密码一定要很长
提高安全性，
对于mongodb（默认端口27017）和redis（默认端口6379）绑定的ip为内网127.0.0.1，
如果开放端口为外网IP，那么，mongodb和redis必须设置密码，否则将会被入侵。


### 2.mongodb的安全设置

mongodb的安装可以参考：http://www.fancyecommerce.com/2016/05/03/yii2-mongodb%E7%9A%84%E5%AE%89%E8%A3%85%E5%92%8C%E9%85%8D%E7%BD%AE-mongo/


#### 1.1 设置端口和ip

安全ip连接设置：vim /etc/mongod.conf

```
net:
  port: 27017
  bindIp: 127.0.0.1
```

port代表开放的访问端口，bindIp这个是一个安全ip配置，允许那些ip连接mongodb，如果设置成bind_ip = 0.0.0.0，代表任意ip，建议只写连接的ip，如果是本机，就填写127.0.0.1即可。

这个是一个安全设置，线上系统一定要注意，iptables设置，只允许部分ip访问该端口，其他的ip不允许访问该port，而且mongodb也要设置允许的ip。

#### 2.2 mongodb账号密码

另外，对于线上系统，最好是使用账号密码的方式连接，进一步增强安全性。
这个您自行查阅资料，现在还没有写相关文章。


### 3.Yii给予的安全防范

[最佳安全实践](http://www.yiichina.com/doc/guide/2.0/security-best-practices)

3.1 域名指向@app/web目录，这样可以防止暴露其他文件

3.2 将develop（开发）模式改成product（生产）模式

打开 @app/web/index.php(@app代表  @appfront  @apphtml5 等入口)

将代码：

```
defined('YII_DEBUG') or define('YII_DEBUG', true);
defined('YII_ENV') or define('YII_ENV', 'dev');
```

改成

```
defined('YII_DEBUG') or define('YII_DEBUG', false);
defined('YII_ENV') or define('YII_ENV', 'prod');
```

打开后，线上环境的错误信息不回直接报出，只会给予一个错误编号，譬如：

```
{"code":500,"error_no":"5a3b0e4d3e00ca3c3f3aaf52"}
```

然后可以在后台查看具体的报错信息，详细参看：
[Fecshop Error Handler ](fecshop_error_handler.md)

这样，用户如果有错误，直接把错误编号发过来，开发人员就可以查到相应的错误，
另外，开发人员可以自己去查看后台的ErrorHandle，处理没有发现的错误问题。

3.3 安全加密访问(HTTPS) 

现在firefox，chrome，都把http连接默认设置为不安全的连接，
因为是明码传输，而对于https是加密传输，会更安全一些，
https的安装和使用可以参看文章：

[centos 下安装 Let’s Encrypt 永久免费 SSL 证书](http://www.fancyecommerce.com/2017/04/07/centos-%e4%b8%8b%e5%ae%89%e8%a3%85-lets-encrypt-%e6%b0%b8%e4%b9%85%e5%85%8d%e8%b4%b9-ssl-%e8%af%81%e4%b9%a6/)


3.4 xss攻击

对于xss 攻击，fecshop默认都已经过滤掉，如果您开发了新功能，一定要注意
处理。

### 4.后台地址隐藏

> 这个是很重要的一个部分，当你的网站有一定的访问量，一定要把后台登录地址隐藏起来。

fecshop的后台是使用独立的域名，您解析到您的主机，通过ip反向检测是可以查出来的，
这样就暴露了你的登录地址，后台没有验证码，可能会被黑客使用工具暴力破解出来
你的主机的后台密码，因此后台的地址要隐藏掉，你可以有下面的几种方法


4.1、这种是比较简单的，也就是你使用本地host映射一个假的域名，譬如你的域名是fecshopexample.com,
已经备案，然后，你可以用一个 子域名：   jk23jr2lkr2l3rk23ljdflk32l.fecshopexample.com
,这个子域名不要做解析，你在nginx配置好，然后在本地windows host中做域名ip映射即可。

这样只有在win host加了映射才能访问，别人无法访问，这样别人访问不了你的地址

4.2、使用vpn的方式，使用内网访问，这种安全性会更高，不过也复杂

肯定还有其他很多的方式隐藏掉后台访问路径，各自有各自的方法，
第一种方式比较方便简单，您在项目初期可以使用第一种方式隐藏后台登录地址


4.3、后台密码，一定要尽量的长一些

### 5.其他密码

对于mysql linux密码等要设置的比较长，防止安全破解,另外设置ip访问权限，
只有设置的ip才能访问。

### 6.cron定时脚本

对于console的脚本知识，你可以参看：[Fecshop console 介绍和配置](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-console-about.html)

对于周期性在cron中执行的脚本，要输出log日志，这样可以在出问题的时候查看log。

### 7. 其他安全问题

等想到了其他的安全问题，会继续添加注意防范的地方

如果您有自己对安全的一些见解，可以联系我，qq：2358269014
