Fecshop Mysql 数据库介绍
=========================

> Fecshop Mysql数据库的介绍部分


### Fecshop Mysql 前端数据表：

表： article

> 用于前端页面的page单页，可以后台进行编辑，譬如：https://fecshop.appfront.fancyecommerce.com/about-us

```
`id` int(11) NOT NULL AUTO_INCREMENT,
`url_key` varchar(255) DEFAULT NULL COMMENT 'url的path部分，属于自定义url部分，譬如上面的链接，对用的值为`/about-us` ',
`title` text COMMENT 'page页的标题',
`meta_keywords` text COMMENT 'meta关键字',
`meta_description` text,
`content` text COMMENT 'page 内容部分',   
`status` int(5) DEFAULT '1' COMMENT '1代表激活，2代表关闭',
`created_at` int(10) DEFAULT NULL,
`updated_at` int(10) DEFAULT NULL,
`created_user_id` int(20) DEFAULT NULL COMMENT '后台编辑用户的id',
PRIMARY KEY (`id`)
```




表： customer

> 用户信息表，存储前端用户的账户密码等信息。

```
 `id` int(20) unsigned NOT NULL AUTO_INCREMENT,
  `password_hash` varchar(80) DEFAULT NULL COMMENT '密码',
  `password_reset_token` varchar(60) DEFAULT NULL COMMENT '密码token',
  `email` varchar(60) DEFAULT NULL COMMENT '邮箱',
  `firstname` varchar(100) DEFAULT NULL,
  `lastname` varchar(100) DEFAULT NULL,
  `is_subscribed` int(5) NOT NULL DEFAULT '2' COMMENT '1代表订阅，2代表不订阅邮件',
  `auth_key` varchar(60) DEFAULT NULL,
  `status` int(5) DEFAULT NULL COMMENT '状态',
  `created_at` int(18) DEFAULT NULL COMMENT '创建时间',
  `updated_at` int(18) DEFAULT NULL COMMENT '更新时间',
  `password` varchar(50) DEFAULT NULL COMMENT '密码',
  `access_token` varchar(60) DEFAULT NULL,
  `birth_date` datetime DEFAULT NULL COMMENT '出生日期',
  `favorite_product_count` int(15) NOT NULL DEFAULT '0' COMMENT '用户收藏的产品的总数',
  `type` varchar(35) DEFAULT 'default' COMMENT '默认为default，如果是第三方登录，譬如google账号登录注册，那么这里的值为google',
  `access_token_created_at` int(20) DEFAULT NULL COMMENT '创建token的时间',
  `allowance` int(20) DEFAULT NULL COMMENT '限制次数访问',
  `allowance_updated_at` int(20) DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `access_token` (`access_token`)
```

表： customer_address

> 用户的收货地址表，用户下订单的时候可以从该表取出来数据直接使用
> ，该表和customer表是一对多的关系，

```
`address_id` int(15) NOT NULL AUTO_INCREMENT,
  `first_name` varchar(150) DEFAULT NULL COMMENT '收货地址的姓',
  `email` varchar(155) DEFAULT NULL COMMENT '邮箱地址',
  `last_name` varchar(150) DEFAULT NULL COMMENT '名',
  `company` varchar(255) DEFAULT NULL COMMENT '公司',
  `telephone` varchar(100) DEFAULT NULL COMMENT '电话',
  `fax` varchar(150) DEFAULT NULL COMMENT '传真',
  `street1` text COMMENT '街道地址1',
  `street2` varchar(255) DEFAULT NULL COMMENT '街道地址2',
  `city` varchar(150) DEFAULT NULL COMMENT '城市',
  `state` varchar(255) DEFAULT NULL COMMENT '省/州',
  `zip` varchar(50) DEFAULT NULL COMMENT '邮编',
  `country` varchar(50) DEFAULT NULL COMMENT '国家',
  `customer_id` int(20) DEFAULT NULL COMMENT 'customer表的id',
  `created_at` int(20) DEFAULT NULL COMMENT '创建时间戳',
  `updated_at` int(20) DEFAULT NULL COMMENT '更新时间戳',
  `is_default` int(11) NOT NULL DEFAULT '2' COMMENT '1代表是默认地址，2代表不是',
  PRIMARY KEY (`address_id`)
```

