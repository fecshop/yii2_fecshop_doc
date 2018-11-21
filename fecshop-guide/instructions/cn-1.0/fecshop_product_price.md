Fecshop 产品价格
===========

> fecshop的产品价格的介绍


### 产品价格概念

![x](images/pp_1.jpg)

`Cost Price`: 产品的成本价格，在fecshop系统中，这个字段只是一个记录，没有相关的功能，记录产品采购的价格

`Sale Price`: 产品的销售价格，在前端显示的产品价格price

`Special Price`: 产品的销售特价，在销售特价有效的时候，产品的`Sale Price`将会无效，以`Special Price`作为产品的价格

`Special Begin`，`Special End`:产品的销售特价开始时间，和产品的销售特价开始时间，
`当前时间`>= `Special Begin`  &&  `当前时间` < `Special End` 的时候
，`Special Price`才会有效，如果`Special Begin`不填写则代表0，
如果`Special End`不填写，则代表无穷大，因此，这两个值都不填写，
代表`Special Price`一直有效


`Tier Price`: 产品的批发价格，譬如产品的价格为10美元，购买2个为9.5美元，购买5个为9美元，
买的越多，产品的单价越低

`Custom Option Price`：淘宝模式custom option各个选项的价格，需要注意的是，
这个并不是这个选项的价格，而是在产品计算出来的价格基础上进行累加或者累减，
譬如产品的计算价格是10美元，`Custom Option Price`为1美元，那么产品的价格为11美元

`Final Price`: 产品计算的最终价格，该字段是为了在分类和搜索页面侧栏产品价格过滤，以及
按照价格排序，该字段是由console计算出来更新到产品的final_price字段，
该脚本一般一天跑一次，关于该脚本详细参看：[Product Final Price:计算最终价格的脚本](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-console-product-final-price.html)
, 需要注意的是，该属性仅仅用于过滤和排序，而不能使用该字段作为产品价格计算，
因为排序和过滤存在一定的误差并不会有影响（脚本计算的价格后，当产品价格更新后，
`Final Price`的值并没有更新，只有在下次中间脚本计算后才会更新）

### 产品最终价格计算

产品的价格计算是product price services处理的：[product price services](https://github.com/fecshop/yii2_fecshop/blob/master/services/product/Price.php)

1.初始值：产品的价格 = `Sale Price`

2.如果`Special Price`有效，则产品的价格 = `Special Price`， 第1步得到的值失效

3.如果存在`Tier Price`，那么用户购买多个产品满足条件，那么加入购物车的产品的价格=
相应的`Tier Price`的值，第2步得到的值失效

4.如果产品是淘宝模式的产品，存在`Custom Option Price`，
如果 `Custom Option Price` != 0, 那么
产品的价格 = 第2步得到的产品价格 + `Custom Option Price`，
`Custom Option Price`可以为负数，相当于在上面减价

然后，在根据汇率，得到当前汇率下的产品的价格，
详细参看：[product price services](https://github.com/fecshop/yii2_fecshop/blob/master/services/product/Price.php)











