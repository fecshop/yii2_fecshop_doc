Fecshop Url自定义
=================

> url 自定义，指的是你可以通过任意的字符串定义当前的页面的url，
保存您的配置后，访问您自定义的url，就会跳转到你设置的页面，这个是为了seo的考虑
，让url中含有当前页面的字符串。
重写url表的存储，可以使用mysql和mongodb两种，您可以通过
配置来进行设置。

### fecshop url 自定义的原理：

- 在数据库中存储url对应关系，也就是重写后的自定义url 对应 一个原来的url。

- fecshop系统初始化url的时候，首先访问数据库，查找对应关系，如果找到，返回对应的 原来url地址，做后续的处理。

### 1.数据库中存储url

通过表url_rewrite 来保存url的对应关系，譬如 /cms/home/index?id=16 对应
/fashion-handbag-women.html，这样在表中就有一个一组关系的对应，
这个功能是由fecshop的url服务完成的。


**配置**：可以通过 url服务的配置来设置存储方式，和随机字符串的个数。
在@fecshop\config\services\Url.php 中的配置：

```php
'url' => [
	'class' 	=> 'fecshop\services\Url',
	'storage'	=> 'mongodb',  # 'mongodb or mysqldb'
	'randomCount'=> 8,  # if url key  is exist in url write table ,  add a random string  behide the url key, this param is define random String length
],
```

- 参数[[storage]]：设置url rewrite表 使用mongodb还是mysql，本功能目前支持双数据库，您可以选择一个数据库来存储，当您选择后，
在线上开始运营后，请不要轻易改变，因为由mysqldb变成mongodb后，在mongodb的url_write表中是不存在mysql存储的自定义url的，如果您坚持要这么做，
您需要想办法，把mysql的自定义url，插入到mongodb的表中。
- 参数[[randomCount]]：设置生成的随机字符串的个数，当url存在重复，或者 字符串过滤后（字符串生成url，需要过滤去一些特殊字符）为空等情况，都会使用到随机数字，来实现自定义url的唯一性。
譬如，在自定义url表中存在了一个自定义url, fashion-hand-bag， 如果你
继续自定义url为fashion-hand-bag，系统会在后面加入一些随机数字，
fashion-hand-bag-23943828 ，来实现自定义url的唯一性。

**对应关系**：自定义url和原来的url的对应关系是由url服务完成的，
url服务的全部代码如下：

