Api- Product Add Review Submit
================

> 产品评论页面，填写完评论信息，点击提交后访问的api

URL: `/catalog/reviewproduct/submitreview`

格式：`json`

方式：`post`


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


| 参数名称        | 是否必须    |  类型        |  描述     |
| ----------------| -----:      | :----:       |:----:     |
| product_id      | 必须        |   String     | Product Id    |
| customer_name   | 必须        |   String     | 评论用户的name   |
| summary         | 必须        |   String     | 评论的title   |
| captcha         | 必须        |   String     | 验证码    |
| review_content  | 必须        |   String     | 评论内容  |
| selectStar      | 必须        |   Integer    | 评星  |

**请求参数示例如下：**

```
{
    product_id: "580835d0f656f240742f0b7c",
    customer_name: "44444 666",
    summary: "summary title",
    captcha: "2744",
    review_content: "review content ...",
    selectStar: 5
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
| 1100003         | 登录：账户的token已经过期,或者没有登录          | 
| 1300001         | 产品：产品不存在，或者已经下架                  | 
| 1000007         | 无效数据：验证码错误                            | 
| 1000009         | 参数丢失                                        | 
| 1300003         | 产品：产品保存评论失败                          | 



 
 
#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": []
}
```