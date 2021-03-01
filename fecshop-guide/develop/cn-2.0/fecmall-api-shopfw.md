Fecmall ShopFw采集工具api说明
==============================

> fecmall和shopfw采集工具对接的说明


### Api数据格式说明 - 准备部分

关于多语言说明，详细参看api文档: [Fecmall Api 多语言](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-api-mutil-lang.html)



1.获取语言的api

获取fecmall网站有多少种需要翻译的语言

详细参看api文档: [Fecmall Api 获取多语言List](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-api-mutil-lang-list.html)

2.获取分类的api


获取fecmall网站所有的enable的分类

详细参看Api: [Fecshop Api 分类 List](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-api-category.html)

3.属性和属性组


对产品属性组和属性的获取，添加，修改，删除 操作。

[Fecmall Api 产品属性 List](fecmall-api-attr-list.md)

[Fecmall Api 产品属性 FetchOne](fecmall-api-product-attr-fetchone.md)

[Fecmall Api 产品属性 AddOne](fecmall-api-attr-add.md)

[Fecmall Api 产品属性 UpdateOne](fecmall-api-attr-update.md)

[Fecmall Api 产品属性 DeleteOne](fecmall-api-attr-delete.md)

[Fecmall Api 产品属性组 List](fecmall-api-attr-group-list.md)

[Fecmall Api 产品属性组 FetchOne](fecmall-api-product-attr-group-fetchone.md)

[Fecmall Api 产品属性组 AddOne](fecmall-api-attr-group-add.md)

[Fecmall Api 产品属性组 UpdateOne](fecmall-api-attr-group-update.md)

[Fecmall Api 产品属性组 DeleteOne](fecmall-api-attr-group-delete.md)

### Api数据格式说明 - 产品数据新增部分

a) 在产品数据传递之前，shopfw需要先获取语言api数据，来决定翻译多少种语言，

b) 获取fecmall的所有分类，shopfw进而可以建立fecmall的分类树，将采集的产品进行做对应

c) 新建和更新属性，属性组，如果当前属性组和属性，无法满足当前商品要求，就需要对属性组进行修改。


准备api对接完成，就可以进行产品数据的传递了，产品数据传递需要注意的是：

a) shopfw每次新增产品之前，都会通过外部编码`third_refer_code`进行查询，如果fecmal存在产品则不会新增

b) 新增的产品，spu和sku由fecmall生成，shopfw不做记录，而且每次新增，fecmall不做数据存在检查，而是由shopfw控制，
因此每次新增之前，shopfw都会通过过外部编码`third_refer_code`进行查询一次。


下面是新增产品数据的详细api：


1.通过外部编码进行查询产品


传递数据：外部编码`third_refer_code`

返回数据：外部编码对应的产品数组。


通过该api，shopfw来判断，是否已经存在产品，如果已经存在，则不会新增。

如果不存在，则可进行新增产品操作。


详细参看api: [Fecmall Api 产品 List](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-api-product.html)

2.传递图片的api

进行新增产品，先将图片传递过去，api每次只能传递一个图片，因此需要多次循环，将
产品所有的规格sku对应的图片都传递过去。

传递图片格式

```
[
{"imgCode" =>  '11.jpg', 'base64' => 'fdasfadsfadsfsdf..............'}, 
{"imgCode" =>  '22.jpg', 'base64' => 'f3232asfads32df..............'}, 
{"imgCode" =>  '33.jpg', 'base64' => 'f32fdfadsfd32asfads32df..............'}, 
]
```


接收api，返回格式：

```
[
{"imgCode" =>  '11.jpg', 'filePath' => '/1/2/343434.jpg'}, 
{"imgCode" =>  '22.jpg', 'filePath' => '/1/2/343434.jpg'}, 
{"imgCode" =>  '33.jpg', 'filePath' => '/1/2/343434.jpg'}, 
]
```

详细参看文档：[Fecmall Api 产品图片同步](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-api-product-image-sync.html)

3.新增商品api

3.1新增的api中，没有spu和sku，需要fecmall自己生成

3.2产品图片，是保存后的文件路径

3.3产品分类，由shopfw 传递的数据携带，fecmall这边直接插入即可

3.4产品表新增字段：  外部编码，外部url来源，货号。将外部编码  货号做索引

详细参看文档：[Fecmall Api ShopFw-产品新增](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-api-shopfw-product-add.html)

### Api数据格式说明 - 产品数据更新部分


目前只会更新库存和价格部分，其他的不做更新

更新的具体逻辑为：

shopfw先通过`货号`或者`外部编码`进行查询，得到对应的产品数据列表，
然后将采集到的产品数据，通过规格属性（譬如颜色尺码等）进行对应，然后返回数据：
[ {"sku":"xxxx",  "price":34.45, "qty": 33}, {"sku":"yyyy",  "price":134.45, "qty": 133}]

详细参看文档： [Fecmall Api ShopFw-产品更新库存和价格](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-api-shopfw-product-update-stock-and-price.html)























