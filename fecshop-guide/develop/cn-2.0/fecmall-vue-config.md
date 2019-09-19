Fecshop 客户端说明（Vue）
==============

> vue 做的客户段里面的设置和原理部分


### 1.安装设置

对于vue做的客户端，github地址为：https://github.com/fecshop/vue_fecshop_appserver

按照github上面的说明安装完成后，就可以使用了。


 
### 2.VUE开发

VUE需要在本地（localStorage）存储一些变量，用来标示当前的一些类似session的状态


2.1、`fecshop-uuid`

Fecshop-2版本已经弃用！

2.2、`access-token`

该值用于存储 `用户是否登录` 的标示，当用户登录账号成功后，服务端
就会在`response header access-token` 中存放值，VUE取到值后，通过函数
`Vue.prototype.saveReponseHeader`，将其保存到localStorge中，
然后，后面的每次访问都从
localStorge中取出值，放到`request header access-token`中。
服务端从`request header access-token`取出来值，用来辨别登录的用户身份



2.3、`fecshop-lang` 和 `fecshop-currency`

存储到localStorage中，用来保存当前store的 `语言` 和 `货币`，

当用户第一次访问，VUE会从localStorage中取出这两个值，如果这两个值
都为空，VUE会从 `src/config/store.js` 取出来store的配置，如下：

```
export default {
    storeConfig:[
      {
        'domain': 'demo.fancyecommerce.com',  //配置的域名，只有该域名和当前的域名一致的时候，下面的设置才会生效，如果当前域名不是demo.fancyecommerce.com，则不会生效
        'lang_code' : 'fr',
        'currency_code' : 'EUR'
      }
    ]
}
```

如果 VUE从storeConfig中找到了匹配的域名 （`当前的域名 == storeConfig[x]['domain']`）,则会使用配置中的值来初始化 
`fecshop-lang` 和 `fecshop-currency`，并保存到localStorage中。

如果 VUE从storeConfig中找不到匹配的域名，在访问服务端完成后，服务端会将
默认的语言和货币取出来，放到`response header` 中，
返回服务端默认的语言和货币值，客户端（VUE）接收到请求后，VUE会存储到localStorage中，
供下次ajax请求使用。

下次ajax请求，VUE 会从localStorage 取出来 `fecshop-lang` 和 `fecshop-currency`
放到`request header`中，服务端接收请求后，会使用VUE在`request header` 中的值
来返回相应的数据。


当如上设置后，用户第一次打开网站的语言就是法语，对应欧元货币。

从配置中取出来`fecshop-lang` 和 `fecshop-currency`的实现原理：

代码文件为：src/main.js

```
// default 设置 , 如果 localStorage 没有设置语言和货币，则通过配置设置。
// 这样做的是为了搞多语言，可以多个子域名解析过来，不同的域名设置不同的默认货币和语言。
// 下面的语言必须在服务端进行了相应的设置。 @appserver/config/fecshop_local_services/Store.php 的  serverLangs 设置语言
// 下面的货币必须在服务端进行了相应的设置。 @common/config/fecshop_local_services/Page.php 的 currencys 设置货币
var current_domain = window.location.host;
console.log('current_domain ######' + current_domain);
var store_config = store.storeConfig;
var fecshop_lang = window.localStorage.getItem("fecshop-lang");
var fecshop_currency = window.localStorage.getItem("fecshop-currency");
if(!fecshop_lang || !fecshop_currency){
    for(var k in store_config){
        var one = store_config[k];
        if(one.domain == current_domain){
            if(!fecshop_lang){
                console.log('### domain config set lang')
                window.localStorage.setItem("fecshop-lang",one.lang_code);
            }
            if(!fecshop_currency){
                console.log('### domain config set currency')
                window.localStorage.setItem("fecshop-currency",one.currency_code);
            }
        }
    }
}
```





3.从localStorage设置和取出的函数

详细参看文件：src/main.js

3.1、从localStorage取值的函数

```
Vue.prototype.getRequestHeader = function (){
    var headers = {};
    var fecshop_lang = window.localStorage.getItem("fecshop-lang");
    if(fecshop_lang){
        console.log('fecshop lang ######' + fecshop_lang);
        headers['fecshop-lang'] = fecshop_lang;
    }
    var fecshop_currency = window.localStorage.getItem("fecshop-currency");
    if(fecshop_currency){
        console.log('fecshop currency ######' + fecshop_currency);
        headers['fecshop-currency'] = fecshop_currency;
    }
    var access_token = window.localStorage.getItem("access-token");
    if(access_token){
        console.log('fecshop access-token ######' + access_token);
        headers['access-token'] = access_token;
    }
    return headers;
    //console.log('get header ####');
}
```

3.2、将值设置到localStorage中的函数

```
Vue.prototype.saveReponseHeader = function (response){
    // access-token
    var access_token = response.getResponseHeader('access-token');
    if(access_token){
        console.log('save header [access-token1]' );
        var local_access_token = window.localStorage.getItem("access-token");
        console.log('save header [access-token2]' );
        if(local_access_token != access_token){
            console.log('save header [access-token3] ######' + access_token);
            window.localStorage.setItem("access-token",access_token);
            
        }
    }
    // lang
    var fecshop_lang = response.getResponseHeader('fecshop-lang');
    if(fecshop_lang){
        var local_fecshop_lang = window.localStorage.getItem("fecshop-lang");
        if(local_fecshop_lang != fecshop_lang){
            window.localStorage.setItem("fecshop-lang",fecshop_lang);
            console.log('save header [fecshop-lang] ######' + fecshop_lang);
        }
    }
    // currency
    var fecshop_currency = response.getResponseHeader('fecshop-currency');
    if(fecshop_currency){
        var local_fecshop_currency = window.localStorage.getItem("fecshop-currency");
        if(local_fecshop_currency != fecshop_currency){
            window.localStorage.setItem("fecshop-currency",fecshop_currency);
            console.log('save header [fecshop-currency] ######' + fecshop_currency);
        }
    }
}
```


3.2、ajax调用的例子 ：

譬如：https://github.com/fecshop/vue_fecshop_appserver/blob/master/src/views/body/cms/Page.vue

```
$.ajax({
    url: self.pageInitUrl,
    async: true,
    timeout: 120000,
    dataType: 'json', 
    type: 'get',
    headers: self.getRequestHeader(), // 将本地的参数取出来放到request header 的参数中。
    data:{ 
        url_key:page_key
    },
    success:function(reponseData, textStatus,request){
        if(reponseData.code == 200){
            self.title = reponseData.data.title;
            self.content = reponseData.data.content;
            self.saveReponseHeader(request);    // 将response header 里面的参数保存到本地。
        }
        $.hideIndicator();
    },
    error:function(){
        $.hideIndicator();
        $.toast("system error");
        console.log('get get Category info error');
    }
});


```

























