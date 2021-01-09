Fecshop和Trace系统对接
=====================


### fecshop设置对接

下面的信息，`website_id` 和  `access_token`
是从trace后台中获取，您可以参看：
[trace 如何添加网站](trace-fecshop-config.md)

1.打开fecshop的@common/config/fecshop_local_services/Page

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
发送数据，使用的是curl，该值是设置curl的最大超时时间，默认为`1.5`秒

`trace_url`：`追踪Js Url`，这个就是您前面配置的部分，将
`trace.fecshop.com/fec_trace.js`,中的`trace.fecshop.com`替换成您自己
的域名

`trace_api_url`：`追踪Api Url`，这个就是您前面配置的部分，将
`http://tracejs.fecshop.com/fec/trace/api`,中的`tracejs.fecshop.com`替换成您自己
的域名即可。

填写完成后，保存即可完成

> fecshop已经默认将埋点写入系统中，只需要配置即可使用，如果
您想关闭trace功能，只需要将配置中的
`traceJsEnable`: 设置为`false`即可，默认是`false`















