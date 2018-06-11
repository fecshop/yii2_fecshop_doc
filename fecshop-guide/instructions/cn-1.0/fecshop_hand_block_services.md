Fecshop 关于block和services
===========================

> 对于MVC，这个基本程序员都知道，这个不需要多说，而对于fecshop的block和services
有不少童鞋疑惑，这两个层是干嘛的，下面细致讲解



对于MVC，这个都了解，controller，view也就是theme部分，model，这个不用多说

为了更好的管理，我们会模块化，也就是用module，yii2也支持module

电商系统比较复杂，我们会将各个功能模块化，譬如:购物车模块，订单模块，产品模块，搜索模块，用户模块等等
，每个模块由自己独立的mc结构，当然，model是独立出来的

在功能执行的过程中会发现，很多操作都是需要很多model执行，譬如，生成订单，需要订单部分的model生成订单数据，购物车model清空购物车，优惠券model部分更新优惠券使用情况，产品model部分扣库存，等等

如果我们在模块里面写这些调用逻辑，显然是不合适的，我们写到模块的controller里面显然不合适

如果我们将这些逻辑写到model里面，那么生成订单，就会涉及到各个model相互的调用，譬如，生成订单部分，如果我在order model写这个函数，就会涉及到调用其他的很多model的方法，这种方式不利于解耦，而且还会混乱，多个model相互交互，不知道写到那个model里面最合适

因此，我们需要在model上面架设一层，也就是services层，model层的最小的粒度是针对表数据的增删改查，
而services是我们用语言描述一个行为的最小粒度，譬如将一个产品加入购物车，生成一个订单，上架一个产品等等，这些会在相应的services里面存在一个方法

fecshop services的实现，类似于Yii2 component组件，加入services层由很多的好处：

1.services是基于单例模式的对象，通过Yii2的依赖注入的方式生成，很多参数可以以配置注入到对象中

2.懒加载模式，只有用到才会生成对象，节省资源

3.有利于后面重构，目前业务满足的实现，在将来未必满足，譬如，现在的购物车基于mysql实现，如果将来我想把购物车改成redis实现，有了services层，就很方便，我只需要将cart services里面的方法全部实现就可以了，因此，就容易的，譬如官网开发的redis cart：https://github.com/fecshop/yii2_fecshop_redis_cart
，安装这个插件，更改配置，轻松切换

4.多种业务方式实现，譬如fecshop的搜索，中文使用的是xunsearch，外文使用的是mongodb，
当然，官网也有elasticSearch搜索扩展：https://github.com/fecshop/yii2_fecshop_elasticsearch

5.减少代码冗余，fecshop是多入口的电商类型，各个入口有自己的独立的东西，但是services层是公用的，这样各个层调用services提供的底层方法满足自己的需要，而不会将系统搞的乱糟糟

6.对于Restful Api给我们的思想是，将url看成资源，同样，对于fecshop services，目前是基于数据库的实现，将来你可以根据自己的业务，services里面不在是调用的model，而是内网的api，而且，你可以保留原来的实现，搞一个新的services实现，然后将配置切换过去即可，当然，你还可以切换回来

7.更加灵活的配置，因为services是通过yii2的依赖注入容器生成的，因此，对于services class里面的每个public方法，都可以在配置中加入参数注入进去，更改配置，你还可以像yii2 组件一样，通过注入不同的配置生成多个services对象

8.services使用的是基类Yii，譬如使用cart services的语法为 `Yii::$service->cart`,而不需要
使用use引入，因此，可以在任何地方使用，甚至在view文件里面，方便灵活

上面说了services，下面说一下block

1.services的基层调用函数写好后，controller调用services进行组装，由于controler里面有很多action方法，会造成controler里面的代码过多，因此，一个action方法对应一个block文件，会更有利于维护

2.block调用services的方法，进行数据组装和处理，最后生成数据，返回给controller。

3.对于有一些功能块，我们想在很多地方调用，这些块也是有 数据提供层 和 数据展示view组成，
譬如网站的头部 尾部，菜单等等，甚至产品的价格部分，也即是fecshop的小部件：http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_widget.html

block在fecshop小部件中作为数据提供层，详细的实现，您可以去看模板中的header，footer部分的实现

通过上面的说明，可以很清楚的了解services作为底层功能提供层，而block调用services的函数，进一步进行数据的处理，为view部分提供显示数据。

block层不能调用model层，只能调用services层，然后services层调用model

大致的调用结构为 

fecshop入口index.php  --->  fecshop初始化  -->  模块  --> controller -->  block --> services --> model,

然后数据返回 model -->  service --> block  --> controller ,然后controller将数据传递给view部分（theme）

view content部分，又分为多个子view，以fecshop小部件的形式被调用，最后画出来整个页面

















