```

<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */
namespace fecshop\services;
use Yii;
use yii\base\InvalidValueException;
use yii\base\InvalidConfigException;
use yii\base\BootstrapInterface;
use fec\helpers\CUrl;
/**
 * 
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class Url extends Service 
{
	public 	  $randomCount = 8;
	
	protected $_secure;
	protected $_currentBaseUrl;
	protected $_origin_url;
	protected $_httpType;
	protected $_httpBaseUrl;
	protected $_httpsBaseUrl;
	
	/**
	 * save custom url to mongodb collection url_rewrite
	 * @param $str|String, example:  fashion handbag women
	 * @param $originUrl|String , origin url ,example: /cms/home/index?id=5
	 * @param $originUrlKey|String,origin url key, it can be empty ,or generate by system , or custom url key.
	 * @param $type|String, url rewrite type.
	 * @return  rewrite Key. 
	 */
	public function saveRewriteUrlKeyByStr($str,$originUrl,$originUrlKey,$type='system'){
		$originUrl = $originUrl ? '/'.trim($originUrl,'/') : '';
		$originUrlKey = $originUrlKey ? '/'.trim($originUrlKey,'/') : '';
		if($originUrlKey){
			/**
			 * if originUrlKey and  originUrl is exist in url rewrite collectons.
			 */
			$model = $this->find();
			$data = $model->where([
				'custom_url_key' 	=> $originUrlKey,
				'origin_url' 		=> $originUrl,
			])->asArray()->one();
			if(isset($data['custom_url_key'])){
				return $originUrlKey;
			}
		}
		if($originUrlKey){
			$urlKey = $this->generateUrlByName($originUrlKey);
		}else{
			$urlKey = $this->generateUrlByName($str);
		}
		if(strlen($urlKey)<=1){
			$urlKey .= $this->getRandom();
		}
		if(strlen($urlKey)<=2){
			$urlKey .= '-'.$this->getRandom();
		}
		$urlKey = $this->getRewriteUrlKey($urlKey,$originUrl);
		$UrlRewrite = $this->findOne([
			'origin_url' => $originUrl
		]);
		if(!isset($UrlRewrite['origin_url'])){
			$UrlRewrite = $this->newModel();
		}
		$UrlRewrite->type = $type;
		$UrlRewrite->custom_url_key = $urlKey;
		$UrlRewrite->origin_url = $originUrl;
		$UrlRewrite->save();
		return $urlKey;
	}
	
	/**
	 * @property $url_key|String 
	 * remove url rewrite data by $url_key,which is custom url key that saved in custom url modules,like articcle , product, category ,etc..
	 */
	public function removeRewriteUrlKey($url_key){
		$model = $this->findOne([
				'custom_url_key' => $url_key,
			]);
		if($model['custom_url_key']){
			$model->delete();
		}
		
	}
	
	/**
	 *  @property $urlKey|String 
	 *  get $origin_url by $custom_url_key ,it is used for yii2 init,
	 *  in (new fecshop\services\Request)->resolveRequestUri(),  ## fecshop\services\Request is extend  yii\web\Request
	 */
	public function getOriginUrl($urlKey){
		
		return Yii::$service->url->rewrite->getOriginUrl($urlKey);
	}
	
	/**
	 * @property $path|String, for example about-us.html,  fashion-handbag/women.html
	 * genarate current store url by path.
	 */
	public function getUrlByPath($path,$https=false){
		if($https){
			$baseUrl 	= $this->getHttpsBaseUrl();
		}else{
			$baseUrl 	= $this->getHttpBaseUrl();
		}
		return $baseUrl.'/'.$path;
	}
	
	/**
	 * get current base url , is was generate by http(or https ).'://'.store_code  
	 */
	public function getCurrentBaseUrl(){
		if(!$this->_currentBaseUrl){
			$homeUrl = $this->homeUrl();
			if(!$this->_httpType)
				$this->_httpType = $this->secure() ? 'https' : 'http';
			$this->_currentBaseUrl = str_replace("http",$this->_httpType,$homeUrl);
		}
		return $this->_currentBaseUrl;
	}
	
	
	/**
	 * get current home url , is was generate by 'http://'.store_code  
	 */
	public function homeUrl(){
		return Yii::$app->getHomeUrl();
	}
	
	
	
	/**
	 * get http format base url.
	 */
	protected function getHttpBaseUrl(){
		if(!$this->_httpBaseUrl){
			$homeUrl = $this->homeUrl();
			if(strstr($homeUrl,'https://')){
				$this->_httpBaseUrl = str_replace('https://','http://',$homeUrl);
			}else{
				$this->_httpBaseUrl = $homeUrl;
			}
		}
		return $this->_httpBaseUrl;
	}
	/**
	 * get https format base url.
	 */
	protected function getHttpsBaseUrl(){
		if(!$this->_httpsBaseUrl){
			$homeUrl = $this->homeUrl();
			if(strstr($homeUrl,'http://')){
				$this->_httpsBaseUrl = str_replace('http://','https://',$homeUrl);
			}else{
				$this->_httpsBaseUrl = $homeUrl;
			}
		}
		return $this->_httpsBaseUrl;
	}
	
	
	
	
	
	
	
	protected function newModel(){
		return Yii::$service->url->rewrite->newModel();
	}
	protected function find(){
		return Yii::$service->url->rewrite->find();
	}
	
	
	protected function findOne($where){
		return Yii::$service->url->rewrite->findOne($where);
	}
	
	
	
	/**
	 * check current url type is http or https. https is secure url type.
	 */ 
	protected function secure(){
		if($this->_secure === null){
			$this->_secure = isset($_SERVER['HTTPS']) && (strcasecmp($_SERVER['HTTPS'], 'on') === 0 || $_SERVER['HTTPS'] == 1) || isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && strcasecmp($_SERVER['HTTP_X_FORWARDED_PROTO'], 'https') === 0;
		}
		return $this->_secure;
	}
	
	/**
	 * get rewrite url key.
	 */
	protected function getRewriteUrlKey($urlKey,$originUrl){
		$model = $this->find();
		$data = $model->where([
			'custom_url_key' => $urlKey,
		])->andWhere(['<>','origin_url',$originUrl])
		->asArray()->one();
		if(isset($data['custom_url_key'])){
			$urlKey = $this->getRandomUrlKey($urlKey);
			return $this->getRewriteUrlKey($urlKey,$originUrl);
		}else{
			return $urlKey;
		}
	}
	
	
	/**
	 * generate random string.
	 */
	protected function getRandom($length=''){
		if(!$length ){
			$length = $this->randomCount;
		}
		$str = null;
		$strPol = "123456789";
		$max = strlen($strPol)-1;
		for($i=0;$i<$length;$i++){
			$str.=$strPol[rand(0,$max)];//rand($min,$max)生成介于min和max两个数之间的一个随机整数
		}
		return $str;
	  
	}
	/**
	 * if url key is exist in url_rewrite table ,Behind url add some random string 
	 */
	protected function getRandomUrlKey($url){
		if($this->_origin_url){
			$suffix = '';
			$o_url = $this->_origin_url;
			if(strstr($this->_origin_url,'.')){
				list($o_url,$suffix) = explode('.',$this->_origin_url);
				$randomStr = $this->getRandom();
				return $o_url.'-'.$randomStr.'.'.$suffix;
			}
			$randomStr = $this->getRandom();
			return $this->_origin_url.'-'.$randomStr;
		}
	}
	
	/**
	 * clear character that can not use for url.
	 */ 
	protected function generateUrlByName($name){
		$url = iconv('UTF-8', 'ASCII//TRANSLIT', $name);
		$url = preg_replace("{[^a-zA-Z0-9_.| -]}", '', $url);
		$url = strtolower(trim($url, '-'));
		$url = preg_replace("{[_| -]+}", '-', $url);
		$url = '/'.trim($url,'/');
		$this->_origin_url = $url;
		return $url;
	}
	
}


```

