Fecshop 如何重写block和models
========================

很多人做fecshop 的 block的重写二开功能，会出现一些`namespace`的问题。

参考文档：[fecshop重写block的文档](http://www.fecshop.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-rewrite-func.html#8rewritemapblock-model)

文档中写的配置文件是`@common/config/YiiRewriteMap.php`,如果您修改model，而且是全局的话，建议在这个文件里面，如果不是全局的，可以在相应的入口的配置文件，譬如pc端的`@appfront/config/YiiRewriteMap.php`

如果重写block，因为block是根据入口区分的，因此，写到相应的入口中，譬如`appfront`


下面就详细写一个重写apphtml5首页的例子：

重写的block文件为:`@fecshop\app\apphtml5\modules\Cms\block\home\Index.php`

1.打开配置文件@apphtml5/config/YiiRewriteMap.php

在return数组中加入：
```
[
	
	'\fecshop\app\apphtml5\modules\Cms\block\home\Index' => '\apphtml5\local\local_modules\Cms\block\home\Index',
]

```

2.创建文件@apphtml5\local\local_modules\Cms\block\home\Index.php

![](https://i.loli.net/2018/06/28/5b349cf1b6c7a.png)


代码如下：

```
<?php
/*
 * 
 */

namespace apphtml5\local\local_modules\Cms\block\home;

use Yii;

class Index extends \fecshop\app\apphtml5\modules\Cms\block\home\Index
{
    public function getLastData()
    {
        echo 1;
        $this->initHead();
        // change current layout File.
        //Yii::$service->page->theme->layoutFile = 'home.php';
        return [
            //'bestSellerProducts' => $this->getBestSellerProduct(),
            'bestFeaturedProducts'     => $this->getFeaturedProduct(),
            'currency'            => Yii::$service->page->currency->getCurrencyInfo(),
            'currencys'            => Yii::$service->page->currency->getCurrencys(),
            'currentStore'        => Yii::$service->store->currentStore,
            'stores'            => Yii::$service->store->getStoresLang(),
            'currentBaseUrl'    => Yii::$service->url->getCurrentBaseUrl(),
        ];
        
    }
    
}

```


然后访问apphtml5端，在页面左上角如果打印出来一个数字 `1`,就代表重写成功了

这个很简单，就是一个配置加一个文件，你的文件的路径尽量和fecshop的文件路径对应好，方便维护。


models重写，和block重写类似，参考一下可以自己写

最后，好多童鞋遇到namespaceing的问题，出现这些问题，找不到文件或者namespace问题等，
注意去看`字母大小写`和`空格`问题，以及``下划线等细节，`s`字母缺失等问题
。










































