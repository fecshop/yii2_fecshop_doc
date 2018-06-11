Fecshop 重量计算是否加入体积重，如何计算的
==================


> fecshop的产品除了实际重量，还有体积重，您在编辑产品
的时候，编辑产品的`长,宽,高`数据即可计算出来体积重

```
产品的重量 = max(产品的体积重，产品的实际重)
```


fecshop体积重 = 长(cm) * 宽(cm) * 高(cm) / 体积重系数 

体积重系数：默认使用`新体积重系数` ， 5000 , 当然，你可以在shipping services config的配置中设置该系数，配置变量为：
`volumeWeightCoefficient`

```
DHL，UPS更改体积重计算标准。

DHL与UPS快件由2009年2月1日起，体积重的计算标准由6000改为5000，具体如下：

如体积尺寸：100cm x 100cm x 100cm的快件。

旧体积重计算： 100x100x100/6000=166.67KG 计费重量167KG。

新体积重计算： 100x100x100/5000=200KG 计费重量200KG。
```


详细代码查看：https://github.com/fecshop/yii2_fecshop/blob/master/services/Shipping.php






