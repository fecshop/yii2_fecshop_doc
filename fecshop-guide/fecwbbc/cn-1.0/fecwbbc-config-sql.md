FecWbbc跨境多商户 - 静态块配置
======

> 商城的一些静态块html，放到后台单独编辑，便于维护。

### FecWbbc 静态块数据编辑

您有2种方式进入静态块（static block）数据添加，通过`数据库sql导入`，和，通过`后台手动编辑`添加，
您可以选择其中的一种添加`静态块`即可。

1.如果您有数据库操作经验，可以直接使用`sql导入`

下面的sql执行一般是没有问题的。（当然不排除极端环境，可以备份一下数据库）

sql内容如下：

```

INSERT INTO `static_block` (`id`, `identify`, `title`, `status`, `content`, `created_at`, `updated_at`, `created_user_id`) VALUES
(16, 'html5_home_top', 'a:8:{s:8:"title_en";s:17:"Html5： Home Top";s:8:"title_zh";s:0:"";s:8:"title_fr";s:0:"";s:8:"title_de";s:0:"";s:8:"title_es";s:0:"";s:8:"title_pt";s:0:"";s:8:"title_ru";s:0:"";s:8:"title_it";s:0:"";}', 1, 'a:8:{s:10:"content_en";s:5247:"<div class="mb-0 v-card">    <div class="home-v2-top-banner-wrap" moduleindex="1" moduletype="2001" style="padding-bottom:0.426667rem; ">        <div class="agile home-top-banner-wrap ltr">            <div class="agile__list">                <div class="agile__track" style="transform:translate(0px);  transition:transform 0ms ease 0s;  ">                    <div class="agile__slides agile__slides--regular" style="width:100%">                        <a href="" class="agile__slide agile__slide--active agile__slide--current" style="width:100%">                            <img alt="fecmall" class="home-top-banner lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803195524_562.jpg" style="height:5.33333rem;" />                        </a>                    </div>                </div>            </div>        </div>    </div></div><div class="mb-0 v-card">    <div class="home-v2-four-banner-wrap px-1" moduletype="2003" data-src="" lazy="loading" style="padding-bottom:0.426667rem;">        <ul>            <li>              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803031614_661.png" />              <p class="text-overflow mt-1">Tops</p></li>            <li>              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803031726_609.png" />              <p class="text-overflow mt-1">Bottoms</p></li>            <li>              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803033756_660.png" />              <p class="text-overflow mt-1">Dresses</p></li>            <li>              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803033829_619.png" />              <p class="text-overflow mt-1">Lingerie</p></li>            <li class="last-line">              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803033901_216.png" />              <p class="text-overflow mt-1">shoes</p></li>            <li class="last-line">              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803033926_934.png" />              <p class="text-overflow mt-1">Bags</p></li>            <li class="last-line">              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803034004_217.png" />              <p class="text-overflow mt-1">Accessories</p></li>            <li class="last-line">              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803034054_845.png" />              <p class="text-overflow mt-1">Beauty</p></li>        </ul>    </div></div><div class="mb-0 v-card">    <div class="customer-banner" style="padding-bottom:0.426667rem !important;">        <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803034342_751.png" />    </div></div><div class="mb-0 v-card">    <div class="home-v2-banner-with-category" style="padding-bottom:0.426667rem; ">        <div>            <ul class="display-flex pt-2">              <li class="px-1">                <div class="pa-2 category-img">                  <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803034614_854.png" />                </div>                <p class="text-overflow px-2">Socofy</p></li>              <li class="px-1">                <div class="pa-2 category-img">                  <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803034709_246.png" />                </div>                <p class="text-overflow px-2">Gracila</p></li>              <li class="px-1">                <div class="pa-2 category-img">                  <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803062802_374.png" />                </div>                <p class="text-overflow px-2">O-NEWE</p></li>              <li class="px-1">                <div class="pa-2 category-img">                  <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803062814_786.png" />                </div>                <p class="text-overflow px-2">Lostisy</p></li>            </ul>            <div class="separating-banner ba1">              <div class="separating-banner-content separating-banner-subtitle">                <span>UP TO 60%OFF</span></div>              <div class="separating-banner-content separating-banner-title">                <span>Vintage Shoes</span></div>              <div class="separating-banner-content separating-banner-button">                <span class="px-2">buy now &gt;</span></div>            </div>        </div>    </div></div>          ";s:10:"content_zh";s:5219:"<div class="mb-0 v-card">    <div class="home-v2-top-banner-wrap" moduleindex="1" moduletype="2001" style="padding-bottom:0.426667rem; ">        <div class="agile home-top-banner-wrap ltr">            <div class="agile__list">                <div class="agile__track" style="transform:translate(0px);  transition:transform 0ms ease 0s;  ">                    <div class="agile__slides agile__slides--regular" style="width:100%">                        <a href="" class="agile__slide agile__slide--active agile__slide--current" style="width:100%">                            <img alt="fecmall" class="home-top-banner lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803195524_562.jpg" style="height:5.33333rem;" />                        </a>                    </div>                </div>            </div>        </div>    </div></div><div class="mb-0 v-card">    <div class="home-v2-four-banner-wrap px-1" moduletype="2003" data-src="" lazy="loading" style="padding-bottom:0.426667rem;">        <ul>            <li>              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803031614_661.png" />              <p class="text-overflow mt-1">Tops</p></li>            <li>              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803031726_609.png" />              <p class="text-overflow mt-1">Bottoms</p></li>            <li>              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803033756_660.png" />              <p class="text-overflow mt-1">Dresses</p></li>            <li>              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803033829_619.png" />              <p class="text-overflow mt-1">Lingerie</p></li>            <li class="last-line">              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803033901_216.png" />              <p class="text-overflow mt-1">shoes</p></li>            <li class="last-line">              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803033926_934.png" />              <p class="text-overflow mt-1">Bags</p></li>            <li class="last-line">              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803034004_217.png" />              <p class="text-overflow mt-1">Accessories</p></li>            <li class="last-line">              <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803034054_845.png" />              <p class="text-overflow mt-1">Beauty</p></li>        </ul>    </div></div><div class="mb-0 v-card">    <div class="customer-banner" style="padding-bottom:0.426667rem !important;">        <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803034342_751.png" />    </div></div><div class="mb-0 v-card">    <div class="home-v2-banner-with-category" style="padding-bottom:0.426667rem; ">        <div>            <ul class="display-flex pt-2">              <li class="px-1">                <div class="pa-2 category-img">                  <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803034614_854.png" />                </div>                <p class="text-overflow px-2">Socofy</p></li>              <li class="px-1">                <div class="pa-2 category-img">                  <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803034709_246.png" />                </div>                <p class="text-overflow px-2">Gracila</p></li>              <li class="px-1">                <div class="pa-2 category-img">                  <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803062802_374.png" />                </div>                <p class="text-overflow px-2">O-NEWE</p></li>              <li class="px-1">                <div class="pa-2 category-img">                  <img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecro/20200803062814_786.png" />                </div>                <p class="text-overflow px-2">Lostisy</p></li>            </ul>            <div class="separating-banner ba1">              <div class="separating-banner-content separating-banner-subtitle">                <span>UP TO 60%OFF</span></div>              <div class="separating-banner-content separating-banner-title">                <span>Vintage Shoes</span></div>              <div class="separating-banner-content separating-banner-button">                <span class="px-2">buy now &gt;</span></div>            </div>        </div>    </div></div>          ";s:10:"content_fr";s:0:"";s:10:"content_de";s:0:"";s:10:"content_es";s:0:"";s:10:"content_pt";s:0:"";s:10:"content_ru";s:0:"";s:10:"content_it";s:0:"";}', 1615470851, 1615471061, 2),
(17, 'pc-home-top-text', 'a:8:{s:8:"title_en";s:29:"Pc：首页大图顶部文字";s:8:"title_zh";s:0:"";s:8:"title_fr";s:0:"";s:8:"title_de";s:0:"";s:8:"title_es";s:0:"";s:8:"title_pt";s:0:"";s:8:"title_ru";s:0:"";s:8:"title_it";s:0:"";}', 1, 'a:8:{s:10:"content_en";s:566:"<div class="NC-home__top-three-btn lg-8 border-right">     <a class="font-bold text-secondary nc-home-top-new-customer-btn-js" style="color:#99593c" href="">        New Friend Exclusive 15% OFF &gt;     </a></div> <div class="NC-home__top-three-btn lg-8 border-right">     <a class="font-bold text-secondary" style="color:#99593c" href="">        Invite Friend - 50% CashBack &gt; &gt;     </a> </div> <div class="NC-home__top-three-btn lg-8">     <a class="font-bold text-secondary" style="color:#99593c" href="">        Newsletter Get $10 OFF &gt;     </a> </div> ";s:10:"content_zh";s:0:"";s:10:"content_fr";s:0:"";s:10:"content_de";s:0:"";s:10:"content_es";s:0:"";s:10:"content_pt";s:0:"";s:10:"content_ru";s:0:"";s:10:"content_it";s:0:"";}', 1615470874, 1615470874, 2),
(18, 'pc-home-top-image', 'a:8:{s:8:"title_en";s:17:"Pc：首页大图";s:8:"title_zh";s:0:"";s:8:"title_fr";s:0:"";s:8:"title_de";s:0:"";s:8:"title_es";s:0:"";s:8:"title_pt";s:0:"";s:8:"title_ru";s:0:"";s:8:"title_it";s:0:"";}', 1, 'a:8:{s:10:"content_en";s:876:"<div class="item carousel-item top-carousel-item-js active">     <a href="" class="carousel-item-img-container d-block">         <img class="d-block lazyload " src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200930041957_212.jpg" alt="Fecmall" />    </a> </div> <div class="item carousel-item top-carousel-item-js">     <a href="" class="carousel-item-img-container d-block">         <img class="d-block lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20201005211143_374.jpg" alt="Fecmall" />    </a> </div> <div class="item carousel-item top-carousel-item-js">     <a href="" class="carousel-item-img-container d-block">         <img class="d-block lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200929011450_834.jpg" alt="Fecmall" />     </a> </div> ";s:10:"content_zh";s:0:"";s:10:"content_fr";s:0:"";s:10:"content_de";s:0:"";s:10:"content_es";s:0:"";s:10:"content_pt";s:0:"";s:10:"content_ru";s:0:"";s:10:"content_it";s:0:"";}', 1615470897, 1615471083, 2);
INSERT INTO `static_block` (`id`, `identify`, `title`, `status`, `content`, `created_at`, `updated_at`, `created_user_id`) VALUES
(19, 'pc-home-top-banner-image', 'a:8:{s:8:"title_en";s:41:"Pc：首页大图下面的长条banner图";s:8:"title_zh";s:0:"";s:8:"title_fr";s:0:"";s:8:"title_de";s:0:"";s:8:"title_es";s:0:"";s:8:"title_pt";s:0:"";s:8:"title_ru";s:0:"";s:8:"title_it";s:0:"";}', 1, 'a:8:{s:10:"content_en";s:235:"<a href="" style="width:100%;" class="d-block index-banner NC-obscuration">    <img class="d-block lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20201003034451_323.jpg" alt="Fecmall" /></a> ";s:10:"content_zh";s:0:"";s:10:"content_fr";s:0:"";s:10:"content_de";s:0:"";s:10:"content_es";s:0:"";s:10:"content_pt";s:0:"";s:10:"content_ru";s:0:"";s:10:"content_it";s:0:"";}', 1615470919, 1615471094, 2),
(20, 'pc-home-new-arrival', 'a:8:{s:8:"title_en";s:28:"Pc：首页New Arrival部分";s:8:"title_zh";s:0:"";s:8:"title_fr";s:0:"";s:8:"title_de";s:0:"";s:8:"title_es";s:0:"";s:8:"title_pt";s:0:"";s:8:"title_ru";s:0:"";s:8:"title_it";s:0:"";}', 1, 'a:8:{s:10:"content_en";s:1421:"<div class="lg-20per px-lg-15">     <a href="" class="d-block index-banner NC-obscuration">        <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830215841_852.jpg" />    </a> </div> <div class="lg-20per px-lg-15">     <a href="" class="d-block index-banner NC-obscuration">         <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830215904_559.jpg" />     </a> </div> <div class="lg-20per px-lg-15">     <a href="" class="d-block index-banner NC-obscuration">         <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830215919_243.jpg" />    </a> </div> <div class="lg-20per px-lg-15">     <a href="" class="d-block index-banner NC-obscuration">         <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830215935_699.jpg" />     </a> </div> <div class="lg-20per px-lg-15">     <a href="" class="d-block index-banner NC-obscuration">         <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830215953_840.jpg" />    </a> </div> ";s:10:"content_zh";s:0:"";s:10:"content_fr";s:0:"";s:10:"content_de";s:0:"";s:10:"content_es";s:0:"";s:10:"content_pt";s:0:"";s:10:"content_ru";s:0:"";s:10:"content_it";s:0:"";}', 1615470950, 1615471110, 2),
(21, 'pc-home-banner-2', 'a:8:{s:8:"title_en";s:29:"Pc：首页第二个Banner图";s:8:"title_zh";s:0:"";s:8:"title_fr";s:0:"";s:8:"title_de";s:0:"";s:8:"title_es";s:0:"";s:8:"title_pt";s:0:"";s:8:"title_ru";s:0:"";s:8:"title_it";s:0:"";}', 1, 'a:8:{s:10:"content_en";s:1266:"<div class="flex my-lg-30">     <a href="" style="width:100%;" class="d-block index-banner NC-obscuration">         <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830220035_324.jpg" />    </a> </div> <div class="flex mx-lg-n15 my-lg-30">     <div class="lg-8 px-lg-15">         <a href="" class="d-block index-banner NC-obscuration">            <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830220101_154.jpg" />        </a>     </div>     <div class="lg-8 px-lg-15">         <a href="" class="d-block index-banner NC-obscuration">            <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830220129_700.jpg" />        </a>     </div>     <div class="lg-8 px-lg-15" data-banner-id="51937">         <a href="" class="d-block index-banner NC-obscuration">            <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830220146_794.jpg" />         </a>     </div> </div> ";s:10:"content_zh";s:0:"";s:10:"content_fr";s:0:"";s:10:"content_de";s:0:"";s:10:"content_es";s:0:"";s:10:"content_pt";s:0:"";s:10:"content_ru";s:0:"";s:10:"content_it";s:0:"";}', 1615470970, 1615471184, 2),
(22, 'pc-home-footer', 'a:8:{s:8:"title_en";s:29:"Pc：首页Footer底部部分";s:8:"title_zh";s:0:"";s:8:"title_fr";s:0:"";s:8:"title_de";s:0:"";s:8:"title_es";s:0:"";s:8:"title_pt";s:0:"";s:8:"title_ru";s:0:"";s:8:"title_it";s:0:"";}', 1, 'a:8:{s:10:"content_en";s:12388:"<div class="container common-footer__trust-icon-container">    <div class="bg-white flex justify-content-around">        <div class="common-footer__trust-icon-item text-center py-lg-40">            <span class="common-footer__trust-icon-item-img d-inline-block mb-lg-5"></span>            <p class="font-bold text-black mb-lg-5">High-quality Goods</p>            <p class="font-small text-grey">Enjoy top quality items for less</p>        </div>        <div class="common-footer__trust-icon-item text-center py-lg-40">            <span class="common-footer__trust-icon-item-img d-inline-block mb-lg-5"></span>            <p class="font-bold text-black mb-lg-5">24/7 Livechat</p>            <p class="font-small text-grey">Get instant assistance whenever you need it</p>        </div>        <div class="common-footer__trust-icon-item text-center py-lg-40">            <span class="common-footer__trust-icon-item-img d-inline-block mb-lg-5"></span>            <p class="font-bold text-black mb-lg-5">Express Shipping</p>            <p class="font-small text-grey">Fast &amp; reliable delivery options</p>        </div>        <div class="common-footer__trust-icon-item text-center py-lg-40">            <span class="common-footer__trust-icon-item-img d-inline-block mb-lg-5"></span>            <p class="font-bold text-black mb-lg-5">Secure Payment</p>            <p class="font-small text-grey">Multiple safe payment methods</p>        </div>    </div></div><div class="container font-small">    <div class="flex">        <div class="wid-24">            <h3 class="font-bold footer-index__category font-bold">Company Information</h3>            <ul>                <li class="footer-index__item">                    <a class="footer-index__link" href="" rel="nofollow">                        About Fecmall                    </a>                </li>                <li class="footer-index__item">                    <a class="footer-index__link" href="" rel="nofollow">                        Privacy Policy                    </a>                </li>                <li class="footer-index__item">                    <a class="footer-index__link" href="" rel="nofollow">                        Return Policy                    </a>                </li>                <li class="footer-index__item">                    <a class="footer-index__link" href="" rel="nofollow">                        Terms And Conditions                    </a>                </li>                <li class="footer-index__item">                    <a class="footer-index__link" href="" rel="nofollow">                        Intellectual Property Claims                    </a>                </li>                <li class="footer-index__item hidden footer-index-impressum-js">                    <a class="footer-index__link" href="" rel="nofollow">                        imprint                    </a>                </li>            </ul>        </div>        <div class="wid-24">            <h3 class="font-bold footer-index__category font-bold">                Customer Service            </h3>            <ul>                <li class="footer-index__item">                    <a class="footer-index__link" href="" rel="nofollow">                      Track Order                    </a>                </li>                <li class="footer-index__item">                    <a class="footer-index__link" href="" rel="nofollow">                        Shipping FAQ                    </a>                </li>                <li class="footer-index__item">                    <a class="footer-index__link" href="" rel="nofollow">                        Order FAQ                    </a>                </li>                <li class="footer-index__item">                    <a class="footer-index__link" href="" rel="nofollow">                        Shipping Methods                    </a>                </li>                <li class="footer-index__item">                    <a class="footer-index__link" href="" rel="nofollow">                        Payment Methods                    </a>                </li>                <li class="footer-index__item">                    <a class="footer-index__link footer-top-searches-js" href="">                        Top Searches                    </a>                </li>            </ul>        </div>        <div class="wid-24">            <h3 class="font-bold footer-index__category font-bold">                Cooperation            </h3>            <ul>                <li class="footer-index__item">                    <a class="footer-index__link" href="" rel="nofollow">                        Blogger Program                    </a>                </li>                <li class="footer-index__item footer-index-affiliate-js">                    <a class="footer-index__link" href="" rel="nofollow">                        Affiliate - Make Money                    </a>                </li>                <li class="footer-index__item">                    <a class="footer-index__link" href="" rel="nofollow">                        VIP Program                    </a>                </li>                <li class="footer-index__item footer-index-dropship-js">                    <a class="footer-index__link" href="" rel="nofollow">                        Dropship Program                    </a>                </li>                <li class="footer-index__item footer-index-wholesale-js">                    <a class="footer-index__link" href="" rel="nofollow">                        Wholesale Program                    </a>                </li>                <li class="footer-index__item footer-index-student-program-js">                    <a class="footer-index__link" href="" rel="nofollow">                        Student Program                    </a>                </li>                <li class="footer-index__item hidden footer-index-student-es-program-js">                    <a class="footer-index__link" href="" rel="nofollow">                        programa de estudiantes                    </a>                </li>            </ul>        </div>        <div class="wid-28 flex column justify-content-between">            <div class="footer-index-subscribed-content-js justify-content-start">                <div class="mb-lg-20 footer-sub-form-container-js hidden">                </div>                <h3 class="font-bold footer-index__category font-bold footer-index__subscribed-tips footer-index-subscribed-tips-js">                    FOLLOW US AND GET NEWEST INFORMATION                </h3>                <div class="lg-fit">                    <ul class="flex footer-index-community footer-index-community-js mx-lg-n10" data-site="en">                        <li class="mx-lg-10 footer-index__link--icon-container link--icon__vk-icon hidden footer-index-vk-js">                            <a class="footer-index__link--icon" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-vk" style="font-style: italic;"></span>                            </a>                        </li>                        <li class="mx-lg-10 footer-index__link--icon-container link--icon__facebook-icon">                            <a class="footer-index__link--icon footer-index-facebook-js" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-facebook" style="font-style: italic;"></span>                            </a>                        </li>                        <li class="mx-lg-10 footer-index__link--icon-container link--icon__instagram-icon">                            <a class="footer-index__link--icon footer-index-instagram-js" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-instagram1" style="font-style: italic;"></span>                            </a>                        </li>                        <li class="mx-lg-10 footer-index__link--icon-container link--icon__twitter-icon">                            <a class="footer-index__link--icon footer-index-twitter-js" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-twitter" style="font-style: italic;"></span>                            </a>                        </li>                        <li class="mx-lg-10 footer-index__link--icon-container link--icon__pinterest-icon">                            <a class="footer-index__link--icon footer-index-pin-js" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-pinterest1" style="font-style: italic;"></span>                            </a>                        </li>                        <li class="mx-lg-10 footer-index__link--icon-container link--icon__youtube-icon">                            <a class="footer-index__link--icon footer-index-youtube-js" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-youtube" style="font-style: italic;"></span>                            </a>                        </li>                        <li class="mx-lg-10 footer-index__link--icon-container link--icon__blogger-icon">                            <a class="footer-index__link--icon" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-blogger" style="font-style: italic;"></span>                            </a>                        </li>                    </ul>                </div>            </div>            <div class="flex justify-content-start align-items-center">                <a class="d-inline-block footer-app__qr">                    <img class="lazyload footer-app__qr-code lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/qrcode_fecmall.jpg" />                </a>                <div class="lg px-lg-20 font-bold font-normal footer-download-tip-js">                    Get a free gift and use                     <span style="color:#E30057;">20% OFF</span>                     coupon now                </div>            </div>        </div>    </div>    <div class="mt-lg-50">        <div class="flex justify-content-center align-items-center">            <div class="my-lg-10 mx-lg-5 footer-authitem__img footer-paypal-img">                <img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/paypal.png" />            </div>            <div class="my-lg-10 mx-lg-5 footer-authitem__img footer-visa-img">                <img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/visa.png" />            </div>            <div class="my-lg-10 mx-lg-5 footer-authitem__img footer-mastercard-img">                <img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/mastercard.png" />            </div>            <div class="my-lg-10 mx-lg-5 footer-authitem__img footer-mada-img">                <img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/mada.png" />            </div>            <div class="my-lg-10 mx-lg-5 footer-authitem__img footer-oxxo-img">                <img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/oxxo.png" />            </div>            <div class="my-lg-10 mx-lg-5 footer-authitem__img footer-sofort-img">                <img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/sofort.png" />            </div>            <div class="my-lg-10 mx-lg-5 footer-authitem__img footer-ideal-img">                <img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/ideal.png" />            </div>                    </div>        <div class="font-small text-grey pt-lg-10 pb-lg-30 text-center">            Copyright &copy; 2014-2020 <a style="color:#777" target="_blank" href="http://www.fecmall.com">Fecmall.com</a> All Rights Reserved.        </div>    </div></div>";s:10:"content_zh";s:0:"";s:10:"content_fr";s:0:"";s:10:"content_de";s:0:"";s:10:"content_es";s:0:"";s:10:"content_pt";s:0:"";s:10:"content_ru";s:0:"";s:10:"content_it";s:0:"";}', 1615470992, 1615471161, 2);


```