表： ipn_message (已经废弃的表)

```
`ipn_id` int(15) unsigned NOT NULL AUTO_INCREMENT,
  `txn_id` varchar(20) DEFAULT NULL COMMENT 'transaction id',
  `payment_status` varchar(20) DEFAULT NULL COMMENT '支付状态',
  `updated_at` int(15) DEFAULT NULL COMMENT '更新时间',
  PRIMARY KEY (`ipn_id`)
```

表： migration

> 这个是用于mysql Yii2 migration的表，关于migration，可以参看：http://www.yiichina.com/doc/guide/2.0/db-migrations

```
 `version` varchar(180) NOT NULL,
  `apply_time` int(11) DEFAULT NULL,
  PRIMARY KEY (`version`)
```

表： product_custom_option_qty

> 产品custom option类型产品对应的库存信息

```
  `id` int(20) NOT NULL AUTO_INCREMENT,
  `product_id` varchar(50) NOT NULL COMMENT '产品id',
  `custom_option_sku` varchar(50) NOT NULL COMMENT '产品自定义属性sku',
  `qty` int(20) NOT NULL COMMENT '产品个数。',
  PRIMARY KEY (`id`),
```
表： product_flat_qty

> 产品库存表

```
  `id` int(20) NOT NULL AUTO_INCREMENT,
  `product_id` varchar(50) NOT NULL COMMENT '产品表的id',
  `qty` int(20) NOT NULL COMMENT '产品表的个数',
  PRIMARY KEY (`id`),
  UNIQUE KEY `product_id` (`product_id`)
```

表： sales_coupon

> 优惠券表

```
  `coupon_id` int(15) unsigned NOT NULL AUTO_INCREMENT,
  `created_at` int(15) DEFAULT NULL COMMENT '创建时间',
  `updated_at` int(15) DEFAULT NULL COMMENT '更新时间',
  `created_person` int(15) NOT NULL COMMENT '创建人的id',
  `coupon_name` varchar(100) DEFAULT NULL COMMENT '优惠劵名称',
  `coupon_description` varchar(255) DEFAULT NULL COMMENT '优惠劵描述',
  `coupon_code` varchar(100) DEFAULT NULL COMMENT '优惠劵编号',
  `expiration_date` int(15) DEFAULT NULL COMMENT '过期时间',
  `users_per_customer` int(15) DEFAULT '0' COMMENT '优惠劵被每个客户使用的最大次数',
  `times_used` int(15) DEFAULT '0' COMMENT '优惠劵被使用了多少次',
  `type` int(5) DEFAULT NULL COMMENT '优惠劵的类型，1代表按照百分比对产品打折，2代表在总额上减少多少',
  `conditions` int(15) DEFAULT NULL COMMENT '优惠劵使用的条件，如果类型为1，则没有条件，如果类型是2，则购物车中产品总额满足多少的时候进行打折。这里填写的是美元金额',
  `discount` int(15) DEFAULT NULL COMMENT '优惠劵的折扣，如果类型为1，这里填写的是百分比，如果类型是2，这里代表的是在总额上减少的金额，货币为美金',
  PRIMARY KEY (`coupon_id`),
```


表： sales_coupon_usage

优惠券使用记录表

```
 `id` int(15) NOT NULL AUTO_INCREMENT,
  `coupon_id` int(25) DEFAULT '0' COMMENT '客户id',
  `customer_id` int(25) DEFAULT '0' COMMENT '客户id',
  `times_used` int(15) DEFAULT '0' COMMENT '使用次数',
  PRIMARY KEY (`id`),
  KEY `coupon_id` (`coupon_id`),
  KEY `customer_id` (`customer_id`)
```

表： sales_flat_cart

> 购物车表

