FA安装
======

> FA系统，全称Fecshop Analysis系统，属于前后端api对接的方式，前端用的vue，后端是基于golang编写的，数据库有mongodb，redis，mysql，
下面是详细的安装

### golang部分安装

1.库包安装

1.1安装xorm

```
go get github.com/go-sql-driver/mysql
go get github.com/go-xorm/xorm
```

2.安装gin

```
go get github.com/gin-gonic/gin
```

参考资料： [centos6 安装go框架gin的步骤，以及中间遇到的坑](http://www.fancyecommerce.com/2017/12/28/centos6-%e5%ae%89%e8%a3%85go%e6%a1%86%e6%9e%b6gin%e7%9a%84%e6%ad%a5%e9%aa%a4%ef%bc%8c%e4%bb%a5%e5%8f%8a%e4%b8%ad%e9%97%b4%e9%81%87%e5%88%b0%e7%9a%84%e5%9d%91/)

上面如果都安装成功了, 下面安装`fec-go`

```
go get github.com/fecshopsoft/fec-go
```

下载完成后，即可下载玩所有的文件

该部分代码在 ``./github.com/fecshopsoft/fec-go`

### 安装 Mysql, ElasticSearch, Mongodb， Nginx

1.安装`mysql`

1.1安装装文档：[mysql5.6安装](http://www.fancyecommerce.com/2016/04/29/linux-安装mysql5-6/)

1.2创建数据库`fa-go`

1.3导入数据库,mysql数据库文件如下：

```
./github.com/fecshopsoft/fec-go/example/my.sql
```

2.安装`elasticSearch6`

注意，这里是安装es6，可以参看文档[安装ElasticSearch](http://www.fecshop.com/topic/672)

3.安装`mongodb`

> 下面的安装文档安装完第3步就可以了，后面是安装php mongodb扩展的部分，不需要安装

安装参考文档[安装mongodb](http://www.fecshop.com/topic/1158)

4.安装nginx

参考文档：http://www.fancyecommerce.com/2016/05/03/linux-安装nginx/


### 配置

1.创建文件以及文件夹

```
mkdir -p /www/fec-go/etc
touch /www/fec-go/etc/config.ini

mkdir -p /www/fec-go/log
touch /www/fec-go/log/router_info.log
touch /www/fec-go/log/router_error.log
touch /www/fec-go/log/global.log
chmod 777 /www/fec-go/log/router_info.log /www/fec-go/log/router_error.log /www/fec-go/log/global.log

mkdir -p /www/fec-go/shell_log
touch /www/fec-go/shell_log/router_info.log
touch /www/fec-go/shell_log/router_error.log
touch /www/fec-go/shell_log/global.log
chmod 777 -R /www/fec-go/shell_log/router_info.log /www/fec-go/shell_log/router_error.log /www/fec-go/shell_log/global.log

mkdir -p /www/fec-go/xlsx
chmod 777 /www/fec-go/xlsx
```

2.将 github.com/fecshopsoft/fec-go/config/config.ini 的内容，复制到 `/www/fec-go/etc/config.ini`，

按照里面的配置说明，配置 `mysql` `mongodb` `elasticsearch`, 以及监听的ip端口

**此部分非常重要，设置数据库连接参数和设置监听的ip端口，清务必填写正确**

3.创建main.go文件

3.1在src/main 下面创建   fec-go.go  和 fec-go-verify.go 文件

3.2将目录（github.com/fecshopsoft/fec-go）下的 `fec-go.go`  和 `fec-go-shell.go`,
复制到 `main/fec-go.go` 和 `main/fec-go-shell.go`。

4.运行

4.1运行web监听脚本（该脚本需要一直运行）

> 该脚本用来接收数据，以及为vue部分提供api，也就是通过web url访问的部分，由这里提供。

进入到main下面，运行

```
go run fec-go.go
```

如果启动成功, 最后会显示：

```
2018/10/15 16:43:07 /root/go/src/github.com/gin-gonic/gin/debug.go:45: [GIN-debug] Listening and serving HTTP on 0.0.0.0:3000
```

`ctrl + c` 会停止当前运行的脚本。

4.2运行数据处理脚本

> 该脚本是数据处理脚本，用来处理数据，也就是将fecshop接收的初始数据进行各个维度的数据聚合，通过
mongodb的mapreduce进行数据分析，得到统计后的数据，以及将数据同步到 ElasticSearch 中。

```
go run fec-go-shell.go
```


```
go run fec-go-shell.go 1 removeEsAllIndex

```

第一个参数： 选填，代表处理N天内的数据统计，默认为`1`

第二个参数： `removeEsAllIndex`,如果删除elasticSearch里面的数据，加上这个参数值，
一般情况下不加这个参数。


4.3cron

> 对于数据统计脚本，一般一天统计一次，因此通过cron可以更好的运行。

```
1 1 * * * /usr/bin/wget http://120.24.37.249:3000/fec/trace/cronssss > /dev/null
01 * * * *  /root/go/src/main/fec-go-shell   >> /www/web_logs/fec-go-shell.log  2>&1
```

第一个是更新数据，将ip和端口换成你自己的即可，一分钟运行一次，这个脚本相当于刷新缓存的性质，
定时的刷新golang中的全局变量（因为有一部分的变量是从数据库里面初始化的，当数据库的内容修改后，
通过这个脚本进行刷新）。

第二个是周期跑数据的脚本，一天跑一次，将`/root/go/src/main/fec-go-shell` 替换成您自己的
路径，后面是log输出文件，自行创建并设置成可写。


### 配置信息

vue后台访问部分的域名为：http://trace.fecshop.com

golang提供的api的域名为：http://traceapi.fecshop.com

### VUE 后台展示部分


1.vue 环境：

```
git 2.7
python 3.6.5
npm 5.6
node 8.11.2
```

[git 2.7安装](http://www.fancyecommerce.com/2017/12/28/centos-%e5%ae%89%e8%a3%85-git/)

[python3安装](http://www.fecshop.com/topic/809)

[npm 5.6 && node8.11.2 安装](http://www.fecshop.com/topic/1397)

2.参考：https://github.com/fecshopsoft/vue-element-admin

按照下面的步骤安装即可

2.1下载
```
git clone https://github.com/fecshopsoft/vue-element-admin.git
```
2.2如果是国内，可以使用taobao源

```
sudo npm install --registry=https://registry.npm.taobao.org
```


2.3npm安装：

```
sudo npm install
```

3.启动

3.1开发模式启动

```
npm run dev
```

如果是本地，就可以访问：http://localhost:9527/#/

3.2生产模式生成静态文件

```
npm run build:prod
```

执行完成后，会生成一个dist文件夹，这个就是vue
编译后生成的静态html文件，可以配置nginx到这个路径，进行访问

3.3更多的其他启动模式参看：https://github.com/fecshopsoft/vue-element-admin.git


### nginx配置

1.后台vue部分相应的nginx配置

域名：`trace.fecshop.com`

vue编译生成的文件所在的路径，下面的配置为：/www/web/online/trace_fecshop/web

配置如下：

```
server {
    listen     80  ;
    server_name trace.fecshop.com;
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

2.golang的nginx配置。

因为上面golang监听的是 0.0.0.0:3000, 我的ip为：120.24.37.249
 ，golang的api访问地址为：`http://120.24.37.249:3000`

因此通过nginx反向代理，将 `http://traceapi.fecshop.com` 代理到`http://120.24.37.249:3000`
,配置如下：

```
server {
    listen 80;
    server_name traceapi.fecshop.com;
    location / {
      proxy_redirect off;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header REMOTE-HOST $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_pass http://120.24.37.249:3000;      # 这里ip地址设置成你的宿主主机ip+端口（或许可以localhost:端口，我没试）
    }
}
```

### vue admin部分的配置

配置是在 ./config文件夹中,下面是配置生产模式

打开文件 ./config/prod.env.js

```
module.exports = {
        NODE_ENV: '"production"',
        ENV_CONFIG: '"prod"',
        BASE_API: '"http://tracejs.fecshop.com"'
}
```

将 `BASE_API`对于的值改成您上面`golang` 对应的域名，然后通过
`npm run build:prod`重新编辑文件到`dist`文件夹中，
然后访问vue admin，后端api的数据将使用配置的`BASE_API`去找相应的数据。

###启动golang

> golang的启动在上面已经介绍了一下，这里重复说一下，可以按照下面的步骤操作：

1.首先在golang中手动执行一下下面的脚本

```
go run fec-go-shell.go
```

2.启动golang服务

```
go run fec-go.go
```


3.cron

> 对于数据统计脚本，一般一天统计一次，因此通过cron可以更好的运行。

```
1 1 * * * /usr/bin/wget http://120.24.37.249:3000/fec/trace/cronssss > /dev/null
01 * * * *  /root/go/src/main/fec-go-shell   >> /www/web_logs/fec-go-shell.log  2>&1
```

第一个是更新数据，将ip和端口换成你自己的即可，一分钟运行一次，这个脚本相当于刷新缓存的性质，
定时的刷新golang中的全局变量（因为有一部分的变量是从数据库里面初始化的，当数据库的内容修改后，
通过这个脚本进行刷新）。

第二个是周期跑数据的脚本，一天跑一次，将`/root/go/src/main/fec-go-shell` 替换成您自己的
路径，后面是log输出文件，自行创建并设置成可写。


然后您就可以访问vue admin了

### FA和Fecshop进行配置对接

参看：[FA和Fecshop进行配置对接](fa-config-fecshop.md)

对接完成后，可以在mongodb看到过来的数据

开启golang服务后，fecshop的js发送的数据和php服务端发送的数据，都会被golang接收，
将原始数据存储到mongodb中

上面的cron，会执行数据处理脚本，通过mongodb的mapreduce，进行数据的统计分析，然后将统计后的
数据保存到elasticsearch中。

您可以在vue admin中查看数据

> 注：如果文档中的描述出现错误或者有歧义，或者内容疏漏，请到 http://www.fecshop.com/topic
中发帖反馈，多谢