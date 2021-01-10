FA-2.0 QA问答
===========


一：我没有配置FA，如果关闭FA数据追踪

答：登陆Fecmall后台  `网站配置` --> `基础配置` --> `FA数据分析配置` 将`状态`设置为 `关闭`即可

二：我配置的FA，没有成功，用那个思路进行调试？


答：FA是一个数据逻辑的处理，您如果按照文档安装配置后，没有成功，可以依次从下面几个逻辑入口

1.fecmall开源版本是否2.9.3+？如果安装了fecyo，fecro等扩展，这些扩展是否是最新版本？
版本太低无法做对接。

2.登陆Fecmall后台  `网站配置` --> `基础配置` --> `FA数据分析配置

查看`状态`是否`开启`，`FA域名`是否填写正确？`FA Website Id` 和 `FA Access Token`，是否和FA添加网站后的`参数`保持一致？


3.打开您的fecmall首页，查看源代码，搜索`_maq`, 看一下，是否能找到下面的js字符串？


```
<script type="text/javascript">
    var _maq = _maq || [];
    _maq.push(['website_id', '72cf9542-47de-11eb-a32b-00163e021360']);
    _maq.push(['fec_store', 'fecyo.fecshop.com']);
    _maq.push(['fec_lang', 'en']);
    _maq.push(['fec_app', 'appfront']);
    _maq.push(['fec_currency', 'USD']);


    (function() {
        var ma = document.createElement('script'); ma.type = 'text/javascript'; ma.async = true;
        ma.src = ('https:' == document.location.protocol ? 'https://' : 'http://') + 'fatrace.fecmall.com/fec_trace.js';
        var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ma, s);
    })();
</script>
```

3.1上面js代码中的`fatrace.fecmall.com/fec_trace.js`就是FA的js，复制出来浏览器访问这个js，看看能不能访问？

这个js地址的域名，必须是您的FA系统的域名


3.2如果可以浏览器访问这个js，加载js文件后，查看js内容的最底部

```
 img.src = '//fatrace.fecmall.com/trace/js?' + args;
```

这个域名是否是您的FA域名？如果不是，进入到FA根目录  打开文件  `appfa/web/fec_trace.js`, 拉到文件最底部，修改域名即可，
注意修改后，清空一下浏览器缓存，否则js无法加载修改后的文件

这个域名的作用是，js收集的信息，通过加载这个图片文件，将参数发送到FA


4.打开mongodb，是否有数据？

譬如今天是`2021-01-10`，那么打开mongodb数据库`fa_trace_2021-01-10`，看一下是否有数据，
您可以访问一次fecmall商城，然后就查看mongodb 表（collection）里面是否有内容

如果没有内容，就代表对接没弄好，重复上面的1-3步骤找问题

如果有内容，就代表已经对接好。



5.手动执行统计脚本，核验检查

```
cd ./addons/fecmall/fecfa/shell
sh dailyStatistics.sh
```

执行后，等待脚本执行完成，看看log是否报错，如果没有报错，那么进入mongodb数据库
`fecfa`(您在common/config/main-local.php中配置的mongodb数据库)，查看是否有一系列的表产品，而且已经有统计后的数据？


6.进入后台查看

7.cron执行，如果手动执行脚本可以出来统计数据，而通过cron没有数据，则说明您的cron配置有问题

7.1查看设立了 `./addons/fecmall/fecfa/shell/dailyStatistics.sh`文件的权限，可以设置成`755`

7.2查看`cron log`日志，是否有输出？如果没有输出，则说明cron设置的语法有问题

如果`log日志`有输出，那么看看是否存在报错

等等



8.上面是一个完整的逻辑，检查您的FA的问题。