```
`cart_id` int(15) unsigned NOT NULL AUTO_INCREMENT,
  `store` varchar(100) DEFAULT NULL COMMENT 'store name',
  `created_at` int(15) DEFAULT NULL COMMENT '创建时间',
  `updated_at` int(15) DEFAULT NULL COMMENT '更新时间',
  `items_count` int(10) DEFAULT '0' COMMENT '购物车中产品的总个数，默认为0个',
  `customer_id` int(15) DEFAULT NULL COMMENT '客户id',
  `customer_email` varchar(90) DEFAULT NULL COMMENT '客户邮箱',
  `customer_firstname` varchar(50) DEFAULT NULL COMMENT '客户名字',
  `customer_lastname` varchar(50) DEFAULT NULL COMMENT '客户名字',
  `customer_is_guest` int(5) DEFAULT NULL COMMENT '是否是游客，1代表是游客，2代表不是游客',
  `remote_ip` varchar(26) DEFAULT NULL COMMENT 'ip地址',
  `coupon_code` varchar(20) DEFAULT NULL COMMENT '优惠劵',
  `payment_method` varchar(20) DEFAULT NULL COMMENT '支付方式',
  `shipping_method` varchar(20) DEFAULT NULL COMMENT '货运方式',
  `customer_telephone` varchar(25) DEFAULT NULL COMMENT '客户电话',
  `customer_address_id` int(20) DEFAULT NULL COMMENT '客户地址id',
  `customer_address_country` varchar(50) DEFAULT NULL COMMENT '客户国家',
  `customer_address_state` varchar(50) DEFAULT NULL COMMENT '客户省',
  `customer_address_city` varchar(50) DEFAULT NULL COMMENT '客户市',
  `customer_address_zip` varchar(20) DEFAULT NULL COMMENT '客户zip',
  `customer_address_street1` text COMMENT '客户街道地址1',
  `customer_address_street2` text COMMENT '客户街道地址2',
  `app_name` varchar(20) DEFAULT NULL COMMENT '属于哪个app',
  PRIMARY KEY (`cart_id`),
  KEY `customer_id` (`customer_id`),
  KEY `customer_email` (`customer_email`)
```


表： sales_flat_cart_item

> 购物车产品表
```
`item_id` int(15) unsigned NOT NULL AUTO_INCREMENT,
  `store` varchar(100) DEFAULT NULL COMMENT 'store name',
  `cart_id` int(15) DEFAULT NULL,
  `created_at` int(15) DEFAULT NULL COMMENT '创建时间',
  `updated_at` int(15) DEFAULT NULL COMMENT '更新时间',
  `product_id` varchar(100) DEFAULT NULL COMMENT '产品id',
  `qty` int(10) DEFAULT NULL COMMENT '个数',
  `custom_option_sku` varchar(50) DEFAULT NULL COMMENT '产品的自定义属性',
  PRIMARY KEY (`item_id`),
  KEY `quote_id` (`cart_id`)
```

表： sales_flat_order

> 订单表

