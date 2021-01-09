FA和Fecshop系统对接
=====================

> 在进行此步骤操作之前，保证您前面的操作都已经完成。


### Fecshop设置对接

1.添加网站，生成 `website_id` 和  `access_token`

从FA Admin后台中获取，您可以参看：
[trace 如何添加网站](fa-config-add-website.md)

通过上面的链接，您可以在FA系统中创建website，然后将这些配置信息填写到fecshop中，
作为安全认证。

2.添加js

下面是一个js文件：https://github.com/fecshopsoft/fec-go/blob/master/fec_trace.js

用来在电商商城中收集数据，您可以放到您的服务器的任意一个域名下面，只要 http://www.xx.com/fec_trace.js 访问到即可
，本处我放到了vue的dist文件夹下面，也就是和vue admin部分是一个域名，因此

在vue admin的`dist`文件夹下面，新建文件`fec_trace.js`，
然后将https://github.com/fecshopsoft/fec-go/blob/master/fec_trace.js
复制到新建的`fec_trace.js`文件中，然后打开`fec_trace.js`文件
的最后部分，可以看到:

```
img.src = '//tracejs.fecshop.com/fec/trace?' + args;
```

`tracejs.fecshop.com`: 这个是golang服务部分的域名，将这个域名替换成您自己的域名即可。

这样js收集的数据，就可以通过这个golang api url，发送数据，golang部分就会接收到数据，然后将数据写入到mongodb中。

3.Fecshop Appfront 和 Apphtml5配置

打开fecshop的@common/config/fecshop_local_services/Page.php

```
'trace' => [
	'class' => 'fecshop\services\page\Trace',
	// 关闭和打开Trace功能，默认关闭，打开前，请先联系申请下面的信息，QQ：2358269014
	'traceJsEnable' => false,
	// trace系统的 站点唯一标示  website id
	'website_id'    => '9b17f5b4-b96f-46fd-abe6-a579837ccdd9',
	// trace系统的Token，当fecshop给trace通过curl发送数据的时候，需要使用该token进行安全认证。
	'access_token'  => 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ3ZWJzaXRlX3VpZCI6IjliMTdmNWI0LWI5NmYtNDZmZC1hYmU2LWE1Nzk4MzdjY2RkOSJ9.-HsUq-qKcn2dhvGoxSYHVqMxNTH0cBcLsUl-R_utaCo',
	// 当fecshop给trace通过curl发送数据，最大的超时时间，该时间是为了防止
	'api_time_out' => 1.5, // 秒
	// 追踪js url，这个是在统计系统，由管理员提供
	'trace_url'     => 'trace.fecshop.com/fec_trace.js',
	// 管理员提供，用于发送登录注册邮件，下单信息等。
	'trace_api_url' => 'http://tracejs.fecshop.com/fec/trace/api',
],
```


`traceJsEnable`: 设置为`true`

`website_id`：`站点唯一标示`,就是在trace后台添加后获取的,就是上面的截图

`access_token`：`验证 Token`,就是在trace后台添加后获取的,就是上面的截图

`api_time_out`：服务端通过api给trace系统
发送数据，使用的是curl，该值是设置curl的最大超时时间，默认为`1.5`秒，
值越大，越不容易丢数据，值越小，php的等待时间越短，越不影响网站的运行，建议`1.5s`

`trace_url`：`追踪Js Url`，这个就是您前面配置的部分，将
`trace.fecshop.com/fec_trace.js`,中的`trace.fecshop.com`替换成您自己
的域名，这个就是上面第2部分添加的js文件，将js的地址添加到该处即可。

`trace_api_url`：`追踪Api Url`，这个就是您前面配置的golang api服务部分，将
`http://tracejs.fecshop.com/fec/trace/api`,中的`tracejs.fecshop.com`替换成您自己
的域名即可。

填写完成后，保存即可完成

> fecshop已经默认将埋点写入系统中，只需要配置即可使用，如果
您想关闭trace功能，只需要将配置中的
`traceJsEnable`: 设置为`false`即可，默认是`false`

4.Vue部分的AppServer部分的配置

Vue部分的地址为：
https://github.com/fecshop/vue_fecshop_appserver/

vue端指的是appserver部分，FA已经和VUE部分打通，可以接收vue端的数据，
这个也是FA比较独特的地方（很多的统计工具无法接收前后端彻底分离这种电商站点）

4.1配置prod环境

打开 `./config/prod.env.js`

```
module.exports = {
  NODE_ENV: '"production"',
  API_ROOT: '"//fecshop.appserver.fancyecommerce.com"',
  WEBSITE_ROOT: '"http://demo.fancyecommerce.com"',
  TRACE_ENABLE: '"true"',
  TRACE_WEBSITE_ID: '"9b17f5b4-b96f-46fd-abe6-a579837ccdd9"',
  TRACE_JS_URL: '"trace.fecshop.com/fec_trace.js"',
}
```

`TRACE_ENABLE`: 设置为true

`TRACE_WEBSITE_ID`: 这个是上面添加网站的website_id，填写即可

`TRACE_JS_URL`: 这个是用于收集数据的js，和上面的appfront部分的一致即可。

> 对于除prod除外的其他的开发模式等，自行在config文件夹中配置

然后重新编译生成prod的静态文件即可。



5.总结

经过了上面的配置，我们就完成了fecshop的配置，
然后测试一下数据，各个环节是否打通，数据是否进入到了golang服务对应的mongodb数据库中。






































