Fecshop Admin 二次开发
=========================

> 关于该入口的描述和说明


### Appadmin 介绍

如果您想扩展后台，建立自己的module，是可以的

首先，需要新建module，这里有一个appfront入口的
新建module的例子，注意，不是appadmin，这个例子只是讲述如何
创建一个模块的步骤

[http://www.fecshop.com/topic/451](http://www.fecshop.com/topic/451)

对于后台，您先做一个新的增删改查，可以参看一下fecshop的cms page部分

1.controller文件：fecshop\app\appadmin\modules\Cms\controllers\ArticleController.php

对于：

```
// 网站信息管理
public function actionIndex()
{
    $data = $this->getBlock()->getLastData();

    return $this->render($this->action->id, $data);
}
```

`$this->getBlock()`:这个是得到Block的方法，具体实现您可以看到继承的积累中的实现，
具体的是按照相应文件名对应的方式，譬如这里对应的block文件是：

`fecshop\app\appfront\modules\Cms\block\article\Index.php`

通过这个方法得到数据，然后传递给view

2.增删改查

为了快速的增删改查，fecshop appadmin进行了一系列的封装，譬如：对于列表，您可以查看：

`fecshop\app\appfront\modules\Cms\block\article\Index.php`

`public function getSearchArr()` : 用来做搜索部分的函数

`public function getTableFieldArr()` ： 用来做列表部分的函数

`$this->_editUrl` :  编辑url

`$this->_deleteUrl` : 删除url

`$this->_service` : 数据获取源serviews

通过设置这几个函数就可以快速的出来一个可以搜索查询，分页，控制显示个数，排序等功能的table list。


对于编辑部分，这里不做详细的阐述，详细您可以自己看代码实现。

上面封装有一点重，在block加入了html部分，这个也是为了快速实现，您可以根据自己的情况进行
其他方式的封装，这个看自己的情况，封装是为了快速开发，因此要看自己的具体业务而定。



