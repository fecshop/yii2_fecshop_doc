Fecshop Vue 设置   
==============

> vue 做的客户段里面的设置和原理部分


### 1. 设置

对于vue做的客户端，github地址为：https://github.com/fecshop/vue_fecshop_appserver

按照github上面的说明安装完成后，就可以使用了。

vue客户端和appserver，是通过api进行数据传递，而且，实现了多语言功能




1.1 安装fecshop，并配置远程数据端，也就是下载fecshop的代码，然后配置好，让其可以访问
fecshop的appserver端，譬如，fecshop的演示地址为：//fecshop.appserver.fancyecommerce.com

1.2 安装VUE客户端部分，设置远程数据段地址：

开发配置文件：`config/dev.env.js`

生产配置文件：`config/prod.env.js`

```
API_ROOT: '"//fecshop.appserver.fancyecommerce.com"',
```

将`API_ROOT`对应的值改成您的值即可，也就是1.1 安装fecshop的appserver入口的地址。

1.2 多语言的设置

配置文件：src/config/store.js

配置内容如下：

```
STORE_CONFIG: [
    {
      'domain': '120.24.37.249:8080',
      'lang_code' : 'fr',
      'currency_code' : 'EUR',
    }
  ]
```

上面代表，如果域名为：`120.24.37.249:8080` ，则进入
网站的默认语言为fr，默认货币为EUR。
您可以配置多个域名，每个域名进入的时候，使用不同的默认语言和货币。


1.2 文字翻译

未...



### 2.数据传递


2.1 header: `fecshop-uuid`

`fecshop-uuid` 相当于pc浏览器开发中的session

数据发送：如果 `window.localStorage` 存在 `fecshop-uuid` ， 则发送的ajax请求，
需要加上该header。具体参看src/main.js 中的 `Vue.prototype.getRequestHeader`

数据接收：ajax请求获得响应后，在ajax response headers中，如果存在`fecshop-uuid`，则客户端需要将其保存到
`window.localStorage`中，以供下次ajax请求使用

2.1 header: `fecshop-lang` 和 `fecshop-currency`

通过第一部可以设置当前store的默认语言和默认货币，
值被保存到`window.localStorage`中，以后的每次ajax请求都需要带上这两个headers
，详情参看src/main.js































