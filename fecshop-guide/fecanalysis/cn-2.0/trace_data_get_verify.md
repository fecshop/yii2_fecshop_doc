接收数据安全验证
=================

### 接收数据验证

1.启动的时候，会初始化可用的website信息，也就是initialization/website.go
里面的InitWebsiteInfo()函数，执行后，
会将结果保存到 全局变量WebsiteInfos里面

只取customer  status 为enable ，customer对应的website status 为enable站点数据
，保存到 全局变量WebsiteInfos里面

2.对于trace系统，接收js和api端传送的数据，要判断是否是合法的数据。

2.1、传递的数据都必须有website_id字段，通过 website_id，
去 全局变量WebsiteInfos查看是否存在，

2.2、如果存在，判断是否过期，如果过期则丢弃

2.3、如果不过期，则查看一下日接收的最大数据数，如果没有到达阈值，则
保存，否则丢弃。

3.更新全局变量WebsiteInfos

因为数据会存在更新，因此，通过一个api访问来更新全局变量：
http://120.24.37.249:3000/fec/trace/crons
(4)

这样，接收数据的限制方面就完成了。




























