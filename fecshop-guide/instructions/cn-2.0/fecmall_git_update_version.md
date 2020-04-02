线上发版
===============

前面的一般都这样，搞一个dev分支，dev分支测试完成后，在不同的环境中测试，测试通过后， 加入到master分支测试，稳定后发布到线上。

可能有一些线上bug紧急处理的支线会直接进master

更新代码
如果有运维，可以运维写脚本处理

1.将线上的配置文件取出来，做一个文件包A

2.脚本执行的部分：

2.1git拖取 master分支（测试完成的分支）到线上

2.2将文件包A覆盖线上环境文件，设置文件权限等等

2.3刷新redis缓存等一些操作。

2.4清除一些.git等一些隐藏文件等等

2.5将发版信息，发送邮件，或者发送slack聊天工具等等，告知开发组等等

2.6回滚操作，如果某些步骤执行失败，那么前面执行成功的步骤，如果需要执行回滚操作的，需要执行回滚操作。

没有运维，自己也可以用shell写一下，不难，一个git命令，一个cp命令， 缓存可以手动刷新

3.简单的方式：

3.1因为本地和线上会有一些文件不一样，将这些不一样的文件不放到git里面，单独ftp上传，这种方式会存在一样的时间差

3.2除了一些数据库配置等万年不变的文件，不放到git里面，其他都放到git里面，然后在
线上做一个文件夹，里面是线上和本地开发不同的文件

让存在线上文件和本地文件不一致的时候，就可以将线上的文件，按照文件路径添加进去，
然后写一个shell文件，先git pull分支内容，然后执行cp命令，进行文件复制，
譬如：`git pull xxxxxxxx && \cp -rf xxxxx`
，另外还有redis刷新缓存等等，一系列发版需要操作的事情都写到这个shell文件里面，具体发版的版本，通过参数的方式传递到
这个shell文件里面的变量中。

3.3如果是多个php，更有必要写命令行，执行命令行发版，如果有运维，可以做一些操作界面的发版工具。

相关的一些讨论：http://www.fecshop.com/topic/1529



### 关于fecmall的`gitignore`文件说明


fecmall再开发过程中，为了让某些文件不上传到github上面，加入了一些`.gitignore`文件，下面进行说明

`.gitignore`是`git`在文件提交，进行某些文件的忽略的设置，关于`gitignore`的语法自行搜索

##### 您需要进行修改的`.gitignore`列表（根据自身情况，自行修改）

```
.gitignore  // 根目录
./addons/.gitignore  // 应用扩展文件夹

./appadmin/.gitignore  
./appadmin/config/.gitignore
./appadmin/web/.gitignore

./appapi/.gitignore
./appapi/config/.gitignore
./appapi/web/.gitignore

./appbdmin/.gitignore
./appbdmin/config/.gitignore
./appbdmin/web/.gitignore

./appfront/.gitignore
./appfront/config/.gitignore
./appfront/web/.gitignore
./appfront/web/语言文件夹/.gitignore   // 具体语言,如果没有，则忽略
./appfront/web/.gitignore

./apphtml5/.gitignore
./apphtml5/config/.gitignore
./apphtml5/web/.gitignore

./appserver/.gitignore
./appserver/config/.gitignore
./appserver/web/.gitignore

./common/config/.gitignore
./console/config/.gitignore
```


##### 详细说明

1.根目录的`.gitignore`文件

这里将`vendor`文件加入进去了，如果您想把`vendor`文件加入`git`，那么可以去掉`vendor`

2.应用扩展目录：`./addons/.gitignore`

```
*
!.gitignore
```

应用市场安装的扩展都在`./addons` 文件夹下，默认不提交到git里面，如果您想提交该文件夹下的文件到`git`,自行修改

3.各个入口的`.gitignore`文件，下面以`appfront`为例子说明，其他的入口（apphtml5，appadmin，appserver，appapi等）和这个类型

```
./appfront/config/.gitignore
`./appfront/web/.gitignore`
`./appfront/web/fr/.gitignore`   // 具体语言
./appfront/.gitignore
```


3.1appfront入口的配置部分: `./appfront/config/.gitignore`

```
main-local.php
params-local.php
```

这两个文件是入口的本地配置部分，关于这两个配置文件，可以将其添加到git，也可以去除，根据自己情况

3.1.1对于文件`./appfront/config/main-local.php`的配置部分`'cookieValidationKey' => 'FoOwzm-xxxxxxxxxxxxxxx',`，这个是在fecmall安装的时候生成的key，为了提高cookie的安全性，因此最好是本地和线上用不同的值（看自身情况决定）

3.1.2对于文件`./appfront/config/params-local.php`，这个目前没有什么配置，您可以将其放入到git里面

3.2appfront入口的web目录部分：`./appfront/web/.gitignore`

里面是web路径下的`gitignore`配置，根据自身情况，自行决定

另外，对于多语言部分，如果您需要用到，譬如`fr`语言`./appfront/web/fr/.gitignore`，那么您也需要配置一下，让其别忽略一些文件

3.3./appfront/.gitignore，可以将里面的内容去掉。


4.其他的入口，和appfront类型，这里不做说明

fecmall的数据库配置文件是在 `./common/config/main-local.php`文件里面，对应`./common/config/.gitignore`,这个文件是不应该提交到git里面的（线上和本地的数据库配置不同）


















