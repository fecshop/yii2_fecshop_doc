Fecshop 独立功能块
==================

> 也就是通过block和view文件组合起来的独立块，block提供数据
view文件负责html的组织显示，共同完成某个区块，可以通过
配置的方式，将独立块加入到各个页面中，譬如网站侧栏的一些区块，
会在很多页面中显示。

### 1. 结构：

block是数据提供者，view是数据显示者，当然，如果当前
的独立功能块不需要block提供数据，那么在配置中
可以不添加block。

### 2. 使用：

对于Fecshop 独立功能块，是通过page服务的子服务widget实现的，
可以点击这里查看具体的原理：
[Fecshop widget服务](fecshop-services-page.md#8page-widget)

### 3. 作用：

当把一个独立功能块制作好后，也就是在`Yii::$service->page->widget`
中配置好，然后显现了相应的block和view文件，那么这个独立
功能块就完成了，可以方便的通过服务一行代码
调用这个独立功能块。