如果您通过sql导入，就不需要执行2步骤了。

#### 2.在平台`后台手动添加`（如果执行了上面的sql导入，这里就不需要执行了）


如果您不会执行sql导入，那么您可以参看下面的步骤，一步一步的在`后台添加配置`(步骤有点繁琐)

一：PC

1.首页顶部文字

后台: `cms` -->  `静态块`

标识符：`pc-home-top-text`

Title: `Pc：首页大图顶部文字`

内容：

```
<div class="NC-home__top-three-btn lg-8 border-right">     
	<a class="font-bold text-secondary nc-home-top-new-customer-btn-js" style="color:#99593c" href="">        New Friend Exclusive 15% OFF &gt;     </a>
</div> 
<div class="NC-home__top-three-btn lg-8 border-right">     
	<a class="font-bold text-secondary" style="color:#99593c" href="">        Invite Friend - 50% CashBack &gt; &gt;     </a> 
</div> 
<div class="NC-home__top-three-btn lg-8">     
	<a class="font-bold text-secondary" style="color:#99593c" href="">        Newsletter Get $10 OFF &gt;     </a> 
</div> 
```

该部分对应pc首页顶部文字，如图：

![](images/fecroo_1.png)


2.首页走马灯大图

后台: `cms` -->  `静态块`

