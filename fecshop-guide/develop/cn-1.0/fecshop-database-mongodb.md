Fecshop Mongodb数据库介绍
=========================

> Fecshop Mongodb数据库的介绍部分


### Fecshop Mongodb数据库


1.article表


```
 {
   "_id": ObjectId("5a17f1b3bfb7ae261d64e956"),
   "created_at": NumberInt(1511518643),  // 创建时间戳
   "created_user_id": NumberInt(1),     // 后台创建用户id
   "updated_at": NumberInt(1512354840), // 更新时间戳
   "url_key": "/about-us-39654914",  // url key,也就是在前端显示的自定义urlkey
   "title": {       // page的标题，下面是各个语言对应的值，
     "title_en": "about us",
     "title_fr": "",
     "title_de": "",
     "title_es": "",
     "title_ru": "",
     "title_pt": "",
     "title_zh": "关于我们"
  },
   "meta_keywords": {  // page的meta信息
     "meta_keywords_en": "about us",
     "meta_keywords_fr": "",
     "meta_keywords_de": "",
     "meta_keywords_es": "",
     "meta_keywords_ru": "",
     "meta_keywords_pt": "",
     "meta_keywords_zh": ""
  },
   "meta_description": { // page的meta信息
     "meta_description_en": "",
     "meta_description_fr": "",
     "meta_description_de": "",
     "meta_description_es": "",
     "meta_description_ru": "",
     "meta_description_pt": "",
     "meta_description_zh": ""
  },
   "content": {  // page的内容
     "content_en": "<p><span id=\"result_box\" lang=\"en\"><span title=\"Fecshop 全称为Fancy ECommerce Shop，是基于php Yii2框架之上开发的一款优秀的开源电商系统， 遵循OSL3.0开源协议，Fecshop支持多语言，多货币，架构上支持pc，手 [...]",
     "content_fr": "<span id=\"result_box\" lang=\"fr\"><span title=\"Fecshop 全称为Fancy ECommerce Shop，是基于php Yii2框架之上开发的一款优秀的开源电商系统， 遵循OSL3.0开源协议，Fecshop支持多语言，多货币，架构上支持pc，手机we [...]",
     "content_de": "",
     "content_es": "",
     "content_ru": "",
     "content_pt": "",
     "content_zh": "Fecshop 全称为Fancy ECommerce Shop，是基于php Yii2框架之上开发的一款优秀的开源电商系统，遵循OSL3.0开源协议，Fecshop支持多语言，多货币，架构上支持pc，手机web，手机app，和erp对接等入口，您可以免费快速的定制和部署属于您的电商系统。预计到201 [...]"
  },
   "status": NumberInt(1)  // page的状态，1代表激活，2代表关闭
}	

```

2.category

> 分类表


```
 {
   "_id": ObjectId("5a1b673ebfb7ae44c26734f2"),
   "created_at": NumberInt(1511745342),
   "created_user_id": NumberInt(1),
   "level": NumberInt(1),   // 菜单的级别，一级菜单是1，二级菜单是2，...
   "updated_at": NumberInt(1511745342),
   "parent_id": "0",   // 分类的父分类id，如果是`0`,则代表是一级分类
   "name": {           // 分类的名字，下面是各个语言对应的名字
     "name_en": "Wedding2222",
     "name_fr": "",
     "name_de": "",
     "name_es": "",
     "name_ru": "",
     "name_pt": "",
     "name_zh": "婚礼"
  },
   "status": NumberInt(1), // 分类的状态
   "menu_show": NumberInt(1),  // 分类是否在前端菜单中显示，1代表显示，2代表不显示，不显示并不代表关闭状态，通过url还是可以访问的
   "url_key": "/wedding-46851137",  // 分类自定义urlkey
   "filter_product_attr_selected": "style,dresses-length,pattern-type,sleeve-length,collar,color",  // 分类侧栏属性过滤添加的属性
   "filter_product_attr_unselected": "",  // 分类侧栏属性过滤去除的属性
   "description": {  // 分类的描述
     "description_en": "",
     "description_fr": "",
     "description_de": "",
     "description_es": "",
     "description_ru": "",
     "description_pt": "",
     "description_zh": ""
  },
   "menu_custom": {  // 分类自定义html
     "menu_custom_en": "<a href=\"//fecshop.appfront.fancyecommerce.com/wedding\"><img alt=\"\" src=\"//img.fancyecommerce.com/custom/menu/what_a.jpg\" width=\"244\" /></a><a style=\" [...]",
     "menu_custom_fr": "<a href=\"//fecshop.appfront.fancyecommerce.com/fr/wedding\"><img alt=\"\" src=\"//img.fancyecommerce.com/custom/menu/what_a.jpg\" width=\"244\" /></a><a styl [...]",
     "menu_custom_de": "",
     "menu_custom_es": "",
     "menu_custom_ru": "",
     "menu_custom_pt": "",
     "menu_custom_zh": ""
  },
   "title": {  // 分类标题
     "title_en": "Wedding",
     "title_fr": "",
     "title_de": "",
     "title_es": "",
     "title_ru": "",
     "title_pt": "",
     "title_zh": ""
  },
   "meta_description": {  // 分类meta 信息
     "meta_description_en": "",
     "meta_description_fr": "",
     "meta_description_de": "",
     "meta_description_es": "",
     "meta_description_ru": "",
     "meta_description_pt": "",
     "meta_description_zh": ""
  },
   "meta_keywords": {  // 分类 meta 信息
     "meta_keywords_en": "",
     "meta_keywords_fr": "",
     "meta_keywords_de": "",
     "meta_keywords_es": "",
     "meta_keywords_ru": "",
     "meta_keywords_pt": "",
     "meta_keywords_zh": ""
  }
}	

```



