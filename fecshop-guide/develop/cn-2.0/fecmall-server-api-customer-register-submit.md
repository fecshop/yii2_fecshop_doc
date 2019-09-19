Api- Customer 注册提交
================

> 注册账户，填写信息提交后执行的api

URL: `/customer/register/account`

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


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| email           | 必须        |   String     | 注册账户email    |
| password        | 必须        |   String     | 注册密码         |
| firstname       | 必须        |   String     | firstname        |
| lastname        | 必须        |   String     | lastname         |
| is_subscribed   | 必须        |   boolean    | 是否订阅邮件     |
| captcha         | 必须        |   String     | 验证码           |

**请求参数示例如下：**

```
{
    email: "zqy2345678@126.com",
    password: "111111",
    firstname: "terry",
    lastname: "water",
    is_subscribed: true,
    captcha: "8272"
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
| 1100006         | 登录：用户已经登录账户                  | 
| 1100001         | 注册：注册数据格式不正确                | 
| 1100007         | 注册：邮箱已经存在                      | 




#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "content": "register success"
    }
}
```