标识符：`pc-home-top-image`

Title: `Pc：首页大图`

内容：

```
<div class="item carousel-item top-carousel-item-js active">     
	<a href="" class="carousel-item-img-container d-block">         <img class="d-block lazyload " src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200930041957_212.jpg" alt="Fecmall" />    </a> 
</div> 
<div class="item carousel-item top-carousel-item-js">     
	<a href="" class="carousel-item-img-container d-block">         <img class="d-block lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20201005211143_374.jpg" alt="Fecmall" />    </a> 
</div> 
<div class="item carousel-item top-carousel-item-js">     
	<a href="" class="carousel-item-img-container d-block">         <img class="d-block lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200929011450_834.jpg" alt="Fecmall" />     </a> 
</div> 
```

该部分对应pc首页顶部文字，如图：

![](images/fecroo_2.png)



3.首页大图下面的banner

后台: `cms` -->  `静态块`

标识符：`pc-home-top-banner-image`

Title: `Pc：首页大图下面的长条banner图`

内容：

```
<a href="" style="width:100%;" class="d-block index-banner NC-obscuration">    <img class="d-block lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20201003034451_323.jpg" alt="Fecmall" /></a> 

```

该部分对应pc首页顶部文字，如图：

![](images/fecroo_3.png)





4.首页New Arrival部分