通过调用 saveRewriteUrlKeyByStr($str,$originUrl,$originUrlKey,$type='system')方法，
来将某个url加入到url自定义中。

@fecshop\services\url [[ Yii::$service->url->saveRewriteUrlKeyByStr($str,$originUrl,$originUrlKey,$type='system'); ]]

- [[$str]]是字符串，一般使用title或者name生成，譬如Article使用的是title
，product使用的是name。
- [[$originUrl]]是原来的url，也就是按照yii2的路由生成的url。
- [[$originUrlKey]]代表自定义url，如果这个值不填写，就会使用上面的[[$str]]来生成，如果填写了这个自定义url，那么就不会使用
上面的$str生成。


如果自定义url存在，系统则会在url的后面加入一段随机字符串。
如果url含有后缀，则会在后缀的前面加上随机字符串。


### 2.在Fecshop初始化的时候查询自定义url，匹配出来 【原来的url】

这个是由 @fecshop\yii\web\Request的resolveRequestUri()方法完成的,
通过重写@yii\web\Request的方法

```
protected function resolveRequestUri()
    {
        if (isset($_SERVER['HTTP_X_REWRITE_URL'])) { // IIS
            $requestUri = $_SERVER['HTTP_X_REWRITE_URL'];
        } elseif (isset($_SERVER['REQUEST_URI'])) {
            $requestUri = $_SERVER['REQUEST_URI'];
            if ($requestUri !== '' && $requestUri[0] !== '/') {
                $requestUri = preg_replace('/^(http|https):\/\/[^\/]+/i', '', $requestUri);
            }
        } elseif (isset($_SERVER['ORIG_PATH_INFO'])) { // IIS 5.0 CGI
            $requestUri = $_SERVER['ORIG_PATH_INFO'];
            if (!empty($_SERVER['QUERY_STRING'])) {
                $requestUri .= '?' . $_SERVER['QUERY_STRING'];
            }
        } else {
            throw new InvalidConfigException('Unable to determine the request URI.');
        }
		
		/**
		 * Replace Code 
		 * //return $requestUri;
		 * To:
		 */
		return $this->getRewriteUri($requestUri);
    }
```

