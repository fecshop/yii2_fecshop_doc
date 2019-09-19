Fecmall Log日志
==============

> fecmall的log实现，使用的是Yii2的log机制来实现的

1.日志配置 `@app/config/main.php` 打开后，可以看到log组件的配置如下：

```
'log' =>[  
	# 追踪级别  
	# 消息跟踪级别  
	# 在开发的时候，通常希望看到每个日志消息来自哪里。这个是能够被实现的，通过配置 log 组件的 yii\log\Dispatcher::traceLevel 属性， 就像下面这样：  
	'traceLevel' => 3,  
	  
	# 通过 yii\log\Logger 对象，日志消息被保存在一个数组里。为了这个数组的内存消耗， 当数组积累了一定数量的日志消息，日志对象每次都将刷新被记录的消息到 log targets 中。 你可以通过配置 log 组件的 yii\log\Dispatcher::flushInterval 属性来自定义数量  
	'flushInterval' => 1,  
	  
	'targets' => [  
		'file' =>[  
			//'levels' => ['trace'],  
			'categories' => ['fecshop_debug'],  
			'class' => 'yii\log\FileTarget',  
			# 当 yii\log\Logger 对象刷新日志消息到 log targets 的时候，它们并 不能立即获取导出的消息。相反，消息导出仅仅在一个日志目标累积了一定数量的过滤消息的时候才会发生。你可以通过配置 个别的 log targets 的 yii\log\Target::exportInterval 属性来 自定义这个数量，就像下面这样：  
			'exportInterval' => 1,  
			# 输出文件  
			'logFile' => '@apphtml5/runtime/fecshop_logs/fecshop_debug.log',  
			# 你可以通过配置 yii\log\Target::prefix 的属性来自定义格式，这个属性是一个PHP可调用体返回的自定义消息前缀  
			'prefix' => function ($message) {  
				return $message;  
			},  
			# 除了消息前缀以外，日志目标也可以追加一些上下文信息到每组日志消息中。 默认情况下，这些全局的PHP变量的值被包含在：$_GET, $_POST, $_FILES, $_COOKIE,$_SESSION 和 $_SERVER 中。 你可以通过配置 yii\log\Target::logVars 属性适应这个行为，这个属性是你想要通过日志目标包含的全局变量名称。 举个例子，下面的日志目标配置指明了只有 $_SERVER 变量的值将被追加到日志消息中。  
			# 你可以将 logVars 配置成一个空数组来完全禁止上下文信息包含。或者假如你想要实现你自己提供上下文信息的方式， 你可以重写 yii\log\Target::getContextMessage() 方法。  
			 'logVars' => [],  
		],  
	],  
],
```

如果要开启log，可以把注释去掉，查看
`'logFile' => '@apphtml5/runtime/fecshop_logs/fecshop_debug.log',`
对应的文件是否存在，如果不存在，需要新建文件 fecshop_debug.log
，并设置可写即可完成配置。

2.日志的使用

```
\Yii::info($post_log,'fecshop_debug');
```

其中第二个参数  `fecshop_debug` 对应上面的配置 
`'categories' => ['fecshop_debug'],`

您可以定义多个 `targets` 每个targets的`categories` 不同，然后在输出的时候做区分
就可以把日志写入到不同的log文件里面了

[Yii2 Log的特性](http://www.fancyecommerce.com/2017/05/18/yii2-log-%E7%89%B9%E6%80%A7/)

通过上面的特性，可以知道log在使用过程中的一些情况，log的配置以及log
文件如果存在问题，调用log的函数`\Yii::info($post_log,'fecshop_debug')`
不会卡住，会继续执行。

fecshop 代码里面会加入一些log的代码，在线上环境中可以把 fecshop_debug 对应的配置去掉
就不会输出log，您可以自定义一些log的配置，然后做自定义log的输出。


关于Yii Log更多的资料可以参阅：  [Yii Log](http://www.yiichina.com/doc/guide/2.0/runtime-logging)












