后台: `cms` -->  `静态块`

标识符：`pc-home-new-arrival`

Title: `Pc：首页New Arrival部分`

内容：

```
<div class="lg-20per px-lg-15">     
	<a href="" class="d-block index-banner NC-obscuration">        <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830215841_852.jpg" />    </a> 
</div> 
<div class="lg-20per px-lg-15">     
	<a href="" class="d-block index-banner NC-obscuration">         <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830215904_559.jpg" />     </a> 
</div> 
<div class="lg-20per px-lg-15">     
	<a href="" class="d-block index-banner NC-obscuration">         <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830215919_243.jpg" />    </a> 
</div> 
<div class="lg-20per px-lg-15">     
	<a href="" class="d-block index-banner NC-obscuration">         <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830215935_699.jpg" />     </a> 
</div> 
<div class="lg-20per px-lg-15">     
	<a href="" class="d-block index-banner NC-obscuration">         <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830215953_840.jpg" />    </a> 
</div> 

```

该部分对应pc首页顶部文字，如图：

![](images/fecroo_4.png)





5.首页New Arrival部分

后台: `cms` -->  `静态块`

标识符：`pc-home-banner-2`

Title: `Pc：首页第二个Banner图`

内容：

```
<div class="flex my-lg-30">     
	<a href="" style="width:100%;" class="d-block index-banner NC-obscuration">         <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830220035_324.jpg" />    </a> 
</div> 
<div class="flex mx-lg-n15 my-lg-30">     
	<div class="lg-8 px-lg-15">         
		<a href="" class="d-block index-banner NC-obscuration">            <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830220101_154.jpg" />        </a>     
	</div>     
	<div class="lg-8 px-lg-15">         
		<a href="" class="d-block index-banner NC-obscuration">            <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830220129_700.jpg" />        </a>     
	</div>     
	<div class="lg-8 px-lg-15" data-banner-id="51937">         
		<a href="" class="d-block index-banner NC-obscuration">            <img class="d-block lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200830220146_794.jpg" />         </a>     
	</div> 
</div> 
```

