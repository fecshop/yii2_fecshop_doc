数据对接原理
============


> 通过js和api两种方式获取追踪数据


### 步骤

1.在追踪系统生成SiteUid，Token，TraceJsUrl等信息

2.Api Url 由管理员提供，这个url是和上面的TraceJsUrl
中的js发送数据的Api Url的域名地址是一致的。

3.在网站中填写这些信息，详情参看[FA-2.0安装](fecmall-analysis-2-install.md)

4.fecshop page Trace services（`Yii::$service->page->trace`），通过配置信息和方法
`getTraceCommonJsCode()`,生成通用追踪信息，

在@app/appfront/theme/base/front/widgets/trace.php中可以看到

```
<?= Yii::$service->page->trace->getTraceCommonJsCode()  ?>
```

这个文件嵌入到了所有的`layout`中，这段代码将显示出来上面的追踪js

4.2对于其他页面的信息的信息，譬如产品页面加入sku，购物车页面加入cart信息，这个
是在具体页面中加入的

譬如产品页面 @app/appfront/theme/base/front/catalog/product/index.php中可以看到：

```
<?= Yii::$service->page->trace->getTraceProductJsCode($sku)  ?>
```

4.3除了js追踪数据，还有php直接给追踪系统发送数据


目前，账户注册，登录，生成订单，订单支付状态修改4个功能的数据发送，是php
发送给追踪系统的

通过 `Yii::$service->page->trace->apiSendTrace($data)` 方法

使用accessToken做安全认证

php服务端发送数据，也分为2种：

用户发起的请求：这种请求是由用户发起，是有cookie的，譬如账户登录，注册，生成订单，一种是有cookie的，譬如账户登录，注册，生成订单，
都是用户发起的请求，进而可以把用户的cookie传递过来，进而数据比较全

paypal ipn发起的请求：这种是paypal ipn发送支付消息给fecshop，
fecshop接收后，需要传递给Trace 系统，这种没有用户的cookie，
但是这种不是添加数据，而是更新订单的支付状态，因此，通过
website_id（网站唯一标示）和invoice（订单号），就可以找到订单唯一行，
然后更新订单状态（mongodb需要做索引）

通过上面的3点，我们将appfront，和apphtml5搞定。


5.vue端（FA-2.0暂不支持vue。下面是FA-1.0的文档，暂时保留）

vue端略复杂一些

5.1我们需要到vue客户端配置
详情参看[Fecshop网站对接](fecshop_relate.md) 第二部分

5.2在文件src/main.js文件中可以看到

```
var trace_website_id = process.env.TRACE_WEBSITE_ID;
var trace_enable = process.env.TRACE_ENABLE;
var trace_js_url = process.env.TRACE_JS_URL;
```
将配置中的信息取出来，

然后通过函数

```

Vue.prototype.reloadTraceJs = function (data){
    if (trace_enable == 'true') {
        // 获取js url
        var sSrc = ('https:' == document.location.protocol ? 'https://' : 'http://') + trace_js_url;
        var scriptSrc;
        // 添加website_id参数
        scriptSrc = sSrc + '?website_id=' + trace_website_id;
        var fecshop_lang = window.localStorage.getItem("fecshop-lang");
        var fecshop_currency = window.localStorage.getItem("fecshop-currency");

        // 添加语言参数
        scriptSrc += '&fec_lang=' + encodeURIComponent(fecshop_lang);
        // 添加货币参数
        scriptSrc += '&fec_currency=' + encodeURIComponent(fecshop_currency);
        // 添加入口参数
        scriptSrc += '&fec_app=appserver';
        // 添加store 参数 - 因为appserver端没有store概念，因此没有
        
        // 添加当前页面参数
        for (var k in data) {
            var v = data[k];
            scriptSrc += '&'+k+'=' + encodeURIComponent(v);
        }
        // 删除前面添加的script
        var allScript = document.getElementsByTagName('script'); 
        for (var i=allScript.length; i>=0; i--){ 
            if (allScript[i] && allScript[i].getAttribute("src")!=null && allScript[i].getAttribute("src").indexOf(sSrc)!=-1){
                allScript[i].parentNode.removeChild(allScript[i]); 
            } 
        } 
        // 重新添加js文件，并加载。
        var ma = document.createElement('script'); ma.type = 'text/javascript'; ma.async = true;
        ma.src = scriptSrc;
        var s = document.getElementsByTagName('script')[0];
        s.parentNode.insertBefore(ma, s);
    }
}  
```

将vue中各个页面的数据传递过来，然后加载js，js将数据发送给trace系统。

和appfront和apphtml5端不同的是，前者使用的是通过变量`_maq` 传递给Js文件，
将`_maq`的值传递给`params`变量，
而vue端是将参数加入到js的url中，然后js通过解析自己的url，将参数获取，
赋值给`params`变量。


实现代码如下：

```
var params = {};
    if( "undefined" != typeof _maq){
    // if(_maq) {
        for(var i in _maq) {
            var x = _maq[i][0];
            if(x){
                params[x] = _maq[i][1];
            }
        }
    } else {
        var jsPath = getJsPath("fec_trace.js");
        var urlparse = jsPath.split("\?");  
        var parms = urlparse[1].split("&"); 
        for(var i = 0; i < parms.length; i++) {  
            var pr = parms[i].split("="); 
            params[pr[0]] = pr[1]; 
        }  
    }
    
    function getJsPath(jsname) {  
        var js = document.scripts;  
        var jsPath = "";  
        for (var i = js.length; i > 0; i--) {  
            if (js[i - 1].src.indexOf(jsname) > -1) {  
                return js[i - 1].src;  
            }  
        }  
        return jsPath;  
    }  
```

所有页面的刷新都需要调用函数this.reloadTraceJs(data):


也就是上面main.js中定义的 `Vue.prototype.reloadTraceJs`

譬如在产品页面  src/views/body/product/Index.vue中的函数fetchProduct()
执行成功后会执行下面的代码：

 
```
// sku trace
var traceData = {"sku": product.sku};
self.reloadTraceJs(traceData);
```

这样就完成了数据的传递

5.3对于登录注册，订单生成等服务端发送的数据，需要vue
发送自身的cookie给服务端（vue类型是api类型，是无状态的，
只从post或get中获取数据），
因此需要获取当前的所有cookie。

在src/main.js中可以看到函数

```
  
Vue.prototype.getTraceAllCookie = function (){
    var cookies = { };
    if (document.cookie && document.cookie != '') {
        var split = document.cookie.split(';');
        for (var i = 0; i < split.length; i++) {
            var name_value = split[i].split("=");
            name_value[0] = name_value[0].replace(/^ /, '');
            cookies[decodeURIComponent(name_value[0])] = decodeURIComponent(name_value[1]);
        }
    }
    return cookies;
}              
```

该函数返回所有的vue端的cookie

譬如 src/views/body/customer/account/Login.vue

可以看到：

```
var cookies = self.getTraceAllCookie();
```

还有 src/views/body/checkout/Onepage.vue中，也可以看到

发送后，服务端会根据cookie信息，给追踪系统发送数据。

5.4对于paypal ipn的信息，是直接发送给服务端的，服务端接收到，更改订单状态。
对于website_id是从fecshop的配置中获取的，发送数据后，Trace接收后更改订单状态


















