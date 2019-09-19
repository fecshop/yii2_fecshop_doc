Api- Customer 登录提交
================

> 用户在 http://demo.fancyecommerce.com/#/customer/account/login 页面，输入email和password，
点击Sign In按钮后执行的api

URL: `/customer/login/account`

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
| email           | 必须        |   String     | 用户的email账户   |
| password        | 必须        |   String     | 用户的密码   |
| captcha         | 必须        |   String     | 用户登录填写的验证码，这个在服务端要求填写的时候，才会填写验证码，如果服务端不要求填写，则设置空字符串   |


**请求参数示例如下：**

```
{
    email: "2358269014@qq.com",   
    password: "xxxx",
    captcha:""
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
| 1100006         | 登录：用户已经登录                              | 
| 1000007         | 无效数据：验证码错误                            | 
| 1100002         | 登录：账户的邮箱或者密码不正确                  | 


#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": []
}
```