表：error_handler_log

> 通过Yii2的errorHandle机制，将所有出现错误信息，保存到表中（生产环境）

```
 {
   "_id": ObjectId("5a34d9d2bfb7ae0ec26cc9e3"),
   "category": "appapi",  // 入口名称。
   "code": NumberInt(404),  // http status ，http状态码
   "message": "Page not found.",  // 错误信息
   "file": "/www/web/develop/fecshop/vendor/yiisoft/yii2/web/Application.php",  // 错误文件
   "line": NumberInt(114),  // 文件所在的行（改行代码执行导致的错误）
   "created_at": NumberInt(1513413074),
   "ip": "106.11.225.134",  // 访问者的id
   "name": "Not Found",    // 错误名称
   "url": "//fecshop.appapi.fancyecommerce.com/",  // 访问的url
   "request_info": {  // request 信息
     "ajax": NumberInt(0),
     "request_type": "get",
     "request_data": [
      
    ],
     "headers_data": {  // header信息。
       "accept-encoding": [
         "gzip"
      ],
       "user-agent": [
         "Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Version/9.0 Mobile/13B143 Safari/601.1"
      ],
       "cache-control": [
         "no-cache"
      ],
       "pragma": [
         "no-cache"
      ],
       "host": [
         "fecshop.appapi.fancyecommerce.com"
      ],
       "accept": [
         "text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2"
      ],
       "connection": [
         "keep-alive"
      ]
    },
     "userHost": null,
     "userIP": "106.11.225.134"
  },
  // 错误追踪信息
   "trace_string": "#0 /www/web/develop/fecshop/vendor/yiisoft/yii2/base/Application.php(380): yii\\web\\Application->handleRequest(Object(yii\\web\\Request))\n#1 /www/web/dev [...]"
}	

```




表：Favorite

> 产品收藏信息表

```
 {
   "_id": ObjectId("5a31e3cabfb7ae29c040a042"),
   "product_id": "580835d0f656f240742f0b7c",
   "user_id": NumberInt(383),                   // customer表的id
   "created_at": NumberInt(1513219018),
   "updated_at": NumberInt(1513219018),
   "store": "fecshop.appfront.fancyecommerce.com/cn"  // store的key
}	

```

表：fecshop_service_log  废弃


表：log_product_view    废弃


表：migration，mongodb表的Yii2 migration信息。也就是安装fecshop，以及
升级fecshop数据库部分的信息


表：newsletter

> 订阅邮件

```
 {
   "_id": ObjectId("5a31e0bfbfb7ae332a4228f3"),
   "email": "logig618@gmail.com",
   "created_at": NumberInt(1513218239),
   "status": NumberInt(1)
}	

```

表：review 

> 产品评论

```
	
{
   "_id": ObjectId("5a3083bbbfb7ae0f2760d422"),
   "product_spu": "p10001",
   "product_id": "580835d0f656f240742f0b7c",
   "rate_star": "5",
   "name": "44444 666",
   "user_id": NumberInt(46),
   "ip": "113.116.126.150",
   "summary": "99999999999",
   "review_content": "99999999999999999999999",
   "review_date": NumberInt(1513128891),
   "store": "fecshop.apphtml5.fancyecommerce.com",
   "lang_code": "en",    // 语言
   "status": NumberInt(1),  // 评论审核状态 ，10是默认状态，1是审核通过，2是审核拒绝状态
   "audit_user": NumberInt(2),  // 评论后台审核人
   "audit_date": NumberInt(1513129505)  // 评论后台审核日志
}	

```

