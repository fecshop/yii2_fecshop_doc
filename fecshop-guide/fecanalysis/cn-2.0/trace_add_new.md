Trace系统添加新平台
===================


1.接收js和api地址会改变，那么对应的需要修改

1.1、添加一个新的追踪js地址

js里面的内容也需要需要修改，将trace.js尾部的

```
img.src = '//120.24.37.249:3000/fec/trace?' + args;
```

改成当前的接收地址


1.2、handler/common/website.go文件里面修改：

```
var FecTraceJsUrl string = "trace.fecshop.com/fec_trace.js"
var FecTraceApiUrl string = "120.24.37.249:3000/fec/trace/api"
```

`FecTraceJsUrl`: 上面新建的js地址

`FecTraceApiUrl`: 相应的api地址，用于接收服务端传送的数据。

1.3、搭建go环境，安装mongodb，mysql

1.4、让新用户在这里注册，对接。

1.5、配置文件 `/etc/fec-go/config.ini` 中的数据库连接等

1.6、website更新部分，http://120.24.37.249:3000/fec/trace/cronssss

通过cron访问该链接，五分钟间隔一次，更新website信息。

1.7、启动数据接收功能： `go run fec-go.go` 

1.8、通过cron，在9点左右启动脚本计算，启动计算统计功能： `go run fec-go-shell.go`


















