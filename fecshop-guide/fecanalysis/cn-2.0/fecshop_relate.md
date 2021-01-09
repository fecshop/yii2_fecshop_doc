Fecshop对接
==========

> 追踪系统和fecshop的对接


### 基础信息

1.提交，申请登录账户，通过后，登录账号进入系统

2.菜单：基础信息-->网站管理，添加网站信息（根据里面的提示）
，状态选择`enable`，填写完成后保存

3.如果保存成功，则点击编辑(Edit)按钮，打开编辑框，查看系统生成的信息：

`站点唯一标示(SiteUid)`: 这个是站点的`唯一标示`，网站的获取的信息中，必须含有该值，否则无法传递给Trace系统。

`追踪Js Url(Trace Js Url)`: 这个是电商网站需要添加的js，通过该js收集网站信息，并将数据传递给Trace系统

`验证Token(Access Token)`: 除了在浏览器加入js代码收集信息，
还需要服务端发送追踪数据，譬如订单支付信息，生成订单等这些没有界面的纯服务端
数据信息，因此，对于服务端发送的数据，需要做token
验证，该值的作用就是为了做Token验证。


### Fecshop中配置

> 想要收集数据，需要在电商商城中用js打点，然后将数据传递给Trace系统，
令人开心的是，fecshop已经将打点加入进去，您只需要开启配置就可以使用了

1.Fecshop系统的设置

打开Fecshop的配置文件 `@common/config/fecshop_local_services/Page.php`

`traceJsEnable`: 设置为`true`

`website_id` : 填写上面的`站点唯一标示(SiteUid)`

`access_token` : 填写上面的`验证Token(Access Token)`

`trace_url` : 填写上面的`追踪Js Url(Trace Js Url)`

`trace_api_url` : 这个需要向管理员获取

2.如果您需要使用VUE，也就是AppServer端的前端部分，您需要进行如下的设置：

测试环境打开： config/dev.env.js

生产环境打开： config/prod.env.js

添加配置：


```
TRACE_ENABLE: '"true"',   
TRACE_WEBSITE_ID: '"9b17f5b4-b96f-46fd-abe6-a579837ccdd9"',
TRACE_JS_URL: '"trace.fecshop.com/fec_trace.js"',
```

`TRACE_WEBSITE_ID`: 将里面的值替换成上面的`站点唯一标示(SiteUid)`

`TRACE_JS_URL`: 将里面的值替换成上面的`追踪Js Url(Trace Js Url)`


到这里就配置完成了。
























