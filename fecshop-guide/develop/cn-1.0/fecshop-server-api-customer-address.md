Api- Customer address 列表
================

> 账户中心，获取用户的address列表的api

URL: `/customer/address/index`

格式：`json`

方式：`get`


一：请求部分
---------

#### 1.Request Header


| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 必须        |   String     | 从localStorage取出来的值，识别用户登录状态的标示，用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |
| fecshop-uuid      | 必须        |   String     | 从localStorage取出来的值，用户的唯一标示，VUE第一次访问服务端，服务端会返回fecshop-uuid ，VUE将其保存到本地，后面的每一次请求都需要加上fecshop-uuid    |
| fecshop-currency  | 必须        |   String     | 从localStorage取出来的值，当前的货币值  |
| fecshop-lang      | 必须        |   String     | 从localStorage取出来的值，当前的语言code  |


#### 2.Request Body Form-Data：


无


**请求参数示例如下：**

```
无
```

二：返回部分
----------

#### 1.Reponse Header

| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 选填        |   String     | 用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |
| fecshop-uuid      | 必须        |   String     | 用户的唯一标示，VUE第一次访问服务端，服务端会返回fecshop-uuid ，VUE将其保存到本地，后面的每一次请求都需要加上fecshop-uuid    |

#### 2.Reponse Body Form-Data：

格式：`json`

| 参数名称        | 是否必须    |  类型       |  描述        |
| ----------------| -----:      | :----:      |:----:        | 
| code            | 必须        |   Number    | 返回状态码，200 代表完成，完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md) |
| message         | 必须        |   String    | 返回状态字符串描述  |
| data            | 必须        |   Array     | 返回详细数据        |


#### 3.参数code所有返回状态码：（完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md) ）

| code Value      |        描述                                        |
| ----------------| --------------------------------------------------:| 
| 200             | 成功状态码                                         |  
| 1100003         | 登录：账户的token已经过期,或者没有登录                  | 



#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "addressList": [        // 用户的address列表
            {
                "address_id": "117",        // customer address表的 id
                "first_name": "111",        // 收货人的first name
                "email": "34343@3232.com",  // 收货人的email
                "last_name": "222",         // 收货人的last name
                "company": null,            // 收货人的公司
                "telephone": "3232",        // 收货人的电话
                "fax": null,                // 收货人的传真
                "street1": "3232",          // 收货人的街道详细1
                "street2": "3232",          // 收货人的街道详细2
                "city": "3232",             // 收货人的城市
                "state": "BJ",              // 收货人的省/州
                "zip": "ewewew",            // 收货人的邮编
                "country": "CN",            // 收货人的国家简码
                "customer_id": "46",        // 收货人的customer account id
                "created_at": "1506397313", // 收货地址的创建时间
                "updated_at": "1509161659", // 收货人地址的更新时间
                "is_default": "2",          // 是否是默认收货地址，1代表是，2代表否
                "stateName": "北京市",      // 收货人的省市全称
                "countryName": "China"      // 收货人的国家全称
            },
            {
                "address_id": "118",
                "first_name": "2121",
                "email": "fdfd@3232.com",
                "last_name": "2121",
                "company": null,
                "telephone": "2121",
                "fax": null,
                "street1": "2121",
                "street2": "2121",
                "city": "2121",
                "state": "NO",
                "zip": "2121",
                "country": "AT",
                "customer_id": "46",
                "created_at": "1506397526",
                "updated_at": "1509158174",
                "is_default": "1",
                "stateName": "Niederösterreich",
                "countryName": "Austria"
            }
        ]
    }
}
```