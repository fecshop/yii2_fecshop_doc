Fecmall Api 产品品牌分类 UpsertOne
=============


> Api描述：根据传递的json数据，更新product brand category数据，存在相应的id则更新，不存在则插入



URL: `http://fecshop.appapi.fancyecommerce.com/v1/productbrandcategory/upsertone2`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| remote_id           | 必须          |   String or int    | 远程数据库brand category数据表的id值，该字段作为upsert的key值   |
| name           | 必须        |   Json Array    | 品牌名称，多语言格式，譬如：{ "name_en": "大华","name_zh": ""}       |
| status   | 必须        |   Int    | 选择值[`1`,`2`]，属性状态，1代表激活，2代表关闭|
| sort_order   | 选填        |   Int    | 排序  |

**补充1**：对于参数`remote_id`是远程数据表的id，譬如erp进行数据同步，需要将`erp`.`product_brand_category`表的数据行`id`，传递过来
，作为`remote_id`的值，在`upsert api`中，会先查询`remote_id`对应的`数据行`是否存在，如果存在则`更新`此数据行，
如果没有`remote_id`对应的数据行，则会进行`插入`数据。下次再此调用该api同步数据，就会通过`remote_id`查询到
此数据行，然后进行`更新`。


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
    "remote_id": "4",
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
    "status": "1"
}
```


**Response JSON Data(Body Example)**：将会返回保存到数据库中的数据最终值

```
{
    "code": 200,
    "message": "update product brandcategory success",
    "data": {
        "addData": {
            "id": 119,
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
            "created_at": 1618920201,
            "updated_at": 1618920867,
            "remote_id": "4"
        }
    }
}
```
































































































