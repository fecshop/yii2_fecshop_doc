Fecyo 微信公众号自定义菜单
==============


> 您可以在fecmall后台，进行微信公众号的菜单自定义


### 微信自定义菜单

为了微信关注公众号登陆，在公众管理平台设置了`服务器配置`, 用来接收微信服务器的消息通知，设置后，
将导致在微信公众管理平台将无法设置`自定义菜单`, 只能通过接口设置，因此fecmall加入了该功能

微信自定义菜单文档地址：https://developers.weixin.qq.com/doc/offiaccount/Custom_Menus/Creating_Custom-Defined_Menu.html


`网站配置` --> `基础配置` --> `Fecphone config`    ， 在配置底部可以看到一个文本框`微信- 自定义菜单`

注意: 您需要先保存微信的`appid`  `appsecret`等设置保存后，然后重新打开编辑`微信自定义菜单`。


example:


```

{
	"button": [{
			"type": "view",
			"name": "官网",
			"url": "http://www.fecmall.com/"
		},
		{
			"name": "产品",
			"sub_button": [{
					"type": "view",
					"name": "开源系统",
					"url": "http://www.fecmall.com/fecmall"
				},
				{
					"type": "view",
					"name": "多商户系统",
					"url": "http://www.fecmall.com/fecbbc"
				},
				{
					"type": "view",
					"name": "多商户分销",
					"url": "http://www.fecmall.com/fecbdc"
				},
				{
					"type": "view",
					"name": "分销商城演示",
					"url": "http://fecbdch5.fecshop.com/cn"
				}


			]
		},
		{
			"name": "文档",
			"sub_button": [{
					"type": "view",
					"name": "开发文档",
					"url": "http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-README.html"
				},
				{
					"type": "view",
					"name": "帮助文档",
					"url": "http://www.fecmall.com/doc/fecshop-guide/instructions/cn-2.0/guide-README.html"
				},
				{
					"type": "view",
					"name": "应用市场",
					"url": "http://www.fecmall.com/doc/fecshop-guide/addons/cn-2.0/guide-README.html"
				},


				{
					"type": "view",
					"name": "多商户文档",
					"url": "http://www.fecmall.com/doc/fecmall-guide/instructions/cn-1.0/guide-README.html"
				},
				{
					"type": "view",
					"name": "多商户分销",
					"url": "http://www.fecmall.com/doc/fecmall-guide/fecbdc/cn-1.0/guide-README.html"
				}




			]
		}
	]
}



```


保存，查看您的公众号即可，需要注意的是，微信公众号存在缓存，你需要先`不关注公众号`，然后`重新关注公众号`，才能看到`自定义菜单`变化


























