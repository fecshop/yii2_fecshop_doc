Mongo表索引
============


### 介绍

1.分库分表

按照时间进行分库，一天一个库

按照website_id进行分表，一个website一个表


2.新加计算字段：

`service_timestamp`: 服务器接收数据的时间戳

`service_datetime`: 服务器接收数据, 格式：Y-m-d H:i:s

`service_date`: 服务器接收数据, 格式：Y-m-d

`stay_seconds`: 通过两个相邻的uuid的`service_timestamp`，相减获得，查询uuid = 当前uuid && service_date = 当前的service_date

`uuid_first_page`:由于按照时间分库，站点分表，查询当前表，是否存在uuid，如果不存在，则 uuid_first_page = 1，否则 uuid_first_page = 0

`ip_first_page`: 这个暂时没有发现用处

`uuid_first_category`: 如果存在 uuid 和category，则查询是否存在，如果不存在，则为1，不存在则为0

`ip_first_category`: 暂无用处

`url_new`: 去掉某些参数后的url，譬如：

```
$var_names = [
    'utmsource',
    'cid',
    'aid',
    'mid',
    'affiliate',
    'click',
    'utm_source',
    'utm_medium',
    'utm_campaign',
    'utm_content',
    '_ga',
    'gclid',
];	
	$get['url_new'] = trimVar(removeqsvar($url, $var_names));
```

`search_login_email`: 

```
            where([
				'uuid'=>$one['uuid'],
				'login_email'=>['$exists' => true]
			])
```


1.
```
function removeqsvar($url, $var_names) {
	foreach($var_names as $param){
		$url = preg_replace('/([?&])'.$param.'=[^&]+(&|$)/','$1',$url);
	}
	return $url;
}
```

2.去掉特殊字符，去除大约350的字符

```
function trimVar($url){
	$url = trim($url,"?");
	$url = trim($url,"#");
	$url = trim($url,"&");
	$url = trim($url,"/");
	$url_length = strlen($url);
	# 如果url大约350，那么只取350内的url字符
	if($url_length > 350){
		$url = substr($url,0,350);
	}
	return $url;
}
```


`first_visit_this_url`：如果存在 uuid 和category

索引：

`order.invoice`: 用于在接收数据部分，更新订单的支付状态

`uuid, service_date, _id`: 用于计算 stay_seconds 的值，查询uuid = 当前uuid && service_date = 当前的service_date， _id倒序 ，取一个值，然后查看时间间隔





需要加的索引

1.按照website分表

索引：
order.invoice: