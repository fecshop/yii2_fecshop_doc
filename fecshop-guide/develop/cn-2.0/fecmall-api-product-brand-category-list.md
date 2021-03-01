Fecmall Api 产品属性列表
================

> Api描述：按照分页，得到产品属性数据的列表

URL: `http://fecshop.appapi.fancyecommerce.com/v1/productbrandcategory/list`

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
    "message": "fetch product brand category success",
    "data": [
        {
            "id": "1",
            "name": {
                "name_en": "母婴",
                "name_zh": "",
                "name_fr": "",
                "name_de": "",
                "name_es": "",
                "name_pt": "",
                "name_ru": "",
                "name_it": ""
            },
            "sort_order": "1",
            "status": "1",
            "created_at": "1585734124",
            "updated_at": "1585734124"
        },
        {
            "id": "2",
            "name": {
                "name_en": "服装",
                "name_zh": "",
                "name_fr": "",
                "name_de": "",
                "name_es": "",
                "name_pt": "",
                "name_ru": "",
                "name_it": ""
            },
            "sort_order": "2",
            "status": "1",
            "created_at": "1585734131",
            "updated_at": "1585734131"
        },
        {
            "id": "3",
            "name": {
                "name_en": "家居",
                "name_zh": "",
                "name_fr": "",
                "name_de": "",
                "name_es": "",
                "name_pt": "",
                "name_ru": "",
                "name_it": ""
            },
            "sort_order": "3",
            "status": "1",
            "created_at": "1585734140",
            "updated_at": "1585734140"
        },
        {
            "id": "4",
            "name": {
                "name_en": "通讯",
                "name_zh": "",
                "name_fr": "",
                "name_de": "",
                "name_es": "",
                "name_pt": "",
                "name_ru": "",
                "name_it": ""
            },
            "sort_order": "4",
            "status": "1",
            "created_at": "1585747204",
            "updated_at": "1585747204"
        },
        {
            "id": "5",
            "name": {
                "name_en": "食品",
                "name_zh": "",
                "name_fr": "",
                "name_de": "",
                "name_es": "",
                "name_pt": "",
                "name_ru": "",
                "name_it": ""
            },
            "sort_order": "5",
            "status": "1",
            "created_at": "1585747219",
            "updated_at": "1585747219"
        }
    ]
}
```





























