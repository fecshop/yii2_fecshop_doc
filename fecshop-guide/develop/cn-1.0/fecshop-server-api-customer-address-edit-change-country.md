Api- Customer address 编辑切换国家
================

> 在账户中心编辑address的时候，当切换国家，需要获得相应的`州/省`信息，来做select下拉条
里面的内容，该api就是做这个事情，获取切换国家后对应的 `州/省` 信息

URL: `/customer/address/changecountry`

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


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| country         | 必须        |   String    | 国家Code   |

**请求参数示例如下：**

```
{
    country: "CN"
}
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
        "stateIsSelect": 1,  // 在系统中是否对当前选择的国家配置了省/州？1代表是，2代表否，如果为1，则省显示为下拉条的select，如果为2，则显示为input输入框
        "stateArr": {  // 当stateIsSelect 为1时，这里显示当前国家对应的省的数组。如果stateIsSelect 为2，这里为空
            "BJ": "北京市",
            "SH": "上海市",
            "TJ": "天津市",
            "CQ": "重庆市",
            "HEB": "河北省",
            "SAX": "山西省",
            "LN": "辽宁省",
            "JL": "吉林省",
            "HLJ": "黑龙江省",
            "JS": "江苏省",
            "ZJ": "浙江省",
            "AH": "安徽省",
            "FJ": "福建省",
            "JX": "江西省",
            "SD": "山东省",
            "HEN": "河南省",
            "HUB": "湖北省",
            "HUN": "湖南省",
            "GD": "广东省",
            "HN": "海南省",
            "SC": "四川省",
            "HZ": "贵州省",
            "YN": "云南省",
            "SNX": "陕西省",
            "GS": "甘肃省",
            "QH": "青海省",
            "TW": "台湾省",
            "GX": "广西壮族自治区",
            "NMG": "内蒙古自治区",
            "XZ": "西藏自治区",
            "NX": "宁夏回族自治区",
            "XJ": "新疆维吾尔自治区",
            "XG": "香港特别行政区"
        }
    }
}
```