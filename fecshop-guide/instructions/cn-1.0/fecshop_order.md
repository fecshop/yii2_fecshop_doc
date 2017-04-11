Fecshop 订单
=============

> fecshop 订单指的是在fecshop下单后的订单信息。

### 订单配置

#### 配置文件

为：`@common/config/fecshop_local_services/Order.php`，详细如下：

```
return [
	'order' => [
		'increment_id' => '1000000000', # 订单的格式。
		'requiredAddressAttr' => [ # 必填的订单字段。
			'first_name',
			'last_name',
			'email',
			'telephone',
			'street1',
			'country',
			'city',
			'state',
			'zip'
		],
		#处理多少分钟后，支付状态为pending的订单，归还库存。
		'minuteBeforeThatReturnPendingStock' 	=>  600,
		# 脚本一次性处理多少个pending订单。
		'orderCountThatReturnPendingStock' 		=>  30,
		# 订单状态配置
		'payment_status_pending' 				=> 'pending',		# 未付款
		'payment_status_processing' 			=> 'processing',	# 已付款
		'payment_status_canceled' 				=> 'canceled',		# 已取消
		'payment_status_complete' 				=> 'complete',		# 已完成
		'payment_status_holded' 				=> 'holded',		# hold
		'payment_status_suspected_fraud' 		=> 'suspected_fraud',#欺诈
		
	],
];
```

`increment_id` ：为订单编号格式

`requiredAddressAttr`： 为下单界面必填的字段

`minuteBeforeThatReturnPendingStock`： 这个是下面的后台脚本
（释放未付款订单库存的脚本）所用到的参数，将pending（未支付的订单）
的库存释放掉，这里的单位是分钟，如果您的库存为零库存（
零库存指的是，如果没有库存
可以通过采购部门采购，相当于您不需要考虑库存），可以不需要跑这个脚本。

`orderCountThatReturnPendingStock`： 这个后台脚本一次性处理多少个pending订单。

> **注意**：通过脚本将pending的库存返还给产品后，订单的状态将会变成取消状态，
> 订单取消状态，是无法进行支付的，因此，`minuteBeforeThatReturnPendingStock`
> 尽量设置的大一些，我设置的默认为10个小时，对于零库存商城
> （也就是产品库存为0没有关系，可以继续卖，然后采购部门去采购，这属于零库存模式），
> 这种模式可以批量将产品的所有库存设置的非常大，下面的这个脚本也不需要跑。
> ，下面的这个脚本就是根据上面设置的参数来处理pending状态订单，释放产品库存的脚本。


### 释放未付款订单库存的脚本

文件为： `@fecshop/shell/order/returnPendingProductQtyStock.sh`
，来与通过上面的参数`orderCountThatReturnPendingStock` 和
`minuteBeforeThatReturnPendingStock`来配置脚本的参数

### 订单支付状态的进一步验证

如果您感觉还是不放心，订单传递到erp进行发货处理的时候，加入一层付款成功验证，
譬如paypal，您可以去官方网站下载付款成功的订单，也就是csv表格
，然后通过导入的方式，二次验证订单支付状态，这样是最稳妥的方式，
另外还需要验证一下货币和金额。


### 下单后购物车的清空：

游客用户下单后，购物车是不清空的，支付成功后返回网站再清空购物车产品

登录用户下单后，购物车直接清空，用户可以在账户中心的我的订单中查看未支付订单，重新下单。


















