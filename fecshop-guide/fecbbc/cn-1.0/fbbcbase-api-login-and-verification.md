Api 登录和验证
==================

> 对于需要用户登录这类安全认证的请求，需要先进行用户登录，获取token
> ，然后每次访问带上token，fecshop根据token做安全认证


### 用户登录

**Api获取Token**

> 请将下面url中出现 `http://enterprise.appapi.fecshop.com`的部分替换成您自己的域名

URL: `http://enterprise.appapi.fecshop.com/v2/account/login`

格式：`json`

方式：`post`

**Request JSON Data(Body)：**


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| username        | 必须        |   String    | 经销商的用户名|
| password        | 必须        |   String    | 经销商用户名对应的密码  |

**注意**：上面的username password是appadmin入口，也就是后台的用户名和密码



**Response JSON Data(Body)：**

格式：`json`

| 参数名称        | 是否必须    |  类型       |  描述        |
| ----------------| -----:      | :----:      |:----:        | 
| code            | 必须        |   Number    | 200 代表成功 |
| access-token    | 必须        |   String    | Token字符串  |

Example：`{"access-token":"QBwhbzKFewRzQp6lrerereqiZAw","code":200}`


### php 请求例子：

```
<?php

function getCurlData($url,$type="get",$data=array(),$timeout = 10) {
    //对空格进行转义
    $url = str_replace(' ','+',$url);
    if ($type == "get") {
        if (!empty($data) && is_array($data)) {
            $arr = [];
            foreach ($data as $k=>$v) {
                $arr[] = $k."=".urlencode($v);
            }
            $str = implode("&",$arr);
            if (strstr($url,"?")) {
                $url .= "&".$str;
            } else {
                $url .= "?".$str;
            }
        }
    }
	
    $data = json_encode($data);
    $ch   = curl_init();
    //设置选项，包括URL
    curl_setopt($ch, CURLOPT_URL, "$url");
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt($ch,CURLOPT_TIMEOUT,$timeout);  //定义超时3秒钟  
    if($type == "post"){
        // POST数据
        curl_setopt($ch, CURLOPT_POST, 1);
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
    }
    //执行并获取url地址的内容
    $output = curl_exec($ch);
    //echo $output ;
    //释放curl句柄
    curl_close($ch);
    //var_dump($output);exit;
    
    return $output;
}
$api_url = 'http://enterprise.appapi.fecshop.com/v2/account/login';
$post_data = [
    'username'     => 'username',
    'password'     => '12345678'
];
$return_data = getCurlData($api_url,'post',$post_data,100);
var_dump($return_data); 

?>
```

`{"access-token":"QBhb4zKFF6prrKRzQp6lM3h3MBo3qiZAw","code":200}`




### 用户验证

> 在上面步骤，通过登录api获取了access-token后，
> 我们在需要token验证的Api请求中，在request header中加入access-token即可，这样，就可以验证用户的合法性


### Request Header

| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| access-token      | 必须       |   String     | 身份验证，获取access-toekn参看上面的“用户登录”部分   |



### 用户验证-举例：

我们要访问这个url：http://enterprise.appapi.fecshop.com/v2/article/test

这个url是需要token验证的，下面是我们的示例代码，access-token是上面得到的，
直接填写到下面。

```
<?php
function getCurlData($url,$type="get",$data=array(),$timeout = 10) {
    //对空格进行转义
    $http_header = array();
    if(isset($data['access-token'])){
        $http_header[] = 'access-token: ' . $data['access-token'];
        unset($data['access-token']);
    }
    $url = str_replace(' ','+',$url);
    if ($type == "get") {
        if (!empty($data) && is_array($data)) {
            $arr = [];
            foreach ($data as $k=>$v) {
                $arr[] = $k."=".urlencode($v);
            }
            $str = implode("&",$arr);
            if (strstr($url,"?")) {
                $url .= "&".$str;
            } else {
                $url .= "?".$str;
            }
        }
    }
    
    $ch   = curl_init();
    curl_setopt($ch, CURLOPT_URL, "$url");
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt($ch,CURLOPT_TIMEOUT,$timeout);  //定义超时3秒钟
    if(strtolower($type) == "post"){
        $data = json_encode($data);
        // POST数据
        curl_setopt($ch, CURLOPT_POST, 1);
        $http_header[] = 'Accept: application/json';
        $http_header[] = 'Content-Type: application/json';
        $http_header[] = 'Content-Length: ' . strlen($data);

        // 把post的变量加上
        curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
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
$url = 'http://enterprise.appapi.fecshop.com/v1/article/test';
$data['access-token'] = "5mNtDqOQFodXHyS68hmUP3WdXw1TpJ-a";
$data['sku'] = "GMYR095-9";
$data['warehouse_name'] = "CN";
$data['country_code'] = "US";
$data['quarkscm_shipping_code'] = "RP";
$res = getCurlData($url,'post',$data);
echo $res;
?>


```


可以看到输出：(这个是测试请求，只是把用户post的数据返回回来)

```
{"sku":"GMYR095-9","warehouse_name":"CN","country_code":"US","quarkscm_shipping_code":"RP"}
```

