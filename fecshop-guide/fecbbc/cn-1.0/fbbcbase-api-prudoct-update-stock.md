供应商更新产品库存
===============

> Api描述：更新产品库存，通过累加和累减的方式，进行库存的更新

URL: `http://enterprise.appapi.fancyecommerce.com/v2/productstock/updatebybase`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fbbcbase-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| items            | 必须        |   array       | 批量更新产品库存的数据|


**Request JSON Data(Body Example)：**

```
{
    "items": [
        {
            "sku": "22221",    // 必填 ，字符串,产品id
            "qty": 2,               // 必填 ，int类型，库存更新的个数，正数为累加，负数为累减少            
            "custom_option_sku": "black-s"    // 选填 ，字符串，如果是custom option对应的库存减少，那么需要填写该项
        },
        {
            "sku": "p10001-kahaki-xxl",   
            "qty": 3                          
        },
        {
            "sku": "op0002",  
            "qty": -1        
        }
    ]
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
  "message": "update product stock success",
  "data": []
}
```