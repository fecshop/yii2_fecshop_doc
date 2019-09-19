Fecmall 静态块
==============

> fecmall 静态块是指一块静态的html段，可以在后台通过配置的方式进行修改，
> 这样，可以很方面的让工作人员进行修改。

譬如首页的轮换大图，

![home](images/a1.jpg)

页面底部的文件条款等区块

![home](images/a2.jpg)

您可以在后台进行编辑

![home](images/a3.jpg)

![home](images/a4.jpg)

在content（内容部分），{{homeUrl}} 代表首页。 {{imgBaseUrl}} 代表图片url。
其中，{{imgBaseUrl}}为 对应的文件路径为@appimage/app入口名/


### 使用方法

1.首先在后台新建一个static block，譬如key为home-big-img

2.在代码中调用

```
Yii::$service->cms->staticblock->getStoreContentByIdentify('home-big-img','appfront')
```

第一个参数为key，第二个参数为入口的名字，这个参数的作用
是为了生成url（域名部分）。

