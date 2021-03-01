Fecmall Api 产品属性 FetchOne
=================

> Api描述：根据传递的id，查询得到一行product attr数据


URL: `http://fecshop.appapi.fancyecommerce.com/v1/productattr/fetchone`

格式：`json`

方式：`get`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


您有2种方式，进行获取产品属性：

**Request JSON Data【1】(Body)：** 以`id`的方式进行获取产品属性

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| id              | 必须        |   String    | product_attribute的表id，譬如：11|

**Request JSON Data【2】(Body)：**以属性类型`attr_type`和属性名称`name`的方式进行获取产品属性

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| attr_type              | 必须        |   String    | 产品属性类型:`general_attr` or `spu_attr`, `general_attr`是普通产品属性，`spu_attr`是产品规格属性（Spu属性）|
| name              | 必须        |   String    | 产品属性名称|



**Response Header 参数:**


| 参数名称                    | 是否必须    |  类型       |  描述     |
| ----------------------------| -----:      | :----:      |:----:     |
| X-Rate-Limit-Limit          | 可选        |   String    | 在开启速度限制后才会存在，同一个时间段所允许的请求的最大数目|
| X-Rate-Limit-Remaining      | 可选        |   String    | 在开启速度限制后才会存在，在当前时间段内剩余的请求的数量|
| X-Rate-Limit-Reset          | 可选        |   String    | 在开启速度限制后才会存在，为了得到最大请求数所等待的秒数|



**Response JSON Data(Body)：**

格式：`json`

| 参数名称        | 是否必须    |  类型       |  描述        |
| ----------------| -----:      | :----:      |:----:        | 
| code            | 必须        |   Number    | 200 代表成功 |
| message         | 必须        |   String    | 执行结果的文字描述信息  |
| data            | 必须        |   Object    | api获取的数据保存到data中  |

**Response JSON Data(Body Example)：**

```
{
    "code": 200,
    "message": "fetch product attr success",
    "data": {
        "id": 2,
        "attr_type": "spu_attr",
        "name": "color",
        "status": 1,
        "db_type": "String",
        "show_as_img": 1,
        "display_type": "editSelect",
        "display_data": [
            {
                "key": "one-color"
            },
            {
                "key": "red"
            },
            {
                "key": "white"
            },
            {
                "key": "black"
            },
            {
                "key": "blue"
            },
            {
                "key": "green"
            },
            {
                "key": "yellow"
            },
            {
                "key": "gray"
            },
            {
                "key": "khaki"
            },
            {
                "key": "ivory"
            },
            {
                "key": "beige"
            },
            {
                "key": "orange"
            },
            {
                "key": "cyan"
            },
            {
                "key": "leopard"
            },
            {
                "key": "camouflage"
            },
            {
                "key": "silver"
            },
            {
                "key": "pink"
            },
            {
                "key": "purple"
            },
            {
                "key": "brown"
            },
            {
                "key": "golden"
            },
            {
                "key": "multicolor"
            },
            {
                "key": "white-blue"
            },
            {
                "key": "white-black"
            }
        ],
        "is_require": 1,
        "default": "",
        "created_at": 1564037530,
        "updated_at": 1564116936
    }
}
```














































