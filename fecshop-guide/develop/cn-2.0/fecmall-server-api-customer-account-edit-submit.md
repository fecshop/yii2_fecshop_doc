Api- Customer account编辑提交
================

> 用户中心编辑用户信息，填写完用户的修改信息，点击提交后访问的api

URL: `/customer/editaccount/update`

格式：`json`

方式：`post`

一：请求部分
---------

#### 1.Request Header


| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 必须        |   String     | 从localStorage取出来的值，识别用户登录状态的标示，用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |
| fecshop-currency  | 必须        |   String     | 从localStorage取出来的值，当前的货币值  |
| fecshop-lang      | 必须        |   String     | 从localStorage取出来的值，当前的语言code  |


#### 2.Request Body Form-Data：


| 参数名称             | 是否必须    |  类型       |  描述     |
| ----------------     | -----:      | :----:      |:----:     |
| firstname            | 必须        |   String    | 用户的first name  |
| lastname             | 必须        |   String    | 用户的last  name  |
| current_password     | 必须        |   String    | 用户的当前密码    |
| new_password         | 必须        |   String    | 用户的新密码      |
| confirm_new_password | 必须        |   String    | 用户的新密码确认  |

**请求参数示例如下：**

```
{
    firstname: "44444",
    lastname: "666",
    current_password: "444444",
    new_password: "111111",
    confirm_new_password: "111111"
}
```

二：返回部分
----------

#### 1.Reponse Header

| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 选填        |   String     | 用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |

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
| 1100004         | 编辑：账户的编辑数据不正确                             | 



#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": []
}
```