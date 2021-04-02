Fecmall-services服务部分
=============


> Fecmall Services 是fecmall核心部分，原理有点类似于yii2的组件，懒加载机制。


### Fecmall-services

fecmall的核心功能都是在services里面实现，开发者开发扩展插件，可以新建自己的services，
也可以重写已经存在的services，下面是一个services例子


1.配置例子：

```
'common' => [
    'enable' => true,
    // 公用层的具体配置下载下面
        'config' => [
            'services' => [
                'api' => [
                    'class' => 'fecerp\services\Api',
                ],
            ],
        ],
    ],
]
```

service一般在common里面进行配置，这样各个入口都可以使用services，不需要单独配置。

2.新建文件 @fecerp\services\Api 

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
namespace fecerp\services;

use Yii;
use yii\base\InvalidValueException;
use fecshop\services\Service;
/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class Api extends Service
{
	
	/*
		参数说明：  $url  为API访问的url
					$type 为请求类型，默认为get
					$data 为传递的数组数据
					$timeout 设置超时时间
		返回值：	返回API返回的数据
	*/
    /**
     * @param $url | string, 远程api url
     * @param $type | string, 类型
     * @param $data | array，curl传递的数据
     * @param $timeout | int，超时的时间
     */
	public function curlData($url, $type="get", $data=[], $timeout = 10)
    {
        //对空格进行转义
        $http_header = array();
        if(isset($data['access-token'])){
            $http_header[] = 'access-token: ' . $data['access-token'];
            unset($data['access-token']);
        }
        $url = str_replace(' ','+',$url);
        if($type == "get"){
            if(!empty($data) && is_array($data)){
                $arr = [];
                foreach($data as $k=>$v){
                    $arr[] = urlencode($k)."=".urlencode($v);
                }
                $str  = implode("&",$arr);
                if(strstr($url,"?")){
                    $url .= "&".$str;
                }else{
                    $url .= "?".$str;
                }
            }
        }
        $data = json_encode($data);
        $url = urldecode($url);
        //echo $url ;exit;
        $ch = curl_init();
        //设置选项，包括URL
        curl_setopt($ch, CURLOPT_URL, "$url");
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
        curl_setopt($ch, CURLOPT_HEADER, 0);
        curl_setopt($ch,CURLOPT_TIMEOUT,$timeout); 
        if($type == "post"){
            // POST数据
            curl_setopt($ch, CURLOPT_POST, 1);
            $http_header[] = 'Accept: application/json';
            $http_header[] = 'Content-Type: application/json';
            $http_header[] = 'Content-Length: ' . strlen($data);
            curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
            /*
            curl_setopt($ch, 
                CURLOPT_HTTPHEADER, 
                [
                'Accept: application/json',
                'Content-Type: application/json',
                'Content-Length: ' . strlen($data)
                ]
                );
            // 把post的变量加上
            curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
            */
        }
        curl_setopt($ch, CURLOPT_HTTPHEADER,$http_header);
        //执行并获取url地址的内容
        $output = curl_exec($ch);
        //echo $output ;
        //释放curl句柄
        curl_close($ch);
        //var_dump($output);exit;
        
        return $output;
    }
	
}
```

3.调用

```
Yii::$service->api->curlData($url);
```


service的使用比较简单，具体的基本原理需要您去阅读源码：https://github.com/fecshop/yii2_fecshop/blob/master/services/Service.php


这里只是讲述了services的简单使用，您开发扩展可以按照例子编写您自己的services，
建议开发者多阅读fecmall的一些services方法的代码。

service的使用非常的灵活，您可以通过配置新增和重写fecmall的services，
也可以对于同一个功能，实现多个services，譬如fecmall的search services，有mysql，mongodb，xunsearch，elasticSearch
多种实现，可以通过配置切换不同的搜索。


### 其他资料


[Fecmall 关于服务](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-service-abc.html)



[Fecmall 使用服务](http://www.fecmall.com/doc/fecshop-guide/develop/cn-2.0/guide-fecmall-service-use.html)


[Fecmall 关于block和services](http://www.fecmall.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_hand_block_services.html)


[fecmall 错误处理：model errors， helper errors services，以及page message services error处理](http://www.fecmall.com/topic/2558)






