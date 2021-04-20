Fecmall Api 产品品牌 UpsertOne-2
=================


> Api描述：根据传递的json数据，更新product brand数据，存在相应的id则更新，不存在则插入
，此部分是用于erp传递产品品牌的api


由于历史原因，这个api[Fecmall Api 产品品牌 UpsertOne](fecmall-api-product-brand-upsert.md)用于shopfw传递数据，不方便做出更改，
而当前的文档用于erp传递产品品牌

URL: `http://fecshop.appapi.fancyecommerce.com/v1/productbrand/upsertone2`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| id           | 可选        |   String or int    | brand数据表的id值，该字段作为upsert的key值 ，当id为空则为新增数据，新增数据行的id为数据库生成，当id有值而且在数据表中存在该id则更新，当id有值而且在数据表中不存在该id则插入数据，插入数据行的id为当前参数指定的id      |
| name           | 必须        |   Json Array    | 品牌名称，多语言格式，譬如：{ "name_en": "大华","name_zh": ""}       |
| brand_category_id   | 必须        |   Int    | 品牌分类id|
| logo | 选填        |   String    | logo文件路径字符串 |
| website_url         | 选填        |   String    | 品牌官网url |
| status          | 必须        |   String    | 品牌状态  |




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
    "remote_id": 4,
    "name": {
        "name_en": "大华",
        "name_zh": "",
        "name_fr": "",
        "name_de": "",
        "name_es": "",
        "name_pt": "",
        "name_ru": "",
        "name_it": ""
    },
    "brand_category_id": "4",
    "logo": "/q/v5/qv5ut9v6tdhy9hf1585747365.png",
    "website_url": "http://www.dahua.com",
    "status": 1
}

```


**Response JSON Data(Body Example)**：将会返回保存到数据库中的数据最终值

```
{
    "code": 200,
    "message": "update product brand success",
    "data": {
        "addData": {
            "id": 120,
            "name": {
                "name_en": "大华2877782",
                "name_zh": "",
                "name_fr": "",
                "name_de": "",
                "name_es": "",
                "name_pt": "",
                "name_ru": "",
                "name_it": ""
            },
            "brand_category_id": 119,
            "logo": "/q/v5/qv5ut9v6tdhy9hf1585747365.png",
            "website_url": "http://www.dahua1.com",
            "status": 1,
            "created_at": 1618920038,
            "updated_at": 1618920397,
            "remote_id": 4
        }
    }
}

```






























































