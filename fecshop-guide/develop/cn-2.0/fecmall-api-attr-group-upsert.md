Fecmall Api 产品属性组更新
=================


> Api描述：根据传递的json数据，更新product attr group数据

以远程数据库属性表的id，作为remote_id的参数值，当存在该值则更新，如果不存在则插入。



URL: `http://fecshop.appapi.fancyecommerce.com/v1/productattrgroup/upsertone`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| remote_id           | 必须        |   String or int     | 远程属性组表id       |
| name           | 必须        |   String    | 产品属性组名称，由`字符_- `组成，不要用中文。       |
| status   | 必须        |   Int    | 选择值[`1`,`2`]，属性状态，1代表激活，2代表关闭|
| attr_ids          | 必须         |   数组或者空字符串    | 属性数组|

补充1：`attr_ids`的说明

示例数据：

```
[
    {
        "attr_id": "11",
        "sort_order": 0
    },
    {
        "attr_id": "10",
        "sort_order": 0
    }
]


```

`attr_id`：属性id，`string` or `int`类型 (当用mongodb存储产品数据的时候，该值为字符串)

`sort_order`：属性排序，`int`类型



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



**Request JSON Data(Body Example)**：

```
{
    "remote_id": 1,
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
    "status": "1"
}
```


**Response JSON Data(Body Example)**：将会返回保存到数据库中的数据最终值

```
{
    "code": 200,
    "message": "update product attr group success",
    "data": {
        "addData": {
            "id": 10,
            "remote_id":1,
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
            "status": "1",
            "created_at": 1612850478,
            "updated_at": 1612850593
        }
    }
}

```


























































