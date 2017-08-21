Fecshop vagrant安装
====================

> Vagrant是一个基于Ruby的工具，用于创建和部署虚拟化开发环境。
> 我使用vagrant已经打包好一个box，您可以通过加载我打包好的box进行快速部署
> fecshop的开发环境，vagrant是类似docker的容器类软件，不过和docker原理不同，
> 通过这种方式安装，你就不需要进行繁琐的手动安装各种环境和配置，可以快速部署Fecshop，
> 当然，你可以使用全手动安装方式.
> 
> 链接如下：[Fecshop 全手动安装](fecshop-about-hand-install.md)

您加载我打包好的vagrant box，直接加载过来即可，这个里面的fecshop版本比较老，
需要进一步升级。

vagrant 基础知识：你可能没有使用vagrant，这个没有关系，我整理了一份vagrant使用的教程，地址如下：
[vagrant 下载部署linux环境](http://www.fancyecommerce.com/2016/09/22/vagrant-%E4%B8%8B%E8%BD%BD%E9%83%A8%E7%BD%B2linux%E7%8E%AF%E5%A2%83/)
这些仅仅是参考知识，不是fecshop的安装步骤。

通过vagrant安装fecshop，非常的简便，下面是详细步骤：


### 1.下载Fecshop 环境的box

box地址在百度云盘，下载地址为：[百度云盘vagrant box 下载地址](https://pan.baidu.com/s/1kVwRD2Z) ， 
进入后打开文件夹，下载 package.box即可（就是2.35G的那个文件）。

### 2.本地windows添加hosts

打开C:\Windows\System32\drivers\etc\hosts，添加如下代码（如果是其他IP，将
127.0.0.1 替换成其他IP即可。）：

```
127.0.0.1       rock.fecshoptest.com
127.0.0.1       my.fecshoptest.com
127.0.0.1       appadmin.fecshoptest.com
127.0.0.1       appfront.fecshoptest.com
127.0.0.1       appfront.fecshoptest.es
127.0.0.1       apphtml5.fecshoptest.com
127.0.0.1       appapi.fecshoptest.com
127.0.0.1       appserver.fecshoptest.com
127.0.0.1       img.fecshoptest.com		#appimage/common
127.0.0.1       img2.fecshoptest.com	#appimage/appadmin
127.0.0.1       img3.fecshoptest.com	#appimage/appfront
127.0.0.1       img4.fecshoptest.com	#appimage/apphtml5
127.0.0.1       img5.fecshoptest.com	#appimage/appserver
```

### 3.下载vagrant 和 virtual box 并安装

#### 3.1安装 VirtualBox

虚拟机VirtualBox下载地址：https://www.virtualbox.org/wiki/Downloads

![virtual images](http://img.blog.csdn.net/20160922172454894?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

#### 3.2下载  Vagrant

下载地址：http://downloads.vagrantup.com/

![xiazai](http://img.blog.csdn.net/20160922171328380?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)


经过上面的下载，我们

下载了virtual box   vagrant  二个文件（如图第二个和第三个文件）

![va](http://img.blog.csdn.net/20160922171537180?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

安装 virtualbox ，  vagrant ，这个基本都是下一步，安装完成后要重启



### 4.加载第一部的box，创建虚拟机运行linux

#### 4.1查看vagrant是否安装成功，window建+r ，打开命令行，

![xx](http://img.blog.csdn.net/20160922171658306?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

进入命令行模式，输入vagrant，看看是否安装成功


![xx](http://img.blog.csdn.net/20160922171850354?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

#### 4.2复制box文件

如果安装成功，
在d盘创建文件夹D:\vagrant_lib，然后把第一步下载的package.box复制
到这个文件夹下面
，box的文件路径为 - D:\vagrant_lib\package.box

#### 4.3add vagrant box

按照这个命令添加fecshop box  `vagrant box add 名称 路径`

```
c:\Users\lenovo>d:

D:\>cd vagrant_lib

D:\vagrant_lib>vagrant box add fecshop package.box

```

通过上面的步骤就可以把box加载进来了. 上面添加box的时间会几分钟才能
完成


#### 4.4创建虚拟机

在d盘下面创建一个新的文件夹  vagrant_fecshop，绝对路径为
D:/vagrant_fecshop,进入到这个文件夹下面。执行如下代码

```
vagrant init fecshop
```

完成后，就会在D:/vagrant_fecshop下面生成一个文件，  D:/vagrant_fecshop/Vagrantfile
打开这个文件找到代码
`config.vm.network "forwarded_port"`,将这行代码替换成

```
   config.vm.network "forwarded_port", guest: 80, host: 80
```

注意，前面的注释#要去掉，另外，如果你本地windows有软件占用80端口，请关掉，譬如您本地开启了xampp 
wamp等，请关掉，因为会占用本地win的80端口。

#### 4.5通过vagrant启动虚拟机

也就是在路径D:/vagrant_fecshop下输入命令：

```
vagrant up
```

启动 vagrant up命令，第一次会慢一些，因为要复制文件。

![xxx](http://img.blog.csdn.net/20160922172706451?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)



如果在出现ssh信息，后面有一些警告信息，可以不用理会，直接用ssh连接即可，如果出现其他报错，请查看文章：http://www.fancyecommerce.com/2016/09/22/vagrant-%E4%B8%8B%E8%BD%BD%E9%83%A8%E7%BD%B2linux%E7%8E%AF%E5%A2%83/ 
，
这里面有一些对vagrant报错的解决方案，如果出现其他的报错，请使用bing.com或者google搜搜。

启动成功后，您就可以通过ssh连接了，注意ssh的端口为2222，而不是22，

```
ssh 连接

ip:127.0.0.1

端口:2222

用户名：vagrant，密码 ：vagrant

root的密码也是vagrant (如果密码错误，那就是123456，我忘记打包box时，密码是那个了)

```

您可以通过 appfront.fecshoptest.com 来访问前端。


下面是nginx中的配置，各个入口的域名和对应的文件路径为：

```
pc端地址：appfront.fecshoptest.com appfront.fecshoptest.es 指向 /www/web/develop/fecshop/appfront/web 

后台端地址：appadmin.fecshoptest.com 指向/www/web/develop/fecshop/appadmin/web

html5端地址（未开发）：apphtml5.fecshoptest.com 指向/www/web/develop/fecshop/apphtml5/web

api端地址（未开发）：appapi.fecshoptest.com     指向/www/web/develop/fecshop/appapi/web

手机app端地址（未开发）：appserver.fecshoptest.com 指向/www/web/develop/fecshop/appserver/web

common图片端地址：img.fecshoptest.com     指向/www/web/develop/fecshop/appimage/common

appadmin图片端地址：img2.fecshoptest.com  指向/www/web/develop/fecshop/appimage/appadmin

appfront图片端地址：img3.fecshoptest.com  指向/www/web/develop/fecshop/appimage/appfront

apphtml5图片端地址：img4.fecshoptest.com  指向/www/web/develop/fecshop/appimage/apphtml5

appserver图片端地址：img5.fecshoptest.com     指向/www/web/develop/fecshop/appimage/appserver

rock mongo访问地址：rock.fecshoptest.com    账号：admin  密码：123456

phpmyadmin访问地址: my.fecshoptest.com      账号：root   密码：123456

后台端地址：appadmin.fecshoptest.com访问后，后台的用户名和密码为admin  123456（如果密码不对，就试试admin123）
```



这样就可以访问了，譬如：appfront.fecshoptest.com 访问前端pc web，
appadmin.fecshoptest.com 访问后台web


### 5.vagrnat 常用命令


```
    vagrant init  # 初始化
    vagrant up  # 启动虚拟机
    vagrant halt  # 关闭虚拟机
    vagrant reload  # 重启虚拟机
    vagrant ssh  # SSH 至虚拟机
    vagrant status  # 查看虚拟机运行状态
    vagrant destroy  # 销毁当前虚拟机
```

### 6.vagrant 常见问题以及方法

1.在启动的时候报错：`default : warning: Authentication failure . Retrying...`

这个没啥大问题，可以直接连接使用。

2.vagrant的fecshop文件如何映射到本地？

vagrant box安装后，在虚拟linux中的文件路径为/www/web/develop/fecshop
，您可以先启动vagrant，将fecshop文件夹改下名字，譬如为：
/www/web/develop/fecshop_cp，然后修改 Vagrantfile，内容如下：

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "centos-6.6-x86_64"
  config.vm.hostname = "dev"
  config.ssh.username = "root"
  config.ssh.password = "123456"
  config.ssh.insert_key = "true"
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
  config.ssh.forward_agent = true
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
   config.vm.network "forwarded_port", guest: 80, host: 80

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  ## config.vm.network "private_network", ip: "192.168.10.12"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  ## config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
    config.vm.synced_folder "D:\\linux\\fecshop", "/www/web/develop/fecshop"
  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true
    vb.name = "dev"
    # Customize the amount of memory on the VM:
    vb.memory = "2048"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end

```

把上面的内容复制到您的`Vagrantfile`中，下面是对该配置文件中的解释。

下面的这个部分是对centos的一些定义，譬如下面配置的root账户密码等

```
config.vm.box = "centos-6.6-x86_64"
  config.vm.hostname = "dev"
  config.ssh.username = "root"
  config.ssh.password = "123456"
  config.ssh.insert_key = "true"
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
  config.ssh.forward_agent = true
```

`config.vm.network "forwarded_port", guest: 80, host: 80` : 端口映射配置，
将vagrant的80映射到本地的80
，这里要注意，要把本地的占用80端口的东西给关掉。

`config.vm.network "private_network", ip: "192.168.10.12"` : 默认给注释了。
这个是映射ip，如果注释这个代码，linux的ip为`127.0.0.1`

`config.vm.synced_folder "D:\\linux\\fecshop", "/www/web/develop/fecshop"`:
这个是地址映射，将window的 `D:\\linux\\fecshop` 挂载到
linux的`/www/web/develop/fecshop`中，这里需要注意的是，如果linux中存在
一个文件夹 /www/web/develop/fecshop，那么，按照上面的配置后重启vagrant
，则linux文件夹将无法访问，访问的是当前配置
的文件夹（就是"D:\\linux\\fecshop"），因此，在上面，我们先把vagrant中的`/www/web/develop/fecshop`改为`/www/web/develop/fecshop_cp`。
然后在做上面的配置

在window需要新建文件夹：`"D:\\linux\\fecshop"`


配置完成后，重启vagrant，shell连接进入linux，然后执行

```
\cp -rf /www/web/develop/fecshop_cp/. /www/web/develop/fecshop/
```

即可，然后在 `D:\\linux\\fecshop` 就可以看到相应的文件了，
然后用phpstorm加载这里的文件即可，当`D:\\linux\\fecshop`中的文件被改动
，linux中 `/www/web/develop/fecshop/` 就会改动，因为这属于磁盘挂载类型，
这样就可以愉快的做开发了。