```
`order_id` int(15) unsigned NOT NULL AUTO_INCREMENT,
  `increment_id` varchar(25) DEFAULT NULL COMMENT '递增个数',
  `order_status` varchar(80) DEFAULT NULL COMMENT '订单状态',
  `store` varchar(100) DEFAULT NULL COMMENT 'store name',
  `created_at` int(15) DEFAULT NULL COMMENT '创建时间',
  `updated_at` int(15) DEFAULT NULL COMMENT '更新时间',
  `items_count` int(10) DEFAULT '0' COMMENT '订单中产品的总个数，默认为0个',
  `total_weight` decimal(12,2) DEFAULT '0.00' COMMENT '总重量',
  `order_currency_code` varchar(10) DEFAULT NULL COMMENT '当前货币',
  `order_to_base_rate` decimal(12,4) DEFAULT NULL COMMENT '当前货币和默认货币的比率',
  `grand_total` decimal(12,2) DEFAULT NULL COMMENT '当前订单的总额',
  `base_grand_total` decimal(12,2) DEFAULT NULL COMMENT '当前订单的默认货币总额',
  `subtotal` decimal(12,2) DEFAULT NULL COMMENT '当前订单的产品总额',
  `base_subtotal` decimal(12,2) DEFAULT NULL COMMENT '当前订单的产品默认货币总额',
  `subtotal_with_discount` decimal(12,2) DEFAULT NULL COMMENT '当前订单的去掉的总额',
  `base_subtotal_with_discount` decimal(12,2) DEFAULT NULL COMMENT '当前订单的去掉的默认货币总额',
  `is_changed` int(5) DEFAULT '1' COMMENT '是否change，1代表是，2代表否',
  `checkout_method` varchar(20) DEFAULT NULL COMMENT 'guest，register，代表是游客还是登录客户。',
  `customer_id` int(15) DEFAULT NULL COMMENT '客户id',
  `customer_group` varchar(20) DEFAULT NULL COMMENT '客户组id',
  `customer_email` varchar(90) DEFAULT NULL COMMENT '客户邮箱',
  `customer_firstname` varchar(50) DEFAULT NULL COMMENT '客户名字',
  `customer_lastname` varchar(50) DEFAULT NULL COMMENT '客户名字',
  `customer_is_guest` int(5) DEFAULT NULL COMMENT '是否是游客，1代表是游客，2代表不是游客',
  `remote_ip` varchar(26) DEFAULT NULL COMMENT 'ip地址',
  `coupon_code` varchar(20) DEFAULT NULL COMMENT '优惠劵',
  `payment_method` varchar(20) DEFAULT NULL COMMENT '支付方式',
  `shipping_method` varchar(20) DEFAULT NULL COMMENT '货运方式',
  `shipping_total` decimal(12,2) DEFAULT NULL COMMENT '运费总额',
  `base_shipping_total` decimal(12,2) DEFAULT NULL COMMENT '默认货币运费总额',
  `customer_telephone` varchar(25) DEFAULT NULL COMMENT '客户电话',
  `customer_address_country` varchar(50) DEFAULT NULL COMMENT '客户国家',
  `customer_address_state` varchar(50) DEFAULT NULL COMMENT '客户省',
  `customer_address_city` varchar(50) DEFAULT NULL COMMENT '客户市',
  `customer_address_zip` varchar(20) DEFAULT NULL COMMENT '客户zip',
  `customer_address_street1` text COMMENT '客户地址1',
  `customer_address_street2` text COMMENT '客户地址2',
  `order_remark` text COMMENT '订单的备注信息，有买家填写提交',
  `txn_type` varchar(20) DEFAULT NULL COMMENT 'Transaction类型，是在购物车点击支付按钮下单，还是在下单页面填写完货运地址信息下单',
  `txn_id` varchar(30) DEFAULT NULL COMMENT 'Transaction Id 支付平台唯一交易号,通过这个可以在第三方支付平台查找订单',
  `payer_id` varchar(30) DEFAULT NULL COMMENT '它是特定PayPal帐户的外部唯一标识符',
  `ipn_track_id` varchar(20) DEFAULT NULL,
  `receiver_id` varchar(20) DEFAULT NULL,
  `verify_sign` varchar(80) DEFAULT NULL,
  `charset` varchar(20) DEFAULT NULL,
  `payment_fee` decimal(12,2) DEFAULT NULL COMMENT '交易服务费',
  `payment_type` varchar(20) DEFAULT NULL COMMENT '交易类型',
  `correlation_id` varchar(20) DEFAULT NULL COMMENT '相关id，快捷支付里面的字段',
  `base_payment_fee` decimal(12,2) DEFAULT NULL COMMENT '交易费用，基础货币值，通过货币进行的转换',
  `protection_eligibility` varchar(20) DEFAULT NULL COMMENT '保护资格，快捷支付里面的字段',
  `protection_eligibility_type` varchar(255) DEFAULT NULL COMMENT '保护资格类型，快捷支付里面的字段',
  `secure_merchant_account_id` varchar(20) DEFAULT NULL COMMENT '商人账户安全id',
  `build` varchar(20) DEFAULT NULL COMMENT 'build',
  `paypal_order_datetime` datetime DEFAULT NULL COMMENT '订单创建，Paypal时间',
  `theme_type` int(5) DEFAULT NULL COMMENT '1-pc,2-mobile',
  `if_is_return_stock` int(5) NOT NULL DEFAULT '2' COMMENT '1,代表订单归还了库存，2代表订单没有归还库存，此状态作用：用来标示pending订单是否释放产品库存',
  `payment_token` varchar(255) DEFAULT NULL COMMENT '支付过程中使用的token，譬如paypal express支付',
  `version` int(5) NOT NULL DEFAULT '0' COMMENT '订单支付成功后，需要更改订单状态和扣除库存，为了防止多次执行扣除库存，进而使用版本号，默认为0，执行一次更改订单状态为processing，则累加1，执行完查询version是否为1，如果不为1，则说明执行过了，事务则回滚。',
  PRIMARY KEY (`order_id`),
  KEY `customer_id` (`customer_id`),
  KEY `oupload_at_order_status` (`updated_at`,`order_status`,`if_is_return_stock`),
  KEY `payment_token` (`payment_token`)
```

