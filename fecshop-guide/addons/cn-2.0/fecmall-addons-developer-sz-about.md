Fecmall-开发扩展插件简介
=============

> 本部分文档，是从各个角度，详细阐述fecmall的各个机制，图文，代码实例的方式详细讲解，
方便开发快速的学习，上手，开发fecmall插件


### 开发扩展插件前，需要阅读的整体性文档。

在看本部分文档之前，建议您先看完 `Fecmall开发者中心`部分的文档


1.从整体角度逻辑阐述，fecmall开发者在开发插件的整体介绍：

- 如何在fecmall应用市场注册开发者账户，`添加应用`，

- 本地开发通过`Gii工具`初始化应用文件，

- 应用扩展入口配置文件`Config.php`的整体语法，

- Fecmall辅助工具`测试安装`，`升级`，`卸载`，

- Fecmall扩展插件文件`打包`

- Fecmall 应用市场`上传`应用，`审核`发布

- 应用`升级`

详细擦看文档：[Fecmall-开发者中心-创建发布升级应用](fecmall-addons-developer-center.md)


2.在应用市场已发布的插件，用户下单绑定关系后，可以在fecmall后台安装扩展，
fecmall扩展插件是如何在线安装的？原理是什么？

您可以参看文档：
[Fecmall-应用安装和加载原理](fecmall-addons-developer.md) ， 了解原理

3.fecmall的应用扩展文件包，是以`独立包`的方式，通过数据库配置应用扩展`config`文件路径，初始化的时候加载应用扩展的配置，
因此，应用扩展的`Config.php`文件是应用的核心配置所在，理解`Config.php`配置的语法才能更容易开发扩展。

详细参看：[Fecmall-应用配置文件Config.php配置详解](fecmall-addons-developer-config-example.md)

4.对于开发者本地开发扩展，需要手动创建各个文件，为了方便快速的`初始化组件`，您可以使用Gii工具，生成扩展`初始化`文件

详细参看：[Fecmall-应用初始化Gii工具](fecmall-addons-developer-init-tools.md)




### Fecmall-开发扩展插件详细


看完上面的这些文档，您对fecmall应用扩展在整体层面上有一个了解，
当我们开发具体的功能，就需要在`config.php`添加相应的配置，然后开发具体的功能来满足需要，
本部分就是以`细粒`角度，以例子的方式，详细阐述具体的语法和代码。


fecmall的应用开发具体详细，大致一下几个知识点

1.Fecmall-administer插件安装部分

插件作为一个扩展文件包，有`安装`，`升级`，`关闭`，`卸载`步骤，用户可以根据具体需要进行操作，
作为开发者，对于应用扩展在`安装`步骤，升级步骤需要执行的sql，需要写入到相应的文件里面，
当用户安装该插件的时候，自动执行相关操作

详细参看：[Fecmall-administer插件安装部分](fecmall-addons-developer-sz-administer.md)


2.Fecmall-module模块部分

fecmall的模块，本质就是`yii2`框架的模块，也就是将商城的各个业务块，拆分成多个模块`module`，
譬如`产品模块`，`购物车模块`，每个模块下面有各自的`controller`，`block`等

详细参看文档： [Fecmall-module模块部分](fecmall-addons-developer-sz-module.md)

3.Fecmall-component组件部分

Fecmall的`component`组件，本质就是yii2框架的组件，譬如`user`组件，`request`组件，您可以根据需要，重写现有组件的
配置，函数，或者开发新的组件以供需要

详细参看文档：[Fecmall-component组件部分](fecmall-addons-developer-sz-component.md)


4.Fecmall-services服务部分

Fecmall services，是fecmall的核心所在，fecmall是一个多入口模式的电商系统，各个入口的功能逻辑不同，
而`service`是公用的，为各个入口提供底层功能函数，开发者可以根据需要重写现有的`services`，开发新的`services`，
来满足需要

详细参看文档：[Fecmall-services服务部分](fecmall-addons-developer-sz-services.md)


5.Fecmall-theme模板部分

Fecmall-theme模板，是各个入口的view部分，譬如pc入口的商城页面，admin入口的后台界面等，开发者可以根据需要，
开发新的theme模板，替换`view`，`css`，`js`等，或者添加新的css js文件

详细参看文档：[Fecmall-theme模板部分](fecmall-addons-developer-sz-theme.md)


6.Fecmall-translate翻译部分

如果给各个入口添加`翻译`，以及翻译的原理

详细参看文档：[Fecmall-translate翻译部分](fecmall-addons-developer-sz-translate.md)


7.Fecmall-邮件部分

如何配置邮件，邮件原理，以及`重写`邮件模板等

详细参看文档：[Fecmall-邮件部分](fecmall-addons-developer-sz-email.md)


8.Fecmall-model部分

Fecmall-model，就是`MVC`结构中的`m`部分，也就是`数据库对象`，fecmal的model本质就是yii2框架的`model`

详细参看文档：[Fecmall-model部分](fecmall-addons-developer-sz-model.md)


9.Fecmall-yii2部分

yii2框架，fecmall对其的一些重写

详细参看文档：[Fecmall-yii2部分](fecmall-addons-developer-sz-yii2.md)


10.Fecmall-其他的部分

其他的一些内容的补充

详细参看文档：[Fecmall-其他的部分](fecmall-addons-developer-sz-other.md)





