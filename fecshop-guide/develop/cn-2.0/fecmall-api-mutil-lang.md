AppApi多语言属性说明
=====================

> 对于name title description等属性，不同的语言，这些属性的内容
> 是相应的语言，因此这些属性被称为多语言属性，在fecshop这些属性都是
> 以数组的方式存储

### 配置语言

在给产品或者其他部分导入数据的时候，需要确定系统是否配置了相应的语言，
可以参看文档；[Fecshop 多语言](http://www.fecshop.com/doc/fecshop-guide/instructions/cn-1.0/guide-fecshop_mutil_lang.html)
的第一部分，一：语言的配置

### 导入属性值的填写

填写的方式，统一为 `属性名+'_'+语言简码`的方式作为数组的key，譬如产品name部分：

```
"name": {
    "name_en": "test computer",
    "name_fr": "",
    "name_de": "",
    "name_es": "",
    "name_ru": "",
    "name_pt": "",
    "name_zh": "测试计算机"
},
```

只要语言在第一部分已经配置，这里就可以填写导入。

### 关于导入必填项

默认语言是必须填写的，其他的语言可以选填，譬如fecshop默认的语言是`en_US`，
因此，`name['name_en']` 是必填的，其他的语言选填，
当其他的语言不填写，在前台显示的使用，如果当前语言的值为空，则会使用默认语言
的值作为当前语言的值。








