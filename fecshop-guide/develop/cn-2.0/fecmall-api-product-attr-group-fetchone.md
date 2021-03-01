Fecmall Api 产品属性组 FetchOne
=================

> Api描述：根据传递的id，查询得到一行product attr group数据


URL: `http://fecshop.appapi.fancyecommerce.com/v1/productattrgroup/fetchone`

格式：`json`

方式：`get`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|

您有2种方式，进行获取产品属性：

**Request JSON Data【1】(Body)：** 以`id`的方式进行获取产品属性组

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| id              | 可选        |   String    | product_attribute_group的表id，譬如：11|

**Request JSON Data【2】(Body)：** 以属性组名称`name`的方式进行获取产品属性组

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| name              | 必须        |   String    | 产品属性组名称。|

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
    "message": "fetch product attr group success",
    "data": {
        "id": 10,
        "name": "clothes_group8888",
        "attr_ids": [
            {
                "attr_id": "11",
                "sort_order": 0
            },
            {
                "attr_id": "10",
                "sort_order": 0
            },
            {
                "attr_id": "9",
                "sort_order": 0
            },
            {
                "attr_id": "8",
                "sort_order": 0
            },
            {
                "attr_id": "7",
                "sort_order": 0
            },
            {
                "attr_id": "3",
                "sort_order": 6
            },
            {
                "attr_id": "2",
                "sort_order": 5
            }
        ],
        "status": 1,
        "created_at": 1612850478,
        "updated_at": 1612850593
    }
}
```














































