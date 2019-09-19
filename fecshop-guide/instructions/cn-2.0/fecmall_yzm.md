Fecmall验证码
============

> 在注册账户，登录，找回密码等表单提交的地方需要验证码，
> 您可以通过配置的方式决定是否开启验证码。


### fecmall验证码设置


验证码的开启在`后台`各个部分进行配置，

### 二开功能加入验证码

如果您想在自己的一些功能中加入验证码可以使用（appfront和apphtml5端）

1.显示验证码图片,以及填写验证码的input框，刷新验证码的图标等

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

2.前端提交的验证码，服务端接收后，需要验证：

```
Yii::$service->helper->captcha->validateCaptcha($captcha)
```





























