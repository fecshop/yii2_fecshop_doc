Fecshop Server Api- 状态码
====================

> fecshop appserver 提供的api的各个状态码返回的含义


```
/**
 * 公共状态码
 */
200    : 成功状态
1000000: 程序内部错误：未知错误
1000001: 程序内部错误：mysql连接错误
1000002: 程序内部错误：mongodb连接错误
1000003: 程序内部错误：redis连接错误
1000004: 无效数据：token无效
1000005: 无效请求：该url不存在
1000006: 格式错误：邮箱格式无效
1000007: 无效数据：验证码错误
1000008: 无效参数
1000009: 参数丢失
1000010: 超出限制
1000011: 数据重复
1000012: 确定为攻击返回的状态
1000013: 程序内部错误：传递的无效code
/**
 * 用户部分的状态码
 */
1100000: 注册 - 邮箱已经存在
1100001: 注册 - 邮箱格式不正确 
1100002: 登录 - 账户的邮箱或者密码不正确
1100003: 登录 - 账户的token已经过期,或者没有登录
1100004: 编辑 - 账户的密码格式不正确
1100005: contact - 发送邮件失败
1100006: 登录 - 账户的token已经过期,或者没有登录
1100007: 注册 - 邮箱已经存在
1100008: 账户中该email不存在
1100009: 忘记密码 - token超时
1100010: 忘记密码 - 通过邮件充值密码，传递的参数缺失或不正确
1100011: 忘记密码 - 充值密码失败
1100012: customer address - address id 不存在
1100013: customer address - address 编辑传入的param存在问题，无效
1100014: customer order - reorder 传入的order_id 无效
1100015: custome favorite - favorite id is not exit


/**
 * category状态码
 */
1200000: 分类：分类不存在
 
/**
 * product状态码
 */
1300000: 产品 - 产品收藏失败
1300001: 产品 - 产品不存在，或者已经下架
1300002: 产品 - 产品不存在，或者已经下架
1300003: 产品 - 产品保存平台失败
/**
 * cart
 */
1400001: Cart - 产品加入购物车失败
1400002: Cart - 产品加入购物车传递参数无效
1400003: Cart - 更改cart中product的个数失败
1400004: Cart - coupon不可用
/**
 * order
 */
1500001: Order - 下订单，产品库存不足。
1500002: Order - 下订单，生成订单失败。
1500003: Order - 通过paypal express方式支付，获取token失败
1500004: Order - 下订单，必填的订单字段验证失败。
1500005: Order - 下订单，游客在下订单的同时直接生成账户失败。
1500006: Order - 下订单，游客在下订单的同时保存address信息失败。
1500007: Order - 下订单，购物车数据为空
1500008: Order - 下订单页面，切换address，获取运费的接口，无法获取country
1500009: Order - 通过paypal standard方式支付，获取token失败
1500010: Order - 通过paypal standard方式支付，通过api支付失败
1500011: Order - 通过paypal standard方式支付，api支付订单成功后，更新订单信息失败
1500012: order - 无法从dbsession中获取order increment id
1500013: Order - 通过paypal express方式支付，通过api支付失败
1500014: Order - 通过paypal express方式支付，api支付订单成功后，更新订单信息失败
1500015: Order - 通过paypal express方式支付，获取PayerID失败
1500016: Order - 通过paypal express方式支付，获取address失败
1500017: Order - 下订单，订单已经被支付过
1500018: Order - 下订单，订单不存在
1500019: Order - 下订单，支付宝支付订单失败
/**
 * cms
 */
1600001: Article - 文章不存在

```

























