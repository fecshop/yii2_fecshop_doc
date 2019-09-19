Fecmall 为什么用mongodb做产品存储
=================================


### 前言

1.对于fecmall一版本，
产品数据默认存储在mongodb里面，为了降低门槛，
fecmall二版本实现了product mysql services，
默认存储在mysql数据库里面

2.用户可以使用默认的mysql存储产品数据，也可以切换成mongodb，如果
有技术能力，而且网站有一定的并发，建议使用mongodb

3.本文讲解的是，为什么使用mongodb存储产品数据


对于产品模块，是树形结构，因此在mysql中需要很多的表存储，然后在查询的时候，通过join联合查询得出来数据，作为一个通用商城，用户需要有可以自己在不修改数据库表结构（譬如mysql的表结构）的前提下给产品添加属性，因此，需要通过EAV的引入满足（magento就是引入EAV模型来解决的），这样就会有大量的join，magento的一个分类查询，需要join十几张表，在产品数据几万+的情况下，mysql join操作非常吃内存，并发高的时候性能非常的地下，如果，我想通过单表存储，又能满足我的复杂的查询，又能方便的添加产品属性（不需要修改表结构），又能快速查询，产品数据几万也不会 影响网站性能等等，引入mongodb数据库可以很好的解决这个问题。


先说一下原来的电商实现，mysql需要的表和面对的问题：（多语言的设计）
 
### 1.产品基本表：

1.1产品基本表：product_id 重量，sku，spu，库存，产品状态，上架状态，url_key（伪静态地址），价格，特价，特价开始时间，特价结束时间，成本价格，新产品开始时间，新产品结束时间，产品备注。等产品基本属性

### 2.下面的属性 因为是一对多，因为需要新建表，通过product_id来进行对应：

2.1产品图片表：product_id ， 图片类型（主图,小图，详细描述图），图片地址，图片描述，图片排序号等

2.2产品名字描述表：product_id，语言，名字name，描述description，meta_title，meta_keywords，meta_descrption等和语言有关的描述属性。

2.3产品批发价格表： 两个，三个，五个产品，进行价格优惠，譬如一个产品$10,两个产品的单价为$9.5 等
需要新建一张价格表。

2.4等等其他的一些join类型得标

###3.除了上面的表，我们还需要有一个属性组的概念

譬如衣服类属性组有颜色尺码字段，电视机电脑有型号字段，
也就是不同的产品属性组，有不同的属性，对于产品属性，对应到数据库的表结构，作为一款产品，不可能让用户在使用的过程中还需要手动给数据库加字段，这也是比较危险的操作，表结构是不能动的，因此，我们需要定义一个字段，用来存储这个属性组里面的N的属性，也就是把数组进行序列化serialize存储到一个字段中，也就是在上面的产品基本属性表添加两个字段，一个是属性组，一个是属性组对应的属性序列化数组。

### 4.到了这里我们来看我的功能要求：

4.1对于属性组里面的属性，我希望可以在分类侧栏对属性进行过滤，譬如上面属性组里面的颜色尺码过滤，由于mysql存储的序列化数组，因此无法排序和搜索


实现：当前mysql无法胜任（fecmall二版本 mysql存储产品，侧栏是没有属性过滤功能的）

4.2一个spu里面有多个sku，譬如一款鞋子是一个spu，不同的颜色尺码是不同的sku，在产品分类页面，一款鞋子只显示一次，也就是一款鞋子选一个sku作为代表显示出来，其他的在分类页面不显示

但是，如果用户在分类页面对产品进行了属性过滤，那么就要出现相应属性对应的sku，譬如用户在分类页面对产品进行搜索颜色红色，对于spu应该显示出来红色的衣服sku，而不是其他颜色的sku。
同时，还要满足分页，排序，其他的属性组合过滤等

实现：mysql
进行了实现， 但是效果没有mongodb好

4.3在产品详细页面，进入sku后，需要把这款产品的其他的sku也显示出来，如下：