其他的函数为：

```
/**
	 * get module request url by db ;
	 */
	protected function getRewriteUri($requestUri){
		$baseUrl = $this->getBaseUrl();
		$requestUriRelative = $requestUri;
		if($baseUrl){
			$requestUriRelative = substr($requestUriRelative, strlen($baseUrl));
		}
		
		//echo $requestUriRelative;exit;
		$urlKey  = '';
		$urlParam = '';
		$urlParamSuffix = '';
		
		if(strstr($requestUriRelative,"#")){
			list($urlNoSuffix,$urlParamSuffix)=  explode("#",$requestUriRelative);
			if(strstr($urlNoSuffix,"?")){
				list($urlKey,$urlParam)=  explode("?",$urlNoSuffix);
			}
		}else if(strstr($requestUriRelative,"?")){
			list($urlKey,$urlParam)= explode("?",$requestUriRelative);
		}else{
			$urlKey 	= $requestUriRelative;
		}
		if($urlParamSuffix){
			$urlParamSuffix = '#'.$urlParamSuffix;
		}
		if($originUrlPath = Yii::$service->url->getOriginUrl($urlKey)){
			if(strstr($originUrlPath,'?')){
				if($urlParam){
					$url = $originUrlPath.'&'.$urlParam.$urlParamSuffix;
				}else{
					$url = $originUrlPath.$urlParamSuffix;
				}
				$this->setRequestParam($originUrlPath);
			}else{
				if($urlParam){
					$url = $originUrlPath.'?'.$urlParam.$urlParamSuffix;
				}else{
					$url = $originUrlPath.$urlParamSuffix;
				}
			}
			return $baseUrl.$url;
		}else{
			return $requestUri;
		}
		
	}
	
	/**
	 * after get urlPath from db, if urlPath has get param ,
	 * set the param to $_GET
	 */
	public function setRequestParam($originUrlPath){
		$arr    = explode("?",$originUrlPath);
		$yiiUrlParam = $arr[1];
		$arr    = explode("&",$yiiUrlParam);
		foreach($arr as $a){
			list($key,$val) = explode("=",$a);
			$_GET[$key] = $val;
		}
	}
    
	/**
	 *  mongodb url_rewrite collection columns: _id,  type ,custom_url, yii_url,
	 *	if selete date from UrlRewrite, return the yii url.
	 */
	protected function getOriginUrl($urlKey){
		$UrlData = UrlRewrite::find()->where([
			'custom_url_key' => $urlKey,
		])->asArray()->one();
		if($UrlData['custom_url_key']){
			return $UrlData['origin_url'];
		}
		return ;
	}
```

在yii2初始化，初始化url部分的时候，需要用到Request组件，
通过重写yii\web\Request,的方法，加入我们的自定义url查找原来url的逻辑代码
，通过数据库找到原来的url，返回，
也就是说resolveRequestUri() 的作用是通过自定义的url 找到原来的url key。
后面的处理会使用返回的**原来的url**进行下面的处理，这样就完成了url的自定义。

到这里就完成了fecshop url自定义的整个功能的介绍。





















