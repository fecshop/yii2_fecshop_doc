Fecshop 多货币
==============

> fecshop 支持[多store](fecshop-feature-mutil-stores.md), 同时，
每一个store都有一个默认的货币，在第一次打开store的页面，store下的产品价格都是store设置的货币价格，
当然，用户可以通过多货币切换，查看其他的货币类型下的价格。

货币汇率设置。

### 1.全部货币的配置：

在page服务的子服务currency的配置文件 appfront\config\fecshop_local_services\Page.php，可以看到对货币的配置：

```
'currency' => [
	'baseCurrecy' => 'USD',  # 产品的价格都使用基础货币填写价格值。
	'defaultCurrency' => 'USD', # 如果store不设置货币，就使用这个store默认货币
	'currencys' => [
		'USD' => [
			'rate' 		=> 1,
			'symbol' 	=> '$',
		],
		'RMB' => [
			'rate' 		=> 6.3,
			'symbol' 	=> '￥',
		],
	],
],
```

这个就是所有的货币配置，

- 参数[[baseCurrecy]]: 在网站后台编辑的产品价格，都是基础货币的价格，譬如：我的baseCurrency设置的是RMB，那么，我对产品价格
的填写的值，都是RMB货币下面的价格值，在其他货币的汇率，也是以这个基础货币，换算的比率，对于国际来说，一般用美元作为基础货币。
- 参数[[defaultCurrency]]:代表store默认货币，当某个store的默认货币没有填写的时候，就会从这里取值。
- 参数[[currencys]]: 这个是对货币的配置。
- 参数[[currencys[key]]]:代表货币简码，譬如上面的[['USD']]和[['RMB']]
- 参数：[[rate]]:代表和基础货币的比率.
- 参数：[[symbol]]:代表货币的符号。

### 2.货币子服务  Currency services

货币服务是 Page服务的子服务，文件为：@fecshop\services\page\Currency

得到配置中的所有货币。[[Yii::$service->page->currency->getCurrencys();]] 
代码如下：

```
public function getCurrencys($currencyCode=''){
		$arr = [];
		foreach($this->currencys as $code => $info){
			$arr[$code] = [
				'code' 		=> $code ,
				'rate' 		=> $info['rate'] ,
				'symbol' 	=> $info['symbol'] ,
			];
		}
		if($currencyCode)
			return $arr[$currencyCode];
		return $arr;
	}
```

得到当前货币的价格：

```
public function getCurrentCurrencyPrice($price){
	if(isset($this->currencys[$this->getCurrentCurrency()]['rate'])){
		$rate = $this->currencys[$this->getCurrentCurrency()]['rate'];
		if($rate)
			return ceil($price * $rate  * 100)/100;
	}
	/**
	 * if error current will be set to default currency.
	 */
	$currency = $this->defaultCurrency ;
	$this->setCurrentCurrency($currency);
	return $price;
}
```


**初始化**：
在fecshop的store服务的bootstrap过程中（文件为@fecshop\services\Store，方法为bootstrap(),
在@appfront\config\fecshop_local.php 可以看到bootstrap的配置：'bootstrap' => ['store'],
），执行了store服务的bootstrap
，代码如下：

```
/**
 * init store currency.
 */
if(isset($store['currency']) && !empty($store['currency'])){
	$currency = $store['currency'];
}else{
	$currency = '';
}

Yii::$service->page->currency->initCurrency($currency);

```

也就是通过[[Yii::$service->page->currency->initCurrency($currency);]],
来初始化当前store的货币，当前的默认货币是由store服务的配置文件中配置的

```
'stores' => [
	# store_code ,define by domain and fold.
	'fecshop.appfront.fancyecommerce.com' => [
		'language' 		=> 'en_US',
		'languageName' 		=> 'English',
		'themePackage'	=> 'default',
		'theme'	=> 'default',
		'currency' => 'USD',
	],
	'fecshop.appfront.fancyecommerce.com/fr' => [
		'language' 		=> 'fr_FR',
		'languageName' 		=> 'Fran?ais',
		'themePackage'	=> 'default',
		'theme'	=> 'default',
		'currency' => 'RMB',
	],
	'fecshop.appfront.fancyecommerce.com/es' => [
		'language' 		=> 'es_ES',
		'languageName' 		=> 'Espa?ol',
		'themePackage'	=> 'default',
		'theme'	=> 'default',
		'currency' => 'USD',
	],
	'fecshop.appfront.fancyecommerce.com/cn' => [
		'language' 		=> 'zh_CN',
		'languageName' 		=> '中文',
		'themePackage'	=> 'default',
		'theme'	=> 'default',
		'currency' => 'RMB',
	],
],
```

可以看到每一个store有一个默认货币。
通过这个currency，赋值到currency子服务中，
Yii::$service->page->currency->initCurrency($currency);
，下面我们查看currency子服务的initCurrency($currency)方法：

```
public function initCurrency($currency=''){
		if(!$this->getCurrentCurrency()){
			if(!$currency)
				$currency = $this->defaultCurrency;
			$this->setCurrentCurrency($currency);
		}
		
	}
	
	public function getCurrencyInfo($code=''){
		if(!$code)
			$code = $this->getCurrentCurrency();
		return $this->getCurrencys($code);
	}
	
	public function getCurrentCurrency(){
		if(!$this->_currentCurrency)
			$this->_currentCurrency = CSession::get(self::CURRENCY_CURRENT);
		return $this->_currentCurrency;
	}
	
	public function setCurrentCurrency($currency){
		if($this->isCorrectCurrency($currency)){
			CSession::set(self::CURRENCY_CURRENT,$currency);
			return true;
		}
		
	}
	/**
	 * check param currency if is contained in object variable $currencys.
	 */
	protected function isCorrectCurrency($currency){
		foreach($this->currencys as $code => $info){
			if($code == $currency)
				return true;
		}
		return false;
	}
```

如果session中没有设置货币，则使用store的货币设置
，如果store没有设置货币，则使用默认货币。

这样就完成了对currency服务的初始化。

### 3.如何获取当前货币的价格

在currency子服务中，可以看到：

```
public function getCurrentCurrencyPrice($price){
		if(isset($this->currencys[$this->getCurrentCurrency()]['rate'])){
			$rate = $this->currencys[$this->getCurrentCurrency()]['rate'];
			if($rate)
				return ceil($price * $rate  * 100)/100;
		}
		/**
		 * if error current will be set to default currency.
		 */
		$currency = $this->defaultCurrency ;
		$this->setCurrentCurrency($currency);
		return $price;
	}
```

$price是基础货币，通过上面的方法得到了当前货币
下的价格值,执行函数为：
Yii::$service->page->currency->getCurrentCurrencyPrice($price);






