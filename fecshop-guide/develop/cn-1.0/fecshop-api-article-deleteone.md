Fecshop Api Page DeleteOne
=========================

> Api描述：根据传递的id或url_key，删除一行page数据



URL: `http://fecshop.appapi.fancyecommerce.com/v1/article/deleteone`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| ids             | 必填        |   Array[String]    | page 对应的id，该值是用来做update操作的唯一值 |



**Request JSON Data(Body Example)：**

```
{
    "ids":[
        "5a17f5dbbfb7ae27876ed385",
        "5a17f446bfb7ae261d64e95a"
    ]
}

```


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

**Response JSON Data(Body Example)**：将会返回保存到数据库中的数据最终值

```
{
    "code": 200,
    "message": "add article success",
    "data": []
}

```

报错示例信息：


```
{
    "code": 400,
    "message": "remove article by ids fail",
    "data": {
        "error": [
            "Article Remove Errors:ID 5a17f5dbbfb7ae27876ed385 is not exist.",
            "Article Remove Errors:ID 5a17f446bfb7ae261d64e95a is not exist."
        ]
    }
}
```
