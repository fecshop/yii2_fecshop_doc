Fecmall-安装应用
============

> Fecmall的应用安装，都是在线安装，在安装之前，您需要到应用市场注册账户，应用下单绑定对应关系，
Fecmall的应用大多数都是免费的，绑定关系后，您就可以在fecmall后台应用中心进行在线安装了

`注意`：Fecmall应用的下载源是国内的阿里云，如果您是海外主机，可能会存在下载超时问题
，您可以设置一下php的超时时间，如果还是不行，您可以在本地或者国内主机安装fecmall，将需要的应用全部安装，
然后以服务器迁移的方式部署到海外主机，[Fecmall项目迁移服务器](http://www.fecmall.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_host_change.html)


### FecMall应用市场


1.FecMall应用市场地址：http://addons.fecmall.com/

2.点击右上角的登陆账户按钮，然后点击注册用户，即可注册成为应用市场用户

3.在应用市场中浏览相应的应用，中意的应用可以添加到购物车进行下单

4.下单成功后，既可以在我的应用中心查看

![](images/t1.png)


### 5.用户安装FecMall电商系统

登陆fecmall admin后台，点击应用市场，登陆用户（注意：是fecmall应用市场的注册账户）

![](images/zz91.png)

登陆成功后，即可看到我的应用列表：

![](images/zz92.png)

### 6.在线安装应用

> 用户点击`安装按钮`，即可安装应用

**安装应用前一定要备份数据库！！！！**

有的插件可以几十MB，下载需要时间，您需要耐心等待插件下载完成并安装

如果报错nginx 502 Bad Gateway，请参看：[Fecmall-安装应用-超时问题](fecmall-addons-install-timeout.md)



http://www.fecmall.com/topic/4824

### 7.缓存刷新

1.刷新缓存：安装完应用后需要刷新一下`缓存`，登陆后台，点击菜单： `控制面板` -->  `缓存管理`  ,勾选，刷新缓存

目前最新版本的fecmall，安装新应用后会自动刷新当前用户的后台菜单缓存信息。

2.刷新浏览器，查看后台配置的菜单是否出来，如果没有出来，退出账户，重新登陆试一下。

### 8.应用扩展卸载

由于fecmall的插件的卸载机制，为了安全并没有进行数据库的`卸载`（只做了文件的卸载），如果出现超时现象，您有3种方式解决：

1.需要`手动卸载sql`，您可以参看`administer/Install.php`，查看执行的`sql`，然后手动删除，如果插件执行的sql太多，这个很麻烦，`不建议采用`

2.使用`备份还原`，然后`重新安装`应用插件，推荐该方式，在安装扩展之前一定要先备份sql，发生问题通过sql还原。

3.如果是`新安装`的fecmall，您又没有备份，那么可以`重新安装fecmall`，备份一下sql，然后再进行安装应用。




### 8.按照应用扩展说明，进行其他的一些配置即可使用。

在应用的描述部分，可能有一些安装的说明，仔细阅读，按照他的方法进行`配置`即可。

### 9.如果您安装插件过程中遇到问题，出现错误等


可以用chrome
浏览器查看一下`ajax`的报错信息，发帖到fecmall论坛即可。（然后将帖子地址发给应用开发者）

官网论坛开了一个帖子，整理了安装应用的注意问题：http://www.fecmall.com/topic/2535

`95%`的用户安装应用失败，原因在于 `php超时`（或者nginx）问题，参看帖子：http://www.fecmall.com/topic/2474








