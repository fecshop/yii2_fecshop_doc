Fecshop Block 层
===============

> 因为block不是yii2结构中的一层，而是针对电商业务
的复杂性，fecshop加入的一层，而进行详细介绍。

### 1、介绍

block 是controller调用，然后返回数据给controller，
从而是controller代码高度简洁，一般就几行代码。大量的中间
逻辑转移到了block中处理，从而分工更加的细致。

### 2、使用

在controller中可以通过下面的方式使用。

```
$this->getBlock()->getLastData();
```

使用前，controller必须继承当前app的一个基层controller，
譬如appfront的controller都继承：
`use fecshop\app\appfront\modules\AppfrontController;`,

对于block文件，是文件名和路径对应的关系，
有点类似查找view文件，譬如：

fecshop\app\appfront\modules\Cms\controllers\ArticleController
下的方法

```
public function actionIndex()
{
	$data = $this->getBlock()->getLastData();
	return $this->render($this->action->id,$data);
}
```

` $this->getBlock()`返回的是`fecshop\app\appfront\modules\cms\block\article\Index`
的实例化对象。

### 3、作用：

block层的作用，在MVC四层的基础上面加入了新的一层
，可以避免controller层的雍容，层次比较清晰。
还可以按照需求，快速开发对block进行封装，
譬如appadmin就是把block进行了封装，可以快速的做
增删改查的功能。














