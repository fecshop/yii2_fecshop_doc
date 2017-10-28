fecshop api
===========

> fecshop api这个入口的定位是和第三方系统对接的api部分，譬如和ERP，
> 进行订单传递和产品刊登等，以及erp把订单的物流状态传递个fecshop网站
> 等等


### api配置：

配置文件为：`@fecshop/app/appapi/config/appapi.php`

里面就是api的url定义

您只要了解yii2 的restful机制，自己看源码，很容易看懂

api这个部分目前功能很少，而且没有写相应文档，因为这个部分是和
第三方对接的，因此，定制性比较强，fecshop所做的就是
做好框架，可以让开发者很方便的使用这个入口。













