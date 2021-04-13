Fecmall-安装应用-超时问题
===========

> 通过fecmall后台，在线安装应用，出现超时问题的处理


### Fecmall Nginx 安装应用超时问题


因为php，nginx，都有默认的超时设置，一旦超过超时时间，就会中断下载，
fecmall的有的应用比较大，譬如fecwbbc 8mb+，如果服务器是国外服务器（fecmall应用下载是国内阿里云下载节点）
，可能会出现安装扩展超时问题，报错：nginx 502 Bad Gateway


您需要从配置一下php和nginx的参数


1.配置php的超时参数


1.1php配置文件

```
max_execution_time = 600  

```

将最大执行时间设置600s（10分钟）



1.2php-fpm配置文件（FPM配置文件），更改配置：


```
request_terminate_timeout = 0
```

2.配置nginx的超时时间


```
keepalive_timeout 600;


```

3.重启nginx和php，然后重新安装试试，安装扩展一定记得先备份sql





