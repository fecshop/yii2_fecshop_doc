Fecmall Api 产品属性列表
================

> Api描述：按照分页，得到产品属性数据的列表

URL: `http://fecshop.appapi.fancyecommerce.com/v1/productattr/list`

格式：`json`

方式：`get`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| page            | 可选        |   Int       | 设置获取数据的当前页，如果为空，则代表为第一页|
| numPerPage            | 可选        |   Int       | 设置获取数据每页的个数，如果为空，则会使用fecmall的默认值|

**Response Header 参数:**


| 参数名称                    | 是否必须    |  类型       |  描述     |
| ----------------------------| -----:      | :----:      |:----:     |
| X-Pagination-Total-Count    | 必须        |   String    | 资源的总数量|
| X-Pagination-Page-Count     | 必须        |   String    | 资源的总页数|
| X-Pagination-Current-Page   | 必须        |   String    | 资源的当前页（目前是第几页）|
| X-Pagination-Per-Page       | 必须        |   String    | 每页资源的数量|
| X-Rate-Limit-Limit          | 可选        |   String    | 在开启速度限制后才会存在，同一个时间段所允许的请求的最大数目|
| X-Rate-Limit-Remaining      | 可选        |   String    | 在开启速度限制后才会存在，在当前时间段内剩余的请求的数量|
| X-Rate-Limit-Reset          | 可选        |   String    | 在开启速度限制后才会存在，为了得到最大请求数所等待的秒数|



**Response JSON Data(Body)：**

格式：`json`

| 参数名称        | 是否必须    |  类型       |  描述        |
| ----------------| -----:      | :----:      |:----:        | 
| code            | 必须        |   Number    | 200 代表成功 |
| message         | 必须        |   String    | 执行结果的文字描述信息  |
| data            | 必须        |   Array    | api获取的数据保存到data中  |

**Response JSON Data(Body Example)：**

```
{
    "code": 200,
    "message": "fetch product attr success",
    "data": [
        {
            "id": "2",
            "attr_type": "spu_attr",
            "name": "color",
            "status": "1",
            "db_type": "String",
            "show_as_img": "1",
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
            "is_require": "1",
            "default": "",
            "created_at": "1564037530",
            "updated_at": "1564116936"
        },
        {
            "id": "3",
            "attr_type": "spu_attr",
            "name": "size",
            "status": "1",
            "db_type": "String",
            "show_as_img": "2",
            "display_type": "select",
            "display_data": [
                {
                    "key": "one-size"
                },
                {
                    "key": "S"
                },
                {
                    "key": "M"
                },
                {
                    "key": "L"
                },
                {
                    "key": "XL"
                },
                {
                    "key": "XXL"
                },
                {
                    "key": "XXXL"
                },
                {
                    "key": "XXXXL"
                }
            ],
            "is_require": "1",
            "default": "",
            "created_at": "1564046977",
            "updated_at": "1564046977"
        },
        {
            "id": "4",
            "attr_type": "general_attr",
            "name": "my_remark",
            "status": "1",
            "db_type": "String",
            "show_as_img": "2",
            "display_type": "inputString",
            "display_data": "",
            "is_require": "2",
            "default": "",
            "created_at": "1564047062",
            "updated_at": "1564047062"
        }
    ]
}
```





























