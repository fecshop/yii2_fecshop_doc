Trace系统配置
===========


首先要确定好ip和域名，譬如我的如下：

1.您的go服务器的地址ip：`120.24.37.249` 

2.您的追踪js和trace访问的域名：`trace.fec.com`  

您需要将下面出现该`ip` 和该`域名`的地方，改成**您自己的ip和域名**


### host映射

在本地win添加host映射，打开文件：C:\Windows\System32\drivers\etc\hosts

```
120.24.37.249  trace.fecshopsoft.com
```

> 注意，ip改成您自己的ip就可以了，域名不要改动




### 下载Trace系统包


下载解压即可


### 配置系统后台和js访问

> 也就是trace系统后台的配置，和trace js的配置



1.文件上传，并配置nginx

1.1打开下载的文件包，将里面的`web文件夹`通过ftp上传到服务器
文件路径：`/www/web/online/trace_fecshop/`下面（没有自行新建）

1.2配置nginx

打开nginx的配置文件，添加配置：


```
server {
    listen     80  ;
    # listen 443 ssl http2;
    #     ssl on;
    #     ssl_certificate /etc/letsencrypt/live/fecshop.appfront.fancyecommerce.com/fullchain.pem;
    #     ssl_certificate_key /etc/letsencrypt/live/fecshop.appfront.fancyecommerce.com/privkey.pem;
    #     ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    server_name trace.fec.com;
    root  /www/web/online/trace_fecshop/web;
    server_tokens off;
    include none.conf;
    index index.php index.html index.htm;
    access_log /www/web_logs/access1.log wwwlogs;
    error_log  /www/web_logs/error.log  notice;
    location ~ .*\.(js|css)?$ {
        expires      12h;
    }
}

```

如果想要可以https访问，自行配置开启

`server_name trace.fec.com;`： 域名改成您自己的域名

这样，您的trace系统的后台访问地址为：`trace.fec.com`

您的trace js的访问地址为  `trace.fec.com/fec_trace.js`

这些配置都是前端部分的配置，通过nginx可以直接访问这些前端资源

访问 trace.fec.com  和  ttrace.fec.com/fec_trace.js ，检测是否可以访问，
如果可以访问，则说明配置成功。

### 后台配置

1.上传文件

1.1将 `services/etc/fec-go/config.ini`, 通过ftp上传到服务器`/etc/fec-go/config.ini`

1.2将 `servers/fec-go` 和 `servers/fec-go-shell` 
上传到服务器`/www/services/`


2.编辑配置文件

在服务器中打开：`/etc/fec-go/config.ini`，编辑里面的内容，配置各个数据库

2.1redis的配置

```
redis_user =
redis_password =
redis_port = 127.0.0.1:2183
```

设置redis的用户，密码，端口等信息，您可以使用默认

2.2mysql的配置

```
# mysql用户名
mysql_user      = root  
# mysql密码
mysql_password  = xxxxxx
# mysql host
mysql_host      = 127.0.0.1
# mysql 端口
mysql_port      = 3306
# mysql 数据库名
mysql_db        = fecshop_trace
charset         = utf8
autocommit      = true
# mysql 连接池的设置
maxOpenConns    = 10
# mysql 连接池的设置
maxIdleConns    = 10
```

上面的配置，您配置一下用户名和密码即可


2.3mongodb的配置

```
#mongodb
mgo_ip              = 127.0.0.1
mgo_port            = 27017
mgo_databaseName    = fecshop_trace
mgo_maxPoolSize     = 200
mgo_poolLimit       = 200
```

使用默认即可


2.4log的配置

```
//release,debug,test
#log_mode = release
output_log = false
router_info_log = /www/web_logs/fec-go/router_info.log
router_error_log = /www/web_logs/fec-go/router_error.log
global_log = /www/web_logs/fec-go/global.log 


#shell 日志

shell_output_log = false
shell_router_info_log = /www/web_logs/fec-go-shell/router_info.log
shell_router_error_log = /www/web_logs/fec-go-shell/router_error.log
shell_global_log = /www/web_logs/fec-go-shell/global.log 

```

如果您开启log，则需要新建相应的文件


2.5新建上传文件路径

```
saveUploadFileDir = /www/test/xlsx
```

您新建这个文件路径即可

```
mkdir -p  /www/test/xlsx
```


2.6.用户信息


```
userName = terry
userEmail = 2358269014@qq.com
userTelephone = 18620432962
userToken = tyFDDFA3242sdF322
userUrl = http://120.24.37.249:3001/verify
```

如果您使用付费版，需要远程授权，这些信息购买后会给予

如果使用免费版,不需要进行任何设置

2.7设置golang服务监听的ip和端口

```
#http服务监听的端口
httpHost = 0.0.0.0:3000
```

将`0.0.0.0`改成您的ip即可，也可以不更改，譬如阿里云
的网络设置，需要使用 `0.0.0.0`


这样就设置完了

### 导入数据库

进入mysql，新建数据库`fecshop_trace`

然后将数据库文件  ./services/fec-go.sql 上传到服务器，然后导入到
mysql数据库`fecshop_trace`中


### 开启go服务


1.设置开启数据接收和访问服务


服务器进入文件夹  `cd /www/services/`

执行  `./fec-go` 开启服务

您的golang服务就是 `120.24.37.249:3000`

打开文件：/www/web/online/trace_fecshop/web/fec_trace.js，将
第二行的`120.24.37.249`改成您自己的ip即可。


2.添加网站

访问前面配置好的  `trace.fec.com`，通过`admin  admin123 `
即可进入,进入后，您更改成自己的密码即可

相应的操作参看：

[trace 后台账户介绍](trace-fecshop-account.md)

[trace 如何添加网站](trace-fecshop-config.md)

注意，免费版本只能添加一个网站，不要添加多个，如果添加多个，将会导致无法进行
数据统计。

通过上面的文档，您可以网站信息，然后将网站信息添加fecshop中，详细参看文档：
[Fecshop和Trace系统对接](trace-fecshop-connect.md)

对接完成后，fecshop访问后，trace系统就会接收到数据，具体数据您可以
进入mongodb查看

3.归并统计

当有数据进入到trace系统，您就可以进行数据归并统计科

执行 `./fec-go-shell` 进行数据归并统计。

执行完，您就可以在trace系统中查看统计后的数据

这个脚本一天执行一次即可，可以添加到cron中执行

如果您想执行最近7天的统计数据，可以执行`./fec-go-shell 7` 

您可以设置cron，`crontab -e` 

```
###进入crontab后，加入下面的配置，下面代表每天的9点执行统计
0 09 * * *  /www/services/fec-go-shell

### 这个是更新缓存信息，每分钟运行
* * * * * /usr/bin/wget http://120.24.37.249:3000/fec/trace/cronssss /dev/null 

```

这样，整个配置就完成了。 

















