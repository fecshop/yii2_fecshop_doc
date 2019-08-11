Fecshop验证码
============

> 在注册账户，登录，找回密码等表单提交的地方需要验证码，
> 您可以通过配置的方式决定是否开启验证码。


Fecshop-2.x更新说明
-------------

2版本更新后台配置


验证码的开启在`后台`各个部分进行配置，


Fecshop-1.x
-------------


配置文件为：`@fecshop/app/appfront/config/modules/Customer.php`

打开后通过注释就可以找到各个配置项.


```
return [
	'customer' => [
		'class' => '\fecshop\app\appfront\modules\Customer\Module',
		'params'=> [
			'register' => [
				# 账号注册成功后，是否自动登录
				'successAutoLogin' => true, 
				# 注册登录成功后，跳转的url
				'loginSuccessRedirectUrlKey' => 'customer/account', 
				# 注册页面的验证码是否开启
				'registerPageCaptcha' => true, 
				
			],
			'login' => [
				# 在登录页面 customer/account/login 页面登录成功后跳转的urlkey，
				'loginPageSuccessRedirectUrlKey' => 'customer/account',
				# 在其他页面的弹框方式登录的账号成功后，的页面跳转，如果是false，则代表返回原来的页面。
				'otherPageSuccessRedirectUrlKey' => false  ,
				# 登录页面的验证码是否开启
				'loginPageCaptcha' => false,  
				# 邮件信息，登录账号后是否发送邮件
				
			],
			'forgotPassword' => [
				# 忘记密码页面的验证码是否开启
				'forgotCaptcha' => true, 
				
			],
			
			'leftMenu'  => [
				'Account Dashboard' => 'customer/account',
				'Account Information' => 'customer/editaccount',
				'Address Book' => 'customer/address',
				'My Orders' => 'customer/order',
				'My Product Reviews' => 'customer/productreview',
				'My Favorite' => 'customer/productfavorite',
				
			],
			
			'contacts'	=> [
				# 联系我们页面的验证码是否开启
				'contactsCaptcha' => true, 
				
			],
			'newsletterSubscribe' => [
				
			],
		],
	],
];
```

您可以在appfront通过添加配置覆盖的方式，重新设置是否开启验证码。


2.如果您想在自己的一些功能中加入验证码可以使用（appfront和apphtml5端）

2.1显示验证码图片,以及填写验证码的input框，刷新验证码的图标等

```
<div class="field">
    <label for="captcha" class="required"><em>*</em><?= Yii::$service->page->translate->__('Captcha'); ?></label>
    <div class="input-box register-captcha">
        <input type="text" name="editForm[captcha]" value="" size=10 class="login-captcha-input"> 
        <img class="login-captcha-img"  title="click refresh" src="<?= Yii::$service->url->getUrl('site/helper/captcha'); ?>?<?php echo md5(time() . mt_rand(1,10000));?>" align="absbottom" onclick="this.src='<?= Yii::$service->url->getUrl('site/helper/captcha'); ?>?'+Math.random();"></img>
        <i class="refresh-icon"></i>
    </div>
    <script>
    <?php $this->beginBlock('register_captcha_onclick_refulsh') ?>  
    $(document).ready(function(){
        $(".refresh-icon").click(function(){
            $(this).parent().find("img").click();
        });
    });
    <?php $this->endBlock(); ?>  
    </script>  
    <?php $this->registerJs($this->blocks['register_captcha_onclick_refulsh'],\yii\web\View::POS_END);//将编写的js代码注册到页面底部 ?>
</div>
```

2.2前端提交的验证码，服务端接收后，需要验证：

```
Yii::$service->helper->captcha->validateCaptcha($captcha)
```





























