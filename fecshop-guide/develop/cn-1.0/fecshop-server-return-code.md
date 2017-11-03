Fecshop Server Api- 状态码
====================

> fecshop appserver 提供的api的各个状态码返回的含义


```
/**
 * 公共状态码
 */
public $status_success                                = 200;
public $status_unkown                                 = 1000000;   // 程序内部错误：未知错误
public $status_mysql_disconnect                       = 1000001;   // 程序内部错误：mysql连接错误
public $status_mongodb_disconnect                     = 1000002;   // 程序内部错误：mongodb连接错误
public $status_redis_disconnect                       = 1000003;   // 程序内部错误：redis连接错误
public $status_invalid_token                          = 1000004;   // 无效数据：token无效
public $status_invalid_request_url                    = 1000005;   // 无效请求：该url不存在
public $status_invalid_email                          = 1000006;   // 格式错误：邮箱格式无效
public $status_invalid_captcha                        = 1000007;   // 无效数据：验证码错误
public $status_invalid_param                          = 1000008;   // 无效参数
public $status_miss_param                             = 1000009;   // 参数丢失
public $status_limit_beyond                           = 1000010;   // 超出限制
public $status_data_repeat                            = 1000011;   // 数据重复
public $status_attack                                 = 1000012;   // 确定为攻击返回的状态
public $status_invalid_code                           = 1000013;   // 程序内部错误：传递的无效code
/**
 * 用户部分的状态码
 */
public $account_register_email_exist                  = 1100000; // 注册：邮箱已经存在
public $account_register_invalid_data                 = 1100001; // 注册：注册数据格式不正确 
public $account_login_invalid_email_or_password       = 1100002; // 登录：账户的邮箱或者密码不正确
public $account_no_login_or_login_token_timeout       = 1100003; // 登录：账户的token已经过期,或者没有登录
public $account_edit_invalid_data                     = 1100004; // 编辑：账户的编辑数据不正确
public $account_contact_us_send_email_fail            = 1100005; // contact：发送邮件失败
public $account_is_logined                            = 1100006; // 登录：用户已经登录
public $account_register_fail                         = 1100007; // 注册：邮箱已经存在
public $account_email_not_exist                       = 1100008; // 账户中该email不存在
public $account_forget_password_token_timeout         = 1100009; // 忘记密码：token超时
public $account_forget_password_reset_param_invalid   = 1100010; // 忘记密码：通过邮件重置密码，传递的参数缺失或不正确
public $account_forget_password_reset_fail            = 1100011; // 忘记密码：重置密码失败
public $account_address_is_not_exist                  = 1100012; // customer address：address id 不存在
public $account_address_edit_param_invaild            = 1100013; // customer address：address 编辑传入的param存在问题，无效
public $account_reorder_order_id_invalid              = 1100014; // customer order：reorder 传入的order_id 无效
public $account_favorite_id_not_exist                 = 1100015; // custome favorite: favorite id is not exit


/**
 * category状态码
 */
public $category_not_exist                             = 1200000; // 分类：分类不存在
 
/**
 * product状态码
 */
public $product_favorite_fail                          = 1300000; // 产品：产品收藏失败
public $product_not_active                             = 1300001; // 产品：已经下架

public $product_id_not_exist                           = 1300002; // 产品：产品不存在
public $product_save_review_fail                       = 1300003; // 产品：产品保存评论失败


/**
 * cart
 */
public $cart_product_add_fail                          = 1400001; // Cart：产品加入购物车失败
public $cart_product_add_param_invaild                 = 1400002; // Cart：产品加入购物车传递参数无效
public $cart_product_update_qty_fail                   = 1400003; // Cart：更改cart中product的个数失败
public $cart_coupon_invalid                            = 1400004; // Cart：coupon不可用


/**
 * order
 */
public $order_generate_product_stock_out               = 1500001; // Order: 下订单，产品库存不足。
public $order_generate_fail                            = 1500002; // Order: 下订单，生成订单失败。
public $order_paypal_express_get_token_fail            = 1500003; // Order: 通过paypal express方式支付，获取token失败
public $order_generate_request_post_param_invaild      = 1500004; // Order: 下订单，必填的订单字段验证失败。
public $order_generate_create_account_fail             = 1500005; // Order: 下订单，游客在下订单的同时直接生成账户失败。
public $order_generate_save_address_fail               = 1500006; // Order: 下订单，游客在下订单的同时保存address信息失败。
public $order_generate_cart_product_empty              = 1500007; // Order: 下订单，购物车数据为空
public $order_shipping_country_empty                   = 1500008; // Order: 下订单页面，切换address，从customer address中无法获取country 
public $order_paypal_standard_get_token_fail           = 1500009; // Order: 通过paypal standard方式支付，获取token失败
public $order_paypal_standard_payment_fail             = 1500010; // Order: 通过paypal standard方式支付，通过api支付失败
public $order_paypal_standard_updateorderinfoafterpayment_fail  = 1500011; // Order: 通过paypal standard方式支付，api支付订单成功后，更新订单信息失败
public $order_not_find_increment_id_from_dbsession     = 1500012; // order：无法从dbsession中获取order increment id

public $order_paypal_express_payment_fail              = 1500013;           // Order: 通过paypal express方式支付，通过api支付失败
public $order_paypal_express_updateorderinfoafterpayment_fail   = 1500014;  // Order: 通过paypal express方式支付，api支付订单成功后，更新订单信息失败
public $order_paypal_express_get_PayerID_fail          = 1500015;           // Order: 通过paypal express方式支付，获取PayerID失败
public $order_paypal_express_get_apiAddress_fail       = 1500016;           // Order: 通过paypal express方式支付，获取address失败

public $order_has_been_paid                            = 1500017;           // Order: 下订单，订单已经被支付过
public $order_not_exist                                = 1500018;           // Order: 下订单，订单不存在
public $order_alipay_payment_fail                      = 1500019;           // Order: 下订单，支付宝支付订单失败


```

























