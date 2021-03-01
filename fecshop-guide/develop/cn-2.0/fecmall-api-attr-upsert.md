Fecmall Api 产品属性更新 UpsertOne
==============


> Api描述：根据传递的json数据，更新product attr数据

以远程数据库属性表的id，作为remote_id的参数值，当存在该值则更新，如果不存在则插入。

URL: `http://fecshop.appapi.fancyecommerce.com/v1/productattr/upsertone`

格式：`json`

方式：`post`

**Request Header 参数:**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token    | 必须        |   String    | 登录后获取的token,如何获取access-token，请参考[Fecshop Api 登录和验证](fecshop-api-login-and-verification.md)|


**Request JSON Data(Body)：**

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| remote_id           | 必须        |   String or int    | 远程数据库，attr数据表的id值，该字段作为upsert的key值       |
| attr_type         | 必须        |   String    | 选择值[`spu_attr`, `general_attr`], 属性类型，`spu_attr`代表规格属性，譬如颜色尺码，`general_attr`代表普通属性 |
| name           | 必须        |   String    | 产品属性名称，由`字符_- `组成，不要用中文。       |
| status   | 必须        |   Int    | 选择值[`1`,`2`]，属性状态，1代表激活，2代表关闭|
| show_as_img| 必须        |   Int    | 选择值[`1`,`2`]，只有当属性为规格属性，而且在商城中规格属性以图片的形式显示的时候才会选择1，譬如颜色，其他的都选择值2即可|
| display_type         | 必须        |   String    | 选择值：[`inputString`, `inputString-Lang`, i`nputEmail`, `inputDate`, `editSelect`, `select`], 因为值比较多，在下面单独描述各个值的含义|
| display_data          | 可选        |   数组或者空字符串    | 当`display_type`的值为select和editSelect的时候，才需要填写该值|
| is_require   | 必须        |   Int    | 选择值[`1`,`2`]，产品编辑的时候，是否必填？1代表必填，1代表选填|

补充1：`display_type`的选择子项值说明


`inputString`：当属性为字符串的时候选择该值，譬如产品的sku，spu等属性

`inputString-Lang`：当属性为多语言属性的时候选择该值，譬如产品的name，description等

`inputEmail`：当属性为邮箱类型的产品属性，这个很少用到

`inputDate`：当属性为日期类型的时候选择该值，譬如：特价过期时间，新产品到期时间等

`select`：当产品属性的值为下拉条类型，譬如产品品牌，产品状态等，并且产品属性只能从属性的子项中选择一个，不能选择其他的值，譬如状态属性只有开启和关闭2个状态值

`editSelect`：当产品属性为下拉条类型，但是值并不局限于属性中配置的子项，用户除了可以从下拉条中勾选已经存在的子项，也可以
当成一个input文本框填写新内容，譬如颜色属性，当属性中没有某些颜色子项，可以直接填写新值


补充2：`display_data`的说明

只有当display_type的值为select或者editSelect的时候，才会填写该值，该值的格式为：

```
[
{"key" => "red"},
{"key" => "blue"},
{"key" => "yellow"},
{"key" => "black"},
]
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





**Request JSON Data(Body Example)**：

```
{
    "remote_id" : "1",
    "attr_type": "spu_attr",
    "name": "color22",
    "status": "2",
    "db_type": "String",
    "show_as_img": "1",
    "display_type": "editSelect",
    "display_data": [
        {
            "key": "one-color"
        },
        {
            "key": "red"
        },
        {
            "key": "white"
        },
        {
            "key": "black"
        },
        {
            "key": "blue"
        },
        {
            "key": "green"
        },
        {
            "key": "yellow"
        },
        {
            "key": "gray"
        },
        {
            "key": "khaki"
        },
        {
            "key": "ivory"
        },
        {
            "key": "beige"
        },
        {
            "key": "orange"
        },
        {
            "key": "cyan"
        },
        {
            "key": "leopard"
        },
        {
            "key": "camouflage"
        },
        {
            "key": "silver"
        },
        {
            "key": "pink"
        },
        {
            "key": "purple"
        },
        {
            "key": "brown"
        },
        {
            "key": "golden"
        },
        {
            "key": "multicolor"
        },
        {
            "key": "white-blue"
        },
        {
            "key": "white-black"
        }
    ],
    "is_require": "1"
}

```


**Response JSON Data(Body Example)**：将会返回保存到数据库中的数据最终值

```
{
    "code": 200,
    "message": "update product attr success",
    "data": {
        "addData": {
            "id": "15",
            "remote_id": 1,
            "attr_type": "spu_attr",
            "name": "color22",
            "status": "2",
            "db_type": "String",
            "show_as_img": "1",
            "display_type": "editSelect",
            "display_data": [
                {
                    "key": "one-color"
                },
                {
                    "key": "red"
                },
                {
                    "key": "white"
                },
                {
                    "key": "black"
                },
                {
                    "key": "blue"
                },
                {
                    "key": "green"
                },
                {
                    "key": "yellow"
                },
                {
                    "key": "gray"
                },
                {
                    "key": "khaki"
                },
                {
                    "key": "ivory"
                },
                {
                    "key": "beige"
                },
                {
                    "key": "orange"
                },
                {
                    "key": "cyan"
                },
                {
                    "key": "leopard"
                },
                {
                    "key": "camouflage"
                },
                {
                    "key": "silver"
                },
                {
                    "key": "pink"
                },
                {
                    "key": "purple"
                },
                {
                    "key": "brown"
                },
                {
                    "key": "golden"
                },
                {
                    "key": "multicolor"
                },
                {
                    "key": "white-blue"
                },
                {
                    "key": "white-black"
                }
            ],
            "is_require": "1",
            "default": "",
            "created_at": 1564046977,
            "updated_at": 1612846650
        }
    }
}

```































