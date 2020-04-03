Fecmall Api 产品 更新库存
=========================

> Api描述：根据传递的id，删除一行product数据



URL: `http://fecshop.appapi.fancyecommerce.com/v1/product/updateqty`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| items             | 必填        |   Array[String]    | page 对应的id，该值是用来做update操作的唯一值 |



**Request JSON Data(Body Example)：**

```
{
    "items": [
        {
            "sku":"xxxx",
            "qty": 1,
            "type": "replace"
        },
        {
            "product_id": 15,
            "qty": 1,
            "type": "updateCounter"
        },
        {
            "sku":"zzzz",
            "product_id":"2",
            "qty": 1,
            "type": "updateCounter"
        }
    ]
    
}

```

items 子项说明：

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| sku              | 选填        |   string   | 产品的sku |
| product_id    | 选填        |   string   | 产品的id |
| qty              | 必填        |   int  | 库存数 |
| type            | 必填        |   int  | 库存的变动方式，覆盖的方式，还是累加累减的方式，（replace(覆盖库存)  or  updateCounter（累加或者累减））|

说明：

1.`sku`和`product_id`至少填写一个，如果两者都存在，那么以`product_id`为准

2.`type`是必填的

2.1`type`的值为`replace`：代表直接进行`覆盖更新`，也就是将qty的库存值，直接`覆盖`产品数据表数据

2.2`type`的值为`updateCounter`：代表直接进行`累加`或者`累减`，也就是在原来的基础上进行累加

举例：

1.前提：sku：`xxx`，库存目前为`10`，进行更新的api参数为  {"type":"updateCounter","qty":-2}, 进行更新操作后，xxx的库存变为`8`

2.前提：sku：`xx`x，库存目前为`10`，进行更新的api参数为  {"type":"replace","qty":12}, 进行更新操作后，xxx的库存变为`12`




**Response JSON Data(Body)：**

格式：`json`

| 参数名称        | 是否必须    |  类型       |  描述        |
| ----------------| -----:      | :----:      |:----:        | 
| code            | 必须        |   Number    | 200 代表成功 |
| message         | 必须        |   String    | 执行结果的文字描述信息  |
| data            | 必须        |   Object    | api获取的数据保存到data中  |

**Response JSON Data(Body Example)**：将会返回保存到数据库中的数据最终值

```
{
    "code": 200,
    "message": "update stock success",
    "data": []
}
```

报错示例信息：

```
{
    "code": 400,
    "message": "update stock  fail",
    "data": {
        "error": [
            "Product Update Stock Errors:ID:5a1c2da4bfb7ae0b615fee53 is not exist.",
            "Product Update Stock Errors:ID:5a1c2d3fbfb7ae0b615fee4b is not exist.",
            "Product Update Stock Errors:ID:5a1b678fbfb7ae44c26734f4 is not exist."
        ]
    }
}
```
