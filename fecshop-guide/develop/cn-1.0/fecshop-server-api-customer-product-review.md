Api- 得到分类产品
================

> vue 分类页面，得到分类信息的api

URL: `/customer/productreview/index`

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

返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        "productList": [
            {
                "_id": {
                    "$oid": "59f1b535bfb7ae43950d79b3"      // 产品id
                },
                "product_spu": "p10001",                    // 产品SPU
                "product_id": "580835d0f656f240742f0b7c",   // 产品ID
                "rate_star": "4",                           // 产品评论星级
                "name": "44444 6666",                       // 产品评论人name
                "user_id": 46,                              // 产品评论人customer id
                "ip": "183.14.76.189",                      // 产品评论人的ip
                "summary": "9999999999999",                 // 产品评论标题
                "review_content": "99999999999999999999543253453299",       // 产品评论的内容
                "review_date": "2017-10-26 18:13:09",       // 产品评论时间
                "store": "fecshop.appserver.fancyecommerce.com",            // store
                "lang_code": "en",                          // 评论所在store的语言
                "status": 10,                               // 评论状态
                // 产品的图片
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160905101021_28071.jpg"
            },
            {
                "_id": {
                    "$oid": "59cf1841bfb7ae2f73783266"
                },
                "product_spu": "p10001",
                "product_id": "580835d0f656f240742f0b7c",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.127.4",
                "summary": "44444444",
                "review_content": "44444444444444444",
                "review_date": "2017-09-30 12:06:25",
                "store": "fecshop.appserver.fancyecommerce.com",
                "lang_code": "en",
                "status": 1,
                "audit_user": 2,
                "audit_date": 1506744393,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160905101021_28071.jpg"
            },
            {
                "_id": {
                    "$oid": "59cf1814bfb7ae2f73783265"
                },
                "product_spu": "p10001",
                "product_id": "580835d0f656f240742f0b7c",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.127.4",
                "summary": "rerer",
                "review_content": "erere",
                "review_date": "2017-09-30 12:05:40",
                "store": "fecshop.appserver.fancyecommerce.com",
                "lang_code": "en",
                "status": 1,
                "audit_user": 2,
                "audit_date": 1506744349,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160905101021_28071.jpg"
            },
            {
                "_id": {
                    "$oid": "59cf17b2bfb7ae29ca553ff5"
                },
                "product_spu": "p10001",
                "product_id": "580835d0f656f240742f0b7c",
                "rate_star": "3",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.127.4",
                "summary": "111111111111",
                "review_content": "222222222222222",
                "review_date": "2017-09-30 12:04:02",
                "store": "fecshop.appserver.fancyecommerce.com",
                "lang_code": "en",
                "status": 1,
                "audit_user": 2,
                "audit_date": 1506744278,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160905101021_28071.jpg"
            },
            {
                "_id": {
                    "$oid": "59cf16e3bfb7ae29ca553ff4"
                },
                "product_spu": "p10001",
                "product_id": "580835d0f656f240742f0b7c",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.127.4",
                "summary": "44444",
                "review_content": "5555",
                "review_date": "2017-09-30 12:00:35",
                "store": "fecshop.appserver.fancyecommerce.com",
                "lang_code": "en",
                "status": 1,
                "audit_user": 2,
                "audit_date": 1506744318,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160905101021_28071.jpg"
            },
            {
                "_id": {
                    "$oid": "59cf168fbfb7ae2f73783264"
                },
                "product_id": "580835d0f656f240742f0b7c",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.127.4",
                "summary": "111111111",
                "review_content": "222222222",
                "review_date": "2017-09-30 11:59:11",
                "store": "fecshop.appserver.fancyecommerce.com",
                "lang_code": "en",
                "status": 1,
                "audit_user": 2,
                "audit_date": 1506744325,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160905101021_28071.jpg"
            },
            {
                "_id": {
                    "$oid": "59cf167dbfb7ae2f73783263"
                },
                "product_id": "580835d0f656f240742f0b7c",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.127.4",
                "summary": "32323",
                "review_content": "23232",
                "review_date": "2017-09-30 11:58:53",
                "store": "fecshop.appserver.fancyecommerce.com",
                "lang_code": "en",
                "status": 1,
                "audit_user": 2,
                "audit_date": 1506744278,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160905101021_28071.jpg"
            },
            {
                "_id": {
                    "$oid": "59cf1549bfb7ae2f73783262"
                },
                "product_id": "580835d0f656f240742f0b7c",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.127.4",
                "summary": "323",
                "review_content": "3232",
                "review_date": "2017-09-30 11:53:45",
                "store": "fecshop.appserver.fancyecommerce.com",
                "lang_code": "en",
                "status": 1,
                "audit_user": 2,
                "audit_date": 1506744278,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160905101021_28071.jpg"
            },
            {
                "_id": {
                    "$oid": "59ce09e4bfb7ae27953db5d3"
                },
                "product_spu": "p10001",
                "product_id": "580835d0f656f240742f0b7c",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.127.4",
                "summary": "323232",
                "review_content": "3232323232",
                "review_date": "2017-09-29 16:52:52",
                "store": "fecshop.apphtml5.fancyecommerce.com",
                "lang_code": "en",
                "status": 1,
                "audit_user": 2,
                "audit_date": 1506744278,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160905101021_28071.jpg"
            },
            {
                "_id": {
                    "$oid": "59cc71b8bfb7ae5f5e3890a2"
                },
                "product_spu": "sk0004",
                "product_id": "57c7da4af656f273013bf56e",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.124.94",
                "summary": "432423",
                "review_content": "432423432",
                "review_date": "2017-09-28 11:51:20",
                "store": "fecshop.apphtml5.fancyecommerce.com",
                "lang_code": "en",
                "status": 1,
                "audit_user": 2,
                "audit_date": 1506744278,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160707145718_97803.jpg"
            },
            {
                "_id": {
                    "$oid": "59cc71adbfb7ae5f5b2f6f34"
                },
                "product_spu": "sk0003",
                "product_id": "57c7da9af656f2577a3bf56e",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.124.94",
                "summary": "4324234",
                "review_content": "432432432",
                "review_date": "2017-09-28 11:51:09",
                "store": "fecshop.apphtml5.fancyecommerce.com",
                "lang_code": "en",
                "status": 1,
                "audit_user": 2,
                "audit_date": 1506744278,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160804090311_12690.jpg"
            },
            {
                "_id": {
                    "$oid": "59cc719bbfb7ae5f374c9453"
                },
                "product_spu": "sk0002",
                "product_id": "57c7daecf656f273013bf570",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.124.94",
                "summary": "432432",
                "review_content": "432432423",
                "review_date": "2017-09-28 11:50:51",
                "store": "fecshop.apphtml5.fancyecommerce.com",
                "lang_code": "en",
                "status": 10,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160606112453_71094147323202778861.JPG"
            },
            {
                "_id": {
                    "$oid": "59cc718cbfb7ae5f5b2f6f33"
                },
                "product_spu": "432432",
                "product_id": "57bac5c6f656f2940a3bf570",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.124.94",
                "summary": "432423",
                "review_content": "432423423",
                "review_date": "2017-09-28 11:50:36",
                "store": "fecshop.apphtml5.fancyecommerce.com",
                "lang_code": "en",
                "status": 10,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/1/7/17147202419675158.jpg"
            },
            {
                "_id": {
                    "$oid": "59cc717cbfb7ae5f5b2f6f32"
                },
                "product_spu": "323232",
                "product_id": "57bac59ef656f24f123bf56e",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.124.94",
                "summary": "444444",
                "review_content": "444444444",
                "review_date": "2017-09-28 11:50:20",
                "store": "fecshop.apphtml5.fancyecommerce.com",
                "lang_code": "en",
                "status": 10,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/1/14/11471858072718.jpg"
            },
            {
                "_id": {
                    "$oid": "59cc6bccbfb7ae5c7e7aa9e4"
                },
                "product_spu": "sk2001",
                "product_id": "57c3aaa9f656f24f353bf56e",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.124.94",
                "summary": "2343242342",
                "review_content": "432423432",
                "review_date": "2017-09-28 11:26:04",
                "store": "fecshop.apphtml5.fancyecommerce.com",
                "lang_code": "en",
                "status": 10,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160722142719_52348.jpg"
            },
            {
                "_id": {
                    "$oid": "59cc6bb1bfb7ae5d12315643"
                },
                "product_spu": "sk0008",
                "product_id": "57c7da1ef656f20c713bf56e",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.124.94",
                "summary": "亚摇摇",
                "review_content": "亚摇摇",
                "review_date": "2017-09-28 11:25:37",
                "store": "fecshop.apphtml5.fancyecommerce.com",
                "lang_code": "en",
                "status": 10,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160810112221_81491.jpg"
            },
            {
                "_id": {
                    "$oid": "59cc6b9fbfb7ae5cb20c6873"
                },
                "product_spu": "22221",
                "product_id": "581ae91ff656f20f052f0b77",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.124.94",
                "summary": "哈哈哈哈哈哈",
                "review_content": "哈哈哈哈哈哈",
                "review_date": "2017-09-28 11:25:19",
                "store": "fecshop.apphtml5.fancyecommerce.com",
                "lang_code": "en",
                "status": 10,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20161101155240_26690.jpg"
            },
            {
                "_id": {
                    "$oid": "59cc6b8abfb7ae5c7e7aa9e3"
                },
                "product_spu": "sk1000",
                "product_id": "57cfc212f656f28b5adf9deb",
                "rate_star": "5",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.124.94",
                "summary": "32323",
                "review_content": "3232",
                "review_date": "2017-09-28 11:24:58",
                "store": "fecshop.apphtml5.fancyecommerce.com",
                "lang_code": "en",
                "status": 10,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160715121751_13739.jpg"
            },
            {
                "_id": {
                    "$oid": "59cb7221bfb7ae6ad7287942"
                },
                "product_spu": "sk2001",
                "product_id": "57c3aaa9f656f24f353bf56e",
                "rate_star": "4",
                "name": "44444 6666",
                "user_id": 46,
                "ip": "113.116.127.122",
                "summary": "212121",
                "review_content": "212121",
                "review_date": "2017-09-27 17:40:49",
                "store": "fecshop.apphtml5.fancyecommerce.com",
                "lang_code": "en",
                "status": 10,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20160722142719_52348.jpg"
            },
            {
                "_id": {
                    "$oid": "58806ec2f656f2a6132f0b77"
                },
                "product_spu": "222212",
                "product_id": "581c6833f656f2042f2f0b77",
                "rate_star": "5",
                "name": "terry water",
                "user_id": 46,
                "ip": "101.78.154.74",
                "summary": "xxx",
                "review_content": "xxxxxx",
                "review_date": "2017-01-19 15:46:10",
                "store": "fecshop.appfront.fancyecommerce.com/cn",
                "lang_code": "zh",
                "status": 1,
                "audit_user": 2,
                "audit_date": 1490627124,
                "imgUrl": "//img.fancyecommerce.com/media/catalog/product/cache/bd935443df1c50537d4edaab4af5d446/80/80/2/01/20161024170457_10036.jpg"
            }
        ],
        "count": 20,
        "numPerPage": 20,
        "noActiveStatus": 10,
        "refuseStatus": 2,
        "activeStatus": 1
    }
}
```