该部分对应pc首页顶部文字，如图：

![](images/fecroo_5.png)





6.首页footer底部部分

后台: `cms` -->  `静态块`

标识符：`pc-home-footer`

Title: `Pc：首页Footer底部部分`

内容：

```
<div class="container common-footer__trust-icon-container">    
	<div class="bg-white flex justify-content-around">        
		<div class="common-footer__trust-icon-item text-center py-lg-40">            
			<span class="common-footer__trust-icon-item-img d-inline-block mb-lg-5"></span>            
			<p class="font-bold text-black mb-lg-5">
				High-quality Goods
			</p>            
			<p class="font-small text-grey">
				Enjoy top quality items for less
			</p>        
		</div>        
		<div class="common-footer__trust-icon-item text-center py-lg-40">            
			<span class="common-footer__trust-icon-item-img d-inline-block mb-lg-5"></span>            
			<p class="font-bold text-black mb-lg-5">
				24/7 Livechat
			</p>            
			<p class="font-small text-grey">
				Get instant assistance whenever you need it
			</p>        
		</div>        
		<div class="common-footer__trust-icon-item text-center py-lg-40">            
			<span class="common-footer__trust-icon-item-img d-inline-block mb-lg-5"></span>            
			<p class="font-bold text-black mb-lg-5">
				Express Shipping
			</p>            
			<p class="font-small text-grey">
				Fast &amp; reliable delivery options
			</p>        
		</div>        
		<div class="common-footer__trust-icon-item text-center py-lg-40">            
			<span class="common-footer__trust-icon-item-img d-inline-block mb-lg-5"></span>            
			<p class="font-bold text-black mb-lg-5">
				Secure Payment
			</p>            
			<p class="font-small text-grey">
				Multiple safe payment methods
			</p>        
		</div>    
	</div>
</div>
<div class="container font-small">    
	<div class="flex">        
		<div class="wid-24">            
			<h3 class="font-bold footer-index__category font-bold">
				Company Information
			</h3>            
			<ul>                
				<li class="footer-index__item">                    
					<a class="footer-index__link" href="" rel="nofollow">                        About Fecmall                    </a>                
				</li>                
				<li class="footer-index__item">                    
					<a class="footer-index__link" href="" rel="nofollow">                        Privacy Policy                    </a>                
				</li>                
				<li class="footer-index__item">                    
					<a class="footer-index__link" href="" rel="nofollow">                        Return Policy                    </a>                
				</li>                
				<li class="footer-index__item">                    
					<a class="footer-index__link" href="" rel="nofollow">                        Terms And Conditions                    </a>                
				</li>                
				<li class="footer-index__item">                    
					<a class="footer-index__link" href="" rel="nofollow">                        Intellectual Property Claims                    </a>                
				</li>                
				<li class="footer-index__item hidden footer-index-impressum-js">                    
					<a class="footer-index__link" href="" rel="nofollow">                        imprint                    </a>                
				</li>            
			</ul>        
		</div>        
		<div class="wid-24">            
			<h3 class="font-bold footer-index__category font-bold">
				                Customer Service            
			</h3>            
			<ul>                
				<li class="footer-index__item">                    
					<a class="footer-index__link" href="" rel="nofollow">                      Track Order                    </a>                
				</li>                
				<li class="footer-index__item">                    
					<a class="footer-index__link" href="" rel="nofollow">                        Shipping FAQ                    </a>                
				</li>                
				<li class="footer-index__item">                    
					<a class="footer-index__link" href="" rel="nofollow">                        Order FAQ                    </a>                
				</li>                
				<li class="footer-index__item">                    
					<a class="footer-index__link" href="" rel="nofollow">                        Shipping Methods                    </a>                
				</li>                
				<li class="footer-index__item">                    
					<a class="footer-index__link" href="" rel="nofollow">                        Payment Methods                    </a>                
				</li>                
				<li class="footer-index__item">                    
					<a class="footer-index__link footer-top-searches-js" href="">                        Top Searches                    </a>                
				</li>            
			</ul>        
		</div>        
		<div class="wid-24">            
			<h3 class="font-bold footer-index__category font-bold">
				                Cooperation            
			</h3>            
			<ul>                
				<li class="footer-index__item">                    
					<a class="footer-index__link" href="" rel="nofollow">                        Blogger Program                    </a>                
				</li>                
				<li class="footer-index__item footer-index-affiliate-js">                    
					<a class="footer-index__link" href="" rel="nofollow">                        Affiliate - Make Money                    </a>                
				</li>                
				<li class="footer-index__item">                    
					<a class="footer-index__link" href="" rel="nofollow">                        VIP Program                    </a>                
				</li>                
				<li class="footer-index__item footer-index-dropship-js">                    
					<a class="footer-index__link" href="" rel="nofollow">                        Dropship Program                    </a>                
				</li>                
				<li class="footer-index__item footer-index-wholesale-js">                    
					<a class="footer-index__link" href="" rel="nofollow">                        Wholesale Program                    </a>                
				</li>                
				<li class="footer-index__item footer-index-student-program-js">                    
					<a class="footer-index__link" href="" rel="nofollow">                        Student Program                    </a>                
				</li>                
				<li class="footer-index__item hidden footer-index-student-es-program-js">                    
					<a class="footer-index__link" href="" rel="nofollow">                        programa de estudiantes                    </a>                
				</li>            
			</ul>        
		</div>        
		<div class="wid-28 flex column justify-content-between">            
			<div class="footer-index-subscribed-content-js justify-content-start">                
				<div class="mb-lg-20 footer-sub-form-container-js hidden">                
				</div>                
				<h3 class="font-bold footer-index__category font-bold footer-index__subscribed-tips footer-index-subscribed-tips-js">
					                    FOLLOW US AND GET NEWEST INFORMATION                
				</h3>                
				<div class="lg-fit">                    
					<ul class="flex footer-index-community footer-index-community-js mx-lg-n10" data-site="en">                        
						<li class="mx-lg-10 footer-index__link--icon-container link--icon__vk-icon hidden footer-index-vk-js">                            
							<a class="footer-index__link--icon" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-vk" style="font-style: italic;"></span>                            </a>                        
						</li>                        
						<li class="mx-lg-10 footer-index__link--icon-container link--icon__facebook-icon">                            
							<a class="footer-index__link--icon footer-index-facebook-js" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-facebook" style="font-style: italic;"></span>                            </a>                        
						</li>                        
						<li class="mx-lg-10 footer-index__link--icon-container link--icon__instagram-icon">                            
							<a class="footer-index__link--icon footer-index-instagram-js" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-instagram1" style="font-style: italic;"></span>                            </a>                        
						</li>                        
						<li class="mx-lg-10 footer-index__link--icon-container link--icon__twitter-icon">                            
							<a class="footer-index__link--icon footer-index-twitter-js" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-twitter" style="font-style: italic;"></span>                            </a>                        
						</li>                        
						<li class="mx-lg-10 footer-index__link--icon-container link--icon__pinterest-icon">                            
							<a class="footer-index__link--icon footer-index-pin-js" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-pinterest1" style="font-style: italic;"></span>                            </a>                        
						</li>                        
						<li class="mx-lg-10 footer-index__link--icon-container link--icon__youtube-icon">                            
							<a class="footer-index__link--icon footer-index-youtube-js" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-youtube" style="font-style: italic;"></span>                            </a>                        
						</li>                        
						<li class="mx-lg-10 footer-index__link--icon-container link--icon__blogger-icon">                            
							<a class="footer-index__link--icon" href="" rel="nofollow" target="_blank">                                <span class="nc-icon nc-icon-blogger" style="font-style: italic;"></span>                            </a>                        
						</li>                    
					</ul>                
				</div>            
			</div>            
			<div class="flex justify-content-start align-items-center">                
				<a class="d-inline-block footer-app__qr">                    <img class="lazyload footer-app__qr-code lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/qrcode_fecmall.jpg" />                </a>                
				<div class="lg px-lg-20 font-bold font-normal footer-download-tip-js">
					                    Get a free gift and use                     <span style="color:#E30057;">20% OFF</span>                     coupon now                
				</div>            
			</div>        
		</div>    
	</div>    
	<div class="mt-lg-50">        
		<div class="flex justify-content-center align-items-center">            
			<div class="my-lg-10 mx-lg-5 footer-authitem__img footer-paypal-img">                
				<img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/paypal.png" />            
			</div>            
			<div class="my-lg-10 mx-lg-5 footer-authitem__img footer-visa-img">                
				<img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/visa.png" />            
			</div>            
			<div class="my-lg-10 mx-lg-5 footer-authitem__img footer-mastercard-img">                
				<img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/mastercard.png" />            
			</div>            
			<div class="my-lg-10 mx-lg-5 footer-authitem__img footer-mada-img">                
				<img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/mada.png" />            
			</div>            
			<div class="my-lg-10 mx-lg-5 footer-authitem__img footer-oxxo-img">                
				<img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/oxxo.png" />            
			</div>            
			<div class="my-lg-10 mx-lg-5 footer-authitem__img footer-sofort-img">                
				<img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/sofort.png" />            
			</div>            
			<div class="my-lg-10 mx-lg-5 footer-authitem__img footer-ideal-img">                
				<img class="lazyload lazy-loaded show" alt="Fecmall" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/ideal.png" />            
			</div>                    
		</div>        
		<div class="font-small text-grey pt-lg-10 pb-lg-30 text-center">
			            Copyright &copy; 2014-2020 <a style="color:#777" target="_blank" href="http://www.fecmall.com">Fecmall.com</a> All Rights Reserved.        
		</div>    
	</div>
</div>
```

