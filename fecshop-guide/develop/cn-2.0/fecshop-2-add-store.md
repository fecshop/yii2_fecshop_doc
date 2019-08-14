Fecmall-添加多语言Store
============


### 配置多语言讲解
 
> appfront, apphtml5, appserver 入口都可以配置多语言store
 
1.配置appfront的多语言，fecmall配置多语言store有两种方式：
 
1.1通过子目录的方式，譬如fr,cn,其他的语言可以复制fr文件夹
 
 打开文件夹：D:\wamp64\www\fecshop\appfront\web ， 可以看到
 
![](images/qq50.png)
 
fr 和cn两个目录，
 

 
1.2通过子域名的方式，譬如 ： http://es.appfront.fecshoptest.com , http://de.appfront.fecshoptest.com
 
 下面我们都操作一下：
 
### 后台配置多语言store
 


 
 
 
1.配置子目录方式

1.1譬如:fr语言，打开后台appfront，进行配置（看不清，请放大浏览器查看）
 
![](images/qq48.png)
 
 保存，然后访问：http://appfront.fecshoptest.com/fr/ ， 就可以访问fr语言了

1.2配置子路径方式的cn语言，打开后台appfront，进行配置
 
![](images/qq51.png)
 
 保存，然后访问：http://appfront.fecshoptest.com/cn/ ， 就可以访问cn语言了
 
2.配置子域名方式
  
2.1子域名多语言store，域名为：es.appfront.fecshoptest.com
，需要您自行添加hosts，和nginx（apache）进行配置域名指向web目录
 
 
2.2配置子域名方式的es语言，打开后台appfront，进行配置：es.appfront.fecshoptest.com
 

 ![](images/qq53.png)
 
 保存，然后访问：http://es.appfront.fecshoptest.com ， 就可以访问es语言了
 
> es语言这种，不需要像`fr` `cn`那样，在web目录下面添加子文件夹
 

 
3.apphtml5的多语言配置和appfront类似，这里不做讲述
 
4.appserver多语言配置
 
![](images/qq63.png)
 
 
添加多语言即可
 
 
###添加其他语言

如果fecmall默认的语言不满足您的使用，您可以扩展其他的语言
 
![](images/qq66.png)
   
   
 到此，我们配置fecmall就完成了，恭喜您进阶。








