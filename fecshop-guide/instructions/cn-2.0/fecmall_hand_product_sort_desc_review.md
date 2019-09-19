Fecmall 按照产品评论数倒序分页取产品的详细代码
===================================



按照评论数排序取产品

思路：

1.产品model：https://github.com/fecshop/yii2_fecshop/blob/master/models/mongodb/Product.php

可以看到字段：

```
'review_count',                  //评论总数
'reviw_rate_star_average_lang',  //（语言）评论平均评分
'review_count_lang',             //（语言）评论总数
```

2.产品表（mongodb）product_plat,如果产品被评论就会出现字段


```
"review_count": NumberInt(2),   // 产品总评论数
   "reviw_rate_star_average_lang": {
     "reviw_rate_star_average_lang_en": 5 
  },
   "review_count_lang": {  // 产品在各个语言下的评论数
     "review_count_lang_en": NumberInt(2)   // 英语store下的评论数
  },
```

因此，如果可以按照 `review_count` 取产品数据

product service：https://github.com/fecshop/yii2_fecshop/blob/master/services/product/ProductMongodb.php

可以看到如何查询的方法：

```
/*
     * example filter:
     * [
     * 		'numPerPage' 	=> 20,
     * 		'pageNum'		=> 1,
     * 		'orderBy'	=> ['_id' => SORT_DESC, 'sku' => SORT_ASC ],
     * 		'where'			=> [
                ['>','price',1],
                ['<=','price',10]
     * 			['sku' => 'uk10001'],
     * 		],
     * 	'asArray' => true,
     * ]
     */
    public function coll($filter = '')
    {
        $query = $this->_productModel->find();
        $query = Yii::$service->helper->ar->getCollByFilter($query, $filter);
        return [
            'coll' => $query->all(),
            'count'=> $query->limit(null)->offset(null)->count(),
        ];
    }
```



实现：评论总数（不区分语言store）倒序分页查询产品
```
$enableStatus = Yii::$service->product->getEnableStatus();
$filter = [
	'numPerPage' 	=> 20,
	'pageNum'		=> 1,
	'orderBy'	=> ['review_count' => SORT_DESC ],
	'where'			=> [
		['status' => $enableStatus]

	],
	'asArray' => true,

]

$data = Yii::$service->product->coll($filter);
$coll = $data['coll'];   // 当前页的数据
$count = $data['count'];  // 产品总数，用于分页
```

最后，关于产品评论，参看帮助文档：[Fecmall 产品评论](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_product_review.html)
















