供应商订单发货
===============

> Api描述：将可备货订单进行发货

URL: `http://enterprise.appapi.fancyecommerce.com/v2/order/dispatch`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fbbcbase-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| increment_id            | 必须        |   string       | 订单编号|
| tracking_number            | 必须        |   string       | 订单物流编号|

**Request JSON Data(Body Example)：**

```
{
    "increment_id": "1100000107",
    "tracking_number": "2222222222222"
}
```


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
  "message": "dispatch order success",
  "data": []
}
```