![](https://ooo.0o0.ooo/2017/06/24/594df9940b8c2.png)


实现：当前mysql可以满足并实现

4.4产品属性组，用户可以随意定义，用户可以添加新的属性组，然后设置相应的产品。

实现：当前mysql可以满足并实现

4.5对于上面的设计，是一个sku是一行产品的设计，一个产品如果有6个颜色，6个尺码，那么就会有36个组合，维护起来，需要另外做一个单独的产品来维护，然后进行批量同步，比较费劲，有的用户可能希望一个spu是一行数据，而不是一个sku是一行数据。

对于fecshop，也进行了实现：

![](https://ooo.0o0.ooo/2017/06/24/594dfad02808a.png)

这种方式如果用mysql来做，需要新建一个表进行存储。

按照mysql的方式，上面的4.1 4.2 需要借助搜索引擎来实现，譬如ElasticSearch等，需要把数据复制到es里面，复制数据就要考虑数据同步出现问题的处理，这个就需要多种机制核验，当然，一个比较方便的方法是用MQ，通过消息应答机制来处理，总之进一步增加复杂性，（es是搜索引擎，不是数据库，Es在同步数据后，需要一秒左右的时间才能刷新信息）。

### 5.搜索功能

mysql使用的是`like`搜索,

而对于搜索分词库这些, mysql是无法完成的，对于外文网站，mongodb支持很多语言的（中文不支持）。

###总之

mysql是不能单独胜任电商的所有要求，需要和搜素引擎一起来完成要求。

fecmall用mongodb是一种比较折中的方案：

大家的站一般都是小站，很少有破百万IP的网站，用fecshop的方案，足以支撑起来一个中型网站（几十万ip，几十万产品）

1.mongodb是nosql数据库，存储结构类似于php的多维数组，因此产品数据可以一张表搞定。

2.对于产品库存表，现在已经抽出来放到mysql中，这样后，产品数据就是  一个产品mongodb表+两个产品库存表（因为有淘宝和京东模式，淘宝模式就是上面说的一个spu一行数据）。单表搞定，查询的时候不需要多表join。

3.对于属性组的实现，因为mongo是没有表结构的，因此，可以通过程序对象来控制表结构，这样，表的属性组和属性的添加就很好弄，直接增加一个属性存储就行，就像在数组中增加一个key类似。

4.对于上面的分类spu的显示，以及属性的过滤都可以满足，而且mongodb支持分词搜索，有分词库，可以满足搜索功能。

因此，对于mongodb，不需要elasticSearch，就可以满足所有的项目需求，mongodb在高并发方面的性能也比较优秀，
水平扩展非常的容易，缺点就是不支持多表事务，这对于目前没有太多影响，因为产品表里面涉及到多表事务的就是销售库存，没有其他的了，因此，在这个方面是满足要求的。

当然，mongodb也有自身的缺点，没有表结构，会感觉不够严谨，只要代码撸好，我认为问题不大。
用mongodb做产品库，我是有线上项目的，而且跑了2年了，当然，更多的场景还需要验证。



另外，对于多表事务比较频繁的表，譬如cart order coupon表，都是用的mysql表。

mongodb，我认为并没有增加学习成本，Yii2连的Active Record使用起来还是很方便，
这种方式我认为是一种比较折中的方式，路子有点野，但是有效地吧（就我的经验是这样的，不同观点发表出来学习一下）。

另外，fecshop的设计，有一层services层，有的部分是可以切换数据库的（只是某些部分进行了实现，不是全部，实现这个是为了一点学术的味道）。

譬如：https://github.com/fecshop/yii2_fecshop/blob/master/services/cms/Article.php

```
class Article extends Service
{
    public $storage = 'mongodb';
    protected $_article;
    public function init()
    {
        if ($this->storage == 'mongodb') {
            $this->_article = new ArticleMongodb();
        } elseif ($this->storage == 'mysqldb') {
            $this->_article = new ArticleMysqldb();
        }
    }
```

通过配置 $storage 可以设置使用哪种数据库（$storage是在配置文件里面，service里面的public 属性都是可以通过配置注入的。）

mongodb和mysql实现的service 通过接口做约定：https://github.com/fecshop/yii2_fecshop/blob/master/services/cms/article/ArticleInterface.php



mongodb是文档型数据库，单行数据最大的size好像是16MB，我有点忘记了，对于产品，一行数据
是很小的存储量，也就是几十kB，只要查询索引做好，不会引起性能问题。

mongodb在高并发方面，比mysql强很多的，这是nosql型数据库的优势所在

fecmall目前的中文搜索应的是xunsearch，Elasticsearch对硬件要求高一些，xunsearch小巧一些，不过，如果高并发搜索，还是要用elasticSearch。目前fecshop没有做elasticSearch搜索，后面有时间会做上去，elasticSearch也需要安装一个中文插件才可以做中文搜索的。

mongodb的功能不仅仅这些，mongodb我玩了3年左右了，还可以做统计的，

mongodb mapreduce功能，详情参看：http://www.cnblogs.com/loogn/archive/2012/02/09/2344054.html

mongodb aggregate聚合管道：http://www.runoob.com/mongodb/mongodb-aggregate.html



库存是需要多表事务操作的，放到mongodb中不合适

这个fecmall已经想到并处理了，库存是放到mysql的表 `product_custom_option_qty` 和 `product_flat_qty` 中了
