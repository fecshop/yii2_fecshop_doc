Fecshop 安全问题
===============

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

3.2 在生产环境关闭调试信息，打开 @app/web/index.php(@app代表  @appfront  @apphtml5 等入口)

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

3.3 安全加密访问(HTTPS) 

对于安全https的安装和使用可以参看文章：

[centos 下安装 Let’s Encrypt 永久免费 SSL 证书](http://www.fancyecommerce.com/2017/04/07/centos-%e4%b8%8b%e5%ae%89%e8%a3%85-lets-encrypt-%e6%b0%b8%e4%b9%85%e5%85%8d%e8%b4%b9-ssl-%e8%af%81%e4%b9%a6/)

3.4 xss攻击

对于xss 攻击，fecshop默认都已经过滤掉，如果您开发了新功能，一定要注意
处理。

### 4. 密码设置

4.1 后台

后台密码，一定要尽量的长，后台使用其他域名，尽量把后台访问路径保护起来。

4.2 其他密码

对于mysql linux密码等要设置的比较长，防止安全破解。

### 5. 其他安全问题

等想到了其他的安全问题，会继续添加注意防范的地方

如果您有自己对安全的一些见解，可以联系我，qq：2358269014