表：static_block 

> static block 部分，和mysql的 static_block 类似


表：url_rewrite

> url重写存储部分，和mysql的url_rewrite类似

表：product_flat

> 产品信息表，产品表的库存放到了mysql中，其他的信息都在这张表中

```
 {
   "_id": ObjectId("5a1c2ae6bfb7ae0ee472ae15"),
   "created_at": NumberInt(1511795430),
   "created_user_id": NumberInt(1),
   "updated_at": NumberInt(1511795430),
   "name": {  // 产品名称
     "name_en": "test computer",
     "name_fr": "",
     "name_de": "",
     "name_es": "",
     "name_ru": "",
     "name_pt": "",
     "name_zh": "测试计算机"
  },
   "spu": "computer001",
   "sku": "computer001-xinghao1-cpu36",
   "weight": 0.3,  // 产品重量 
   "score": NumberInt(0), // 产品的评分，这个可以通过销量值填写进去
   "status": NumberInt(1), // 产品的状态，1代表激活，2代表下架
   "qty": NumberInt(334),  // 产品的库存，这个字段已经无效，库存在mysql中
   "min_sales_qty": NumberInt(0),  // 产品的最小销售个数
   "is_in_stock": NumberInt(1),  // 产品 的库存状态，1代表有库存，2代表无库存
   "category": [  // 产品的分类id。可以多个
     "57beb586f656f275313bf57a"
  ],
   "price": 33,  // 产品的销售价格
   "cost_price": 10, // 产品的成本价格
   "tier_price": [ // 产品批发价格
     {
       "qty": NumberInt(2),
       "price": NumberInt(30)
    },
     {
       "qty": NumberInt(4),
       "price": NumberInt(28)
    }
  ],
   "final_price": 33,  // 产品最终价格（这个值是通过脚本批量计算得来，仅仅作为分类搜索页面价格的排序和过滤）
   "meta_keywords": {  // 产品meta信息
     "meta_keywords_en": "sex xx meta keywords",
     "meta_keywords_fr": "",
     "meta_keywords_de": "",
     "meta_keywords_es": "",
     "meta_keywords_ru": "",
     "meta_keywords_pt": "",
     "meta_keywords_zh": ""
  },
   "meta_description": { // 产品meta信息
     "meta_description_en": "sex xx meta keywords sex xx meta keywords sex xx meta keywords",
     "meta_description_fr": "",
     "meta_description_de": "",
     "meta_description_es": "",
     "meta_description_ru": "",
     "meta_description_pt": "",
     "meta_description_zh": ""
  },
   "image": {  // 产品的图片
     "main": { // 产品主图
       "image": "/1/11/111147807271192428.jpg",
       "label": "",
       "sort_order": "",
       "is_thumbnails": "1",  // 产品详情页面：图片是否在橱窗图中显示，1代表显示
       "is_detail": "1"         // 产品详情页面：图片是否在描述中显示，1代表显示
    },  
     "gallery": [  // 产品的细节图
       {
         "image": "/2/01/20161024170457_13851.jpg",
         "label": "",
         "sort_order": ""
      },
       {
         "image": "/2/01/20161024170457_21098.jpg",
         "label": "",
         "sort_order": ""
      },
       {
         "image": "/2/01/20161101155240_26690.jpg",
         "label": "",
         "sort_order": ""
      },
       {
         "image": "/2/01/20161101155240_56328.jpg",
         "label": "",
         "sort_order": ""
      },
       {
         "image": "/2/01/20161101155240_94256.jpg",
         "label": "",
         "sort_order": ""
      }
    ]
  },
   "description": {   // 产品描述信息
     "description_en": "3333",
     "description_fr": "",
     "description_de": "",
     "description_es": "",
     "description_ru": "",
     "description_pt": "",
     "description_zh": ""
  },
   "short_description": {  // 产品短描述信息
     "short_description_en": "334343",
     "short_description_fr": "",
     "short_description_de": "",
     "short_description_es": "",
     "short_description_ru": "",
     "short_description_pt": "",
     "short_description_zh": ""
  },
   "custom_option": {  // 产品 custom option部分，也就是淘宝模式的颜色尺码这类属性
     "red-s-s2-s3": {
       "my_color": "red",
       "my_size": "S",
       "my_size2": "S2",
       "my_size3": "S3",
       "sku": "red-s-s2-s3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161024170457_10036.jpg"
    },
     "red-m-s2-s3": {
       "my_color": "red",
       "my_size": "M",
       "my_size2": "S2",
       "my_size3": "S3",
       "sku": "red-m-s2-s3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161024170457_10036.jpg"
    },
     "red-m-m2-s3": {
       "my_color": "red",
       "my_size": "M",
       "my_size2": "M2",
       "my_size3": "S3",
       "sku": "red-m-m2-s3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161024170457_10036.jpg"
    },
     "red-m-m2-m3": {
       "my_color": "red",
       "my_size": "M",
       "my_size2": "M2",
       "my_size3": "M3",
       "sku": "red-m-m2-m3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161024170457_10036.jpg"
    },
     "red-m-m2-l3": {
       "my_color": "red",
       "my_size": "M",
       "my_size2": "M2",
       "my_size3": "L3",
       "sku": "red-m-m2-l3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161024170457_10036.jpg"
    },
     "red-m-l2-l3": {
       "my_color": "red",
       "my_size": "M",
       "my_size2": "L2",
       "my_size3": "L3",
       "sku": "red-m-l2-l3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161024170457_10036.jpg"
    },
     "red-m-l2-s3": {
       "my_color": "red",
       "my_size": "M",
       "my_size2": "L2",
       "my_size3": "S3",
       "sku": "red-m-l2-s3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161024170457_10036.jpg"
    },
     "red-m-l2-m3": {
       "my_color": "red",
       "my_size": "M",
       "my_size2": "L2",
       "my_size3": "M3",
       "sku": "red-m-l2-m3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161024170457_10036.jpg"
    },
     "red-l-l2-m3": {
       "my_color": "red",
       "my_size": "L",
       "my_size2": "L2",
       "my_size3": "M3",
       "sku": "red-l-l2-m3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161024170457_10036.jpg"
    },
     "red-l-m2-m3": {
       "my_color": "red",
       "my_size": "L",
       "my_size2": "M2",
       "my_size3": "M3",
       "sku": "red-l-m2-m3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161024170457_10036.jpg"
    },
     "red-l-m2-l3": {
       "my_color": "red",
       "my_size": "L",
       "my_size2": "M2",
       "my_size3": "L3",
       "sku": "red-l-m2-l3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161024170457_10036.jpg"
    },
     "black-s-s2-s3": {
       "my_color": "black",
       "my_size": "S",
       "my_size2": "S2",
       "my_size3": "S3",
       "sku": "black-s-s2-s3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161101155240_56328.jpg"
    },
     "black-s-l2-s3": {
       "my_color": "black",
       "my_size": "S",
       "my_size2": "L2",
       "my_size3": "S3",
       "sku": "black-s-l2-s3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161101155240_56328.jpg"
    },
     "black-s-xl2-s3": {
       "my_color": "black",
       "my_size": "S",
       "my_size2": "XL2",
       "my_size3": "S3",
       "sku": "black-s-xl2-s3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161101155240_56328.jpg"
    },
     "black-s-s2-l3": {
       "my_color": "black",
       "my_size": "S",
       "my_size2": "S2",
       "my_size3": "L3",
       "sku": "black-s-s2-l3",
       "qty": NumberInt(9999),
       "price": NumberInt(0),
       "image": "/2/01/20161101155240_56328.jpg"
    },
     "blue-s-s2-s3": {
       "my_color": "blue",
       "my_size": "S",
       "my_size2": "S2",
       "my_size3": "S3",
       "sku": "blue-s-s2-s3",
       "qty": NumberInt(9999),
       "price": 5,
       "image": "/2/01/20161101155240_94256.jpg"
    }
  },
   "attr_group": "test_group",  // 产品属性组
   "relation_sku": "",  // 产品相关产品
   "buy_also_buy_sku": "", // 产品买了还买
   "see_also_see_sku": "", // 产品看了还看
   "my_remark": "111",   // 下面是属性组中定义的属性，
   "my_email": "1111@22.com",
   "my_date": "2016-11-03",
   "style": "Cute",
   "dresses-length": "Mini",
   "pattern-type": "Animal",
   "sleeve-length": "Sleeveless",
   "collar": "Round Neck",
   "url_key": "/test-computer-92982496",  // 产品urlkey
   "reviw_rate_star_average": 5, // 产品平均评分
   "review_count": NumberInt(3), // 产品评论个数
   "reviw_rate_star_average_lang": {  // 产品在各个语言的评分
     "reviw_rate_star_average_lang_zh": 5,
     "reviw_rate_star_average_lang_en": 4
  },
   "review_count_lang": {  // 产品在各个语言的评论数
     "review_count_lang_zh": NumberInt(1),
     "review_count_lang_en": NumberInt(2)
  }
}	

```

