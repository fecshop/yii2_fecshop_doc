Fecshop 手机检测跳转
=================

> 当手机访问pc端(appfront)url，可以通过设置自动跳转到手机html5（apphtml5）端。

### 配置设置

打开配置文件 `@appfront/config/fecshop_local_services/Store.php`

可以看到配置代码：

```
'fecshop.appfront.fancyecommerce.com' => [
    'language'         => 'en_US',        // 语言简码需要在@common/config/fecshop_local_services/FecshopLang.php 中定义。
    'languageName'     => 'English',    // 语言简码对应的文字名称，将会出现在语言切换列表中显示。
    'localThemeDir'    => '@appfront/theme/terry/theme01', // 设置当前store对应的模板路径。关于多模板的方面的知识，您可以参看fecshop多模板的知识。
    'thirdThemeDir'    => [],  // 第三方模板路径，数组，可以多个路径
    'currency'         => 'USD', // 当前store的默认货币,这个货币简码，必须在货币配置中配置
    /*
     * 当设备满足什么条件的时候，进行跳转。
     * 这种方式不怎么高效，最好的方式是在nginx中配置。
     */
    'mobile'        => [
        'enable'            => true,
        'condition'         => ['phone', 'tablet'], // phone 代表手机，tablet代表平板，当都填写，代表手机和平板都会进行跳转
        'redirectDomain'    => 'fecshop.apphtml5.fancyecommerce.com',    // 如果是移动设备访问进行域名跳转，这里填写的值为store key
        'https'             => false,  // 手机端url是否支持https,如果支持，设置https为true，如果不支持，设置为false
    ],
```

当 `mobile.enable` 设置为`true`，当访问`pc`端会跳转到`html5`端。

### 原理

打开`@fecshop/services/Store.php` ，您可以看到 `html5DevideCheckAndRedirect()`方法：

```

/**
 * @property $store_code | String 
 * @property $store | Array
 * mobile devide url redirect.
 */
protected function html5DevideCheckAndRedirect($store_code, $store)
{
    if (!isset($store['mobile'])) {
        return;
    }
    $mobileDetect = Yii::$service->helper->mobileDetect;
    $enable = isset($store['mobile']['enable']) ? $store['mobile']['enable'] : false;
    if (!$enable) {
        return;
    }
    $condition = isset($store['mobile']['condition']) ? $store['mobile']['condition'] : false;
    $redirectDomain = isset($store['mobile']['redirectDomain']) ? $store['mobile']['redirectDomain'] : false;
    if (is_array($condition) && !empty($condition) && !empty($redirectDomain)) {
        
        $mobile_https = (isset($store['mobile']['https']) && $store['mobile']['https']) ? true : false;
        if (in_array('phone', $condition) && in_array('tablet', $condition)) {
            if ($mobileDetect->isMobile()) {
                $this->redirectMobile($store_code, $redirectDomain, $mobile_https);
            }
        } elseif (in_array('phone', $condition)) {
            if ($mobileDetect->isMobile() && !$mobileDetect->isTablet()) {
                $this->redirectMobile($store_code, $redirectDomain, $mobile_https);
            }
        } elseif (in_array('tablet', $condition)) {
            if ($mobileDetect->isTablet()) {
                $this->redirectMobile($store_code, $redirectDomain, $mobile_https);
            }
        }
    }
}

/**
 * @property $store_code | String
 * @property $redirectDomain | String
 * 设备满足什么条件的时候进行跳转。
 */
protected function redirectMobile($store_code, $redirectDomain, $mobile_https)
{
    $currentUrl = Yii::$service->url->getCurrentUrl();
    $redirectUrl = str_replace($store_code, $redirectDomain, $currentUrl);
    // pc端跳转到html5，可能一个是https，一个是http，因此需要下面的代码进行转换。
    if ($mobile_https) {
        if (strstr($redirectUrl,'https://') || strstr($redirectUrl,'http://')) {
            $redirectUrl = str_replace('http://','https://',$redirectUrl);
        } else {
            $redirectUrl = 'https:'.$redirectUrl;
        }
    } else {
        if (strstr($redirectUrl,'https://') || strstr($redirectUrl,'http://')) {
            $redirectUrl = str_replace('https://','http://',$redirectUrl);
        } else {
            $redirectUrl = 'http:'.$redirectUrl;
        }
    }
    header('Location:'.$redirectUrl);
}
```


`html5DevideCheckAndRedirect`方法检测是否是手机访问，如果是，则进行跳转。