表： sales_flat_order_item

订单产品表

```
`item_id` int(15) unsigned NOT NULL AUTO_INCREMENT,
  `store` varchar(100) DEFAULT NULL COMMENT 'store name',
  `order_id` int(15) DEFAULT NULL COMMENT '产品对应的订单表id',
  `created_at` int(16) DEFAULT NULL COMMENT '创建时间',
  `updated_at` int(16) DEFAULT NULL COMMENT '更新时间',
  `product_id` varchar(100) DEFAULT NULL COMMENT '产品id',
  `sku` varchar(100) DEFAULT NULL,
  `name` varchar(255) DEFAULT NULL,
  `custom_option_sku` varchar(50) DEFAULT NULL COMMENT '自定义属性',
  `image` varchar(255) DEFAULT NULL COMMENT '图片',
  `weight` decimal(12,2) DEFAULT NULL COMMENT '重量',
  `qty` int(10) DEFAULT NULL COMMENT '个数',
  `row_weight` decimal(12,2) DEFAULT NULL COMMENT '一个产品重量*个数',
  `price` decimal(12,2) DEFAULT NULL COMMENT '产品价格',
  `base_price` decimal(12,2) DEFAULT NULL COMMENT '默认货币价格',
  `row_total` decimal(12,2) DEFAULT NULL COMMENT '一个产品价格*个数',
  `base_row_total` decimal(12,2) DEFAULT NULL COMMENT '一个产品默认货币价格*个数',
  `redirect_url` varchar(200) DEFAULT NULL COMMENT '产品url',
  PRIMARY KEY (`item_id`),
  KEY `order_id` (`order_id`)
```

表： session_storage

> appserver 接口端实现的一个类似session的功能，记录在数据库中。

```
  `id` int(20) NOT NULL AUTO_INCREMENT,
  `uuid` varchar(200) DEFAULT NULL COMMENT '用户唯一标示',
  `key` varchar(200) DEFAULT NULL COMMENT 'session key',
  `value` text COMMENT 'session value',
  `timeout` int(20) DEFAULT NULL COMMENT '超时时间，秒',
  `updated_at` int(20) DEFAULT NULL COMMENT '创建时间',
  PRIMARY KEY (`id`),
  KEY `uuid` (`uuid`,`key`)
```


表： static_block

> html块，一般用于业务经常需要改动的部分，譬如首页的大图等，
> 在数据库中保存，易于编辑

```
`id` int(11) NOT NULL AUTO_INCREMENT,
  `identify` varchar(100) DEFAULT NULL,
  `title` text,
  `status` int(5) DEFAULT NULL,
  `content` text,
  `created_at` int(11) DEFAULT NULL,
  `updated_at` int(11) DEFAULT NULL,
  `created_user_id` int(20) DEFAULT NULL,
```
表： url_rewrite

> url重写信息存储的表

```
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `type` varchar(50) DEFAULT NULL COMMENT '类型',
  `custom_url_key` varchar(255) DEFAULT NULL COMMENT '自定义url key',
  `origin_url` varchar(255) DEFAULT NULL COMMENT '原来的url ',
  PRIMARY KEY (`id`)
```


表： admin_config

> 后台配置部分存储的表

```
`id` int(20) NOT NULL AUTO_INCREMENT,
  `label` varchar(150) DEFAULT NULL,
  `key` varchar(255) DEFAULT NULL,
  `value` varchar(2555) DEFAULT NULL,
  `description` varchar(255) DEFAULT NULL,
  `created_at` datetime DEFAULT NULL,
  `updated_at` datetime DEFAULT NULL,
  `created_person` varchar(150) DEFAULT NULL,
  PRIMARY KEY (`id`)
```

