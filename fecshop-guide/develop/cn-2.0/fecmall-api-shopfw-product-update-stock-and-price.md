Fecmall Api ShopFw-产品更新库存和价格
===================


Fecmall Api ShopFw-产品新增
=================


> Api描述：根据传递的json数据，新增一行product数据, 该api是专门给shopfw采集工具使用的。



URL: `http://fecshop.appapi.fancyecommerce.com/v1/product/updatestockandqty`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称          | 是否必须    |  类型       |  描述     |
| ------------------| -----:      | :----:      |:----:     |
| items              | 必须        |   Array     | 里面包含sku，qty，price等|

items详细说明


| 参数名称          | 是否必须    |  类型       |  描述     |
| ------------------| -----:      | :----:      |:----:     |
| sku              | 必须        |   string     | sku编码|
| price              | 必须        |   float     | 产品原价|
| special_price              | 必须        |   float     | 产品特价,如果没有特价直接填写0|
| qty              | 必须        |   int     | 销售库存数，直接覆盖fecmall的库存值|




产品导入接口的数据示例：



**Request JSON Data(Body Example)：**

```
{
    "items":[
        {"sku":"gmgq1612880482-ziq6kn", "price":12.22, "special_price":11.11, "qty":14},
        {"sku":"gmgq1612880482-bpb5z9", "price":22.22, "special_price":21.11, "qty":24},
        {"sku":"gmgq1612880482-h2v9hc", "price":32.22, "special_price":31.11, "qty":34}
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
    "message": "add product success",
    "data": []
}

```






































































