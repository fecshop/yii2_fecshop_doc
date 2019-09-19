Api- Customer 忘记密码重置提交
================

> 忘记密码发送给用户邮箱后，用户点击邮箱里面的链接进入网站后，
> 填写充值密码信息，点击按钮提交后访问的api

URL: `/customer/forgot/submitresetpassword`

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
| resetToken      | 必须        |   String    | 重置密码的token   |
| email           | 必须        |   String    | email     |
| newPassword     | 必须        |   String    | 新密码    |
| confirmPassword | 必须        |   String    | 新密码确认|


**请求参数示例如下：**

```
{
    resetToken: "zaow-pri7o_w_p2DTLFs1z0iC4xonLIY_1509445774",
    email: "2358269014@qq.com",
    newPassword: "444444",
    confirmPassword: "444444"
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
| 1100009         | 忘记密码：token超时                                | 
| 1100010         | 忘记密码：通过邮件重置密码，传递的参数缺失或不正确 | 
| 1100011         | 忘记密码：重置密码失败                             | 




#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": []
}
```