该部分对应pc首页顶部文字，如图：

![](images/fecroo_6.png)











二：H5入口


1.后台， cms -->  静态块

> html5首页顶部的大图以及底部的一些图片

标识符：`html5_home_top`

Title: `Html5 Home Top`

内容：

```
<div class="mb-0 v-card">    
	<div class="home-v2-top-banner-wrap" moduleindex="1" moduletype="2001" style="padding-bottom:0.426667rem; ">        
		<div class="agile home-top-banner-wrap ltr">            
			<div class="agile__list">                
				<div class="agile__track" style="transform:translate(0px);  transition:transform 0ms ease 0s;  ">                    
					<div class="agile__slides agile__slides--regular" style="width:100%">                        
						<a href="" class="agile__slide agile__slide--active agile__slide--current" style="width:100%">                            <img alt="fecmall" class="home-top-banner lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803195524_562.jpg" style="height:5.33333rem;" />                        </a>                    
					</div>                
				</div>            
			</div>        
		</div>    
	</div>
</div>
<div class="mb-0 v-card">    
	<div class="home-v2-four-banner-wrap px-1" moduletype="2003" data-src="" lazy="loading" style="padding-bottom:0.426667rem;">        
		<ul>            
			<li>              
				<img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803031614_661.png" />              
				<p class="text-overflow mt-1">
					Tops
				</p>
			</li>            
			<li>              
				<img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803031726_609.png" />              
				<p class="text-overflow mt-1">
					Bottoms
				</p>
			</li>            
			<li>              
				<img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803033756_660.png" />              
				<p class="text-overflow mt-1">
					Dresses
				</p>
			</li>            
			<li>              
				<img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803033829_619.png" />              
				<p class="text-overflow mt-1">
					Lingerie
				</p>
			</li>            
			<li class="last-line">              
				<img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803033901_216.png" />              
				<p class="text-overflow mt-1">
					shoes
				</p>
			</li>            
			<li class="last-line">              
				<img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803033926_934.png" />              
				<p class="text-overflow mt-1">
					Bags
				</p>
			</li>            
			<li class="last-line">              
				<img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803034004_217.png" />              
				<p class="text-overflow mt-1">
					Accessories
				</p>
			</li>            
			<li class="last-line">              
				<img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803034054_845.png" />              
				<p class="text-overflow mt-1">
					Beauty
				</p>
			</li>        
		</ul>    
	</div>
</div>
<div class="mb-0 v-card">    
	<div class="customer-banner" style="padding-bottom:0.426667rem !important;">        
		<img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803034342_751.png" />    
	</div>
</div>
<div class="mb-0 v-card">    
	<div class="home-v2-banner-with-category" style="padding-bottom:0.426667rem; ">        
		<div>            
			<ul class="display-flex pt-2">              
				<li class="px-1">                
					<div class="pa-2 category-img">                  
						<img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803034614_854.png" />                
					</div>                
					<p class="text-overflow px-2">
						Socofy
					</p>
				</li>              
				<li class="px-1">                
					<div class="pa-2 category-img">                  
						<img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803034709_246.png" />                
					</div>                
					<p class="text-overflow px-2">
						Gracila
					</p>
				</li>              
				<li class="px-1">                
					<div class="pa-2 category-img">                  
						<img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803062802_374.png" />                
					</div>                
					<p class="text-overflow px-2">
						O-NEWE
					</p>
				</li>              
				<li class="px-1">                
					<div class="pa-2 category-img">                  
						<img alt="fecmall" class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecwbbc/20200803062814_786.png" />                
					</div>                
					<p class="text-overflow px-2">
						Lostisy
					</p>
				</li>            
			</ul>            
			<div class="separating-banner ba1">              
				<div class="separating-banner-content separating-banner-subtitle">                
					<span>UP TO 60%OFF</span>
				</div>              
				<div class="separating-banner-content separating-banner-title">                
					<span>Vintage Shoes</span>
				</div>              
				<div class="separating-banner-content separating-banner-button">                
					<span class="px-2">buy now &gt;</span>
				</div>            
			</div>        
		</div>    
	</div>
</div>                  

```










