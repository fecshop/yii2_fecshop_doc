数据库字段介绍
============

> 追踪接收的数据字段说明


```

{
    "_id": ObjectId("5ad04d2abfb7ae65301c31cd"),    //id
   "uuid": "e37501a7-bc09-fb98-46e1-ffce67ec85c6",  // 唯一标示
   "ip": "183.14.78.93",                            // ip
   "country_code": "CN",                            // 国家简码
   "country_name": "China",                         // 国家全称
   "state_name": "Guangdong",                       // 省
   "city_name": "Shenzhen",                         // 城市
   "website_id": "9b17f5b4-b96f-46fd-abe6-a579837ccdd9", // 网站唯一标示
   "devide": "PC",                                  // 设备，pc代表电脑端， 其他譬如：Mobile:Android 代表手机安卓端
   "user_agent": "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36",
   "browser_name": "Chrome",                        // 浏览器名称
   "browser_version": "63.0",                       // 浏览器版本
   "browser_date": "2018-04-13 14:24:43",           // 浏览器时间
   "browser_lang": "zh-CN",                         // 浏览器语言
   "operate": "Windows",                            // 操作系统
   "operate_relase": "Windows 7",                   // 操作系统版本
   "url": "http://fecshop.appfront.fancyecommerce.com/men", // 当前的url
   "domain": "fecshop.appfront.fancyecommerce.com",         // 当前的域名
   "title": "Men",                                          // 当前页面的meta title
   "refer_url": "http://fecshop.appfront.fancyecommerce.com/checkout/cart",  // 来源url，也就是从哪个url点击过来的
   "first_referrer_domain": "redirect",     // 首次访问的来源url，redirect代表直接访问
   "first_referrer_url": "redirect",        // 首次访问的来源url中的域名，redirect代表直接访问
   "cl_activity": "",                       // 用户直接访问网站的页面类型，分为 home_page search_page sku_page category_page
   "cl_activity_child": "",                 // 上面的cl_activity对应的值，如果是sku_page, 这里就是sku的值
   "is_return": "1",                        // 是否是老客户，1代表老客户，0代表新客户
   "first_page": "0",                       // 用户访问网站的着陆页，1代表是着陆页，0代表不是着陆页
   "device_pixel_ratio": "1",               // 设备像素比例
   "resolution": "1366x768",                // 解析度，分辨率
   "color_depth": "24",                     // 色深
   "fid": "xxxx",                           // 广告id（唯一）
   "fec_source": "dddd",                    // 广告渠道
   "fec_medium": "",                        // 广告子渠道
   "fec_campaign": "",                      // 广告活动
   "fec_content": "",                       // 广告员
   "fec_design": "",                        // 广告图片设计员
   "fec_store": "fecshop.appfront.fancyecommerce.com",  // 电商系统当前的store
   "fec_lang": "en",                        // 电商系统当前的语言
   "fec_app": "appfront",                   // 电商系统当前的入口，譬如appfront，apphtml5appserver
   "fec_currency": "USD",                   // 电商系统当前的货币
   "category": "Men",                       // 如果是分类页面，这里是分类的name，否则为空，注意，这里的name是默认语言的name
   "sku": "",                               // 产品的sku
   "cart": [
        {
           "sku": "p10001-kahaki-xl",       // 购物车产品sku
           "qty": NumberLong(3),            // 购物车产品个数
           "price": 4.8                     // 购物车产品单价，注意是一个产品的价格，而且是默认货币
        },
        {
           "sku": "kilw0001",
           "qty": NumberLong(1),
           "price": 124 
        } 
    ],
    "search": {
        "text": "dress",                    // 搜索词
        "result_qty": NumberLong(5)         // 搜索该词，对应的产品个数
    },
    "order": {
        "invoice": "1100001840",                // 类型：string，订单号
        "order_type": "standard",               // 类型：string，订单支付类型：standard代表标准支付，express代表快捷支付，对于paypal在购物车页面直接点击paypal按钮进行的支付是express，其他的为标准支付standard
        "payment_status": "payment_pending",    // 类型：string，订单的支付状态， `payment_pending`代表未支付，该值为确定值，未支付订单payment_pending  ， 支付订单 payment_confirmed
        "payment_type": "paypal_standard",      // 类型：string，支付方式，也就是您的支付方式的名称，如果某种支付渠道有多种，譬如paypal有standard和express，请在名字区分开，譬如 paypal_standard， paypal_express，其他没有的，直接用名字即可，譬如alipay  
        "amount": 124,                          // 类型：Float， 订单的总额，这里的总额是您的电商系统的基础货币。
        "shipping": 0,                          // 类型：Float， 订单的运费，同上，基础货币
        "discount_amount": 0,                   // 类型：Float， 订单的优惠券折扣，同上，基础货币
        "coupon": "",                           // 类型：string，订单的优惠券
        "email": "2358269014@qq.com",           // 类型：string，下单者的邮箱
        "first_name": "terry",                  // 类型：string，下单者的first_name
        "last_name": "water",                   // 类型：string，下单者的last_name
        "city": "qingdao",                      // 类型：string，订单的收货地址 - 城市
        "zip": "434343",                        // 类型：string，订单的收货地址 - 邮编
        "country_code": "CN",                   // 类型：string，订单的收货地址 - 国家简码
        "state_code": "SD",                     // 类型：string，订单的收货地址 - 省简码
        "country_name": "China",                // 类型：string，订单的收货地址 - 国家全称
        "state_name": "山东省",                 // 类型：string，订单的收货地址 - 省全称
        "address1": "xx市xx镇",                 // 类型：string，订单的收货地址 - 详细街道地址1
        "address2": "",                         // 类型：string，订单的收货地址 - 详细街道地址2
        "products": [                           // 类型：Array， 订单的产品数组
            {
                "sku": "kilw0001",                                          // 类型：string，订单的产品sku
                "name": "Off-the-Shoulder Long Sleeve High-Low Day Dress",  // 类型：string，订单的产品name
                "qty": 5,                                                   // 类型：int，   订单的产品数量
                "price": 124                                                // 类型：float， 订单的产品单价，注意，这个是一个产品的价格
            },
            {
                "sku": "kxxw0601",
                "name": "sex sex Day Dress",
                "qty": NumberLong(5),
                "price": 64 
            }
        ] 
    },
    "login_email": "2358269014@qq.com",     // 登录email
    "register_email": "2358269014@qq.com",  // 注册email
    
}

```




