表： admin_menu

> 后台菜单表

```
`id` int(15) NOT NULL AUTO_INCREMENT,
  `name` varchar(150) DEFAULT NULL,
  `level` int(5) DEFAULT NULL,
  `parent_id` int(15) DEFAULT NULL,
  `url_key` varchar(255) DEFAULT NULL,
  `role_key` varchar(150) DEFAULT NULL COMMENT '权限key，也就是controller的路径，譬如/fecadmin/menu/managere,controller 是MenuController，当前的值为：/fecadmin/menu',
  `created_at` datetime DEFAULT NULL,
  `updated_at` datetime DEFAULT NULL,
  `sort_order` int(10) NOT NULL DEFAULT '0',
  `can_delete` int(5) DEFAULT '2' COMMENT '是否可以被删除，1代表不可以删除，2代表可以删除',
  PRIMARY KEY (`id`)
```

表： admin_role

> 后台权限组表

```
  `role_id` int(15) NOT NULL AUTO_INCREMENT,
  `role_name` varchar(100) DEFAULT NULL COMMENT '权限名字',
  `role_description` varchar(255) DEFAULT NULL COMMENT '权限描述',
  PRIMARY KEY (`role_id`)
```

表： admin_role_menu

> 后台权限组和菜单对应表

```
  `id` int(15) NOT NULL AUTO_INCREMENT,
  `menu_id` int(15) NOT NULL,
  `role_id` int(15) NOT NULL,
  `created_at` datetime DEFAULT NULL,
  `updated_at` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
```

表： admin_user

> 后台用户表

```
  `id` int(20) unsigned NOT NULL AUTO_INCREMENT,
  `username` varchar(50) DEFAULT NULL COMMENT '用户名',
  `password_hash` varchar(80) DEFAULT NULL COMMENT '密码',
  `password_reset_token` varchar(60) DEFAULT NULL COMMENT '密码token',
  `email` varchar(60) DEFAULT NULL COMMENT '邮箱',
  `person` varchar(100) DEFAULT NULL COMMENT '用户姓名',
  `code` varchar(100) DEFAULT NULL,
  `auth_key` varchar(60) DEFAULT NULL,
  `status` int(5) DEFAULT NULL COMMENT '状态',
  `created_at` int(18) DEFAULT NULL COMMENT '创建时间',
  `updated_at` int(18) DEFAULT NULL COMMENT '更新时间',
  `password` varchar(50) DEFAULT NULL COMMENT '密码',
  `access_token` varchar(60) DEFAULT NULL,
  `access_token_created_at` int(20) DEFAULT NULL COMMENT 'access token 的创建时间，格式为Int类型的时间戳',
  `allowance` int(20) DEFAULT NULL,
  `allowance_updated_at` int(20) DEFAULT NULL,
  `created_at_datetime` datetime DEFAULT NULL,
  `updated_at_datetime` datetime DEFAULT NULL,
  `birth_date` datetime DEFAULT NULL COMMENT '出生日期',
  PRIMARY KEY (`id`),
  UNIQUE KEY `username` (`username`),
  UNIQUE KEY `access_token` (`access_token`)
```

表： admin_user_role

> 后台用户和权限组对应表

```
 `id` int(20) NOT NULL AUTO_INCREMENT,
  `user_id` int(30) NOT NULL,
  `role_id` int(30) NOT NULL,
  PRIMARY KEY (`id`)
```

表： admin_visit_log

> 后台用户访问记录表

```
  `id` int(15) NOT NULL AUTO_INCREMENT,
  `account` varchar(25) DEFAULT NULL COMMENT '操作账号',
  `person` varchar(25) DEFAULT NULL COMMENT '操作人姓名',
  `created_at` datetime DEFAULT NULL COMMENT '操作时间',
  `menu` varchar(100) DEFAULT NULL COMMENT '菜单',
  `url` text COMMENT 'URL',
  `url_key` varchar(150) DEFAULT NULL COMMENT '参数',
  PRIMARY KEY (`id`)
```
