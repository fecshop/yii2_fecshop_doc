FecMall Fecyo 首页Banner以及静态块配置
=========================


> Fecyo在初始安装，需要对首页以及一些静态块，进行配置

### Fecyo 首页Banner以及静态块配置


首先，fecyo pc入口的产品页面，需要开启面包屑导航才能版面正常

后台：`网站配置` --> `Appfront配置`  --> `分类产品配置 ` 

将 `产品页面-显示面包屑导航` 设置成 `Yes`即可


![](images/aaa.png)

1.参数配置

在这里配置页面顶部的搜索词，以及首页各个板块的sku（在下面截图的右侧有注释）

![](images/fecyo1.png)

您可以按照下面的内容先填写上去,安装完成后，根据自己的需要更改

Hot Search: `卫衣,牛仔裤,运动鞋,椰子,nike,欧文`

Hot Product Skus：`testest,p10001-kahaki-xxl-t4,222212,22221,p10001-kahaki-xxl,p10001-black-m,op0002-33,men0003,men0001,sk0002,sk0003,sk0008`

Chaoliu Top Sku1：`sk10004-001,sk10003-001,sk10002-002,sk10002,sk1000-blue,sk2001-blue-zo`

Chaoliu Top Sku2：`men0003,men0001,sk0002,sk0003,sk0008`

Chaoliu Bottom Skus1：`sk10004-001,sk10003-001,sk10002-002,sk10002,sk1000-blue,sk2001-blue-zo`

Chaoliu Bottom Skus2：`men0003,men0001,sk0002,sk0003,sk0008`

New Product Skus：`testest,p10001-kahaki-xxl-t4,222212,22221,p10001-kahaki-xxl,p10001-black-m,op0002-33,men0003,men0001,sk0002,sk0003,sk0008,sk0002,sk0003,sk0008,sk1000-blue,sk0004,sk1000-khak`


2.首页的板块配置

后台菜单： cms-->静态块

![](images/fecyo2.png)

新建如下的静态块：（点击添加按钮）

2.1首页大图(PC)

标题：PC：首页大图

标识符：pc-home-big-img

内容：()

```
<ul class="bxslider">                
	<li style="">
        <a href="{{homeUrl}}" rel="nofollow" target="_blank" title="">
            <img src="{{imgBaseUrl}}/addons/fecyo/01b4983297a531dbc96d3e2897a25b4db8.jpg" alt="" />
        </a>                
	</li>                
	<li style="">                    
		<a href="{{homeUrl}}" rel="nofollow" target="_blank" title="">
            <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01d099c85d0b3768c1ae87fc5f996644b5.jpg" alt="" />
        </a>                
	</li>                
	<li style="">                    
		<a href="{{homeUrl}}" rel="nofollow" target="_blank" title="">
            <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01b4983297a531dbc96d3e2897a25b4db8.jpg" alt="" />
        </a>                
	</li>                
	<li style="">                    
		<a href="{{homeUrl}}" rel="nofollow" target="_blank" title="">
            <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01d099c85d0b3768c1ae87fc5f996644b5.jpg" alt="" />
        </a>                
	</li>            
</ul>
```

注意：对于内容部分，使用的是可视化编辑器，需要先点击`源代码`,然后在粘贴上面的`html`代码
，如图：


![](images/fecyo3.png)

另外因为是`中英双语`，粘贴了`en`语言后，点击`zh`语言，然后再点击`源代码`按钮，将上面的内容html代码粘贴上去

![](images/fecyo4.png)

下面的，其他的静态块的内容复制，和该处类似，都这样操作（可视化编辑器部分）


填写完成后保存即可

2.2

标识符：pc-home-brand

标题：PC：首页品牌

内容：(需要en和zh都填写，写法参看上面)

```
<div class="img-brand">            
	<ul class="img-list imgopacity clearfix">                
		<li class="img-item">
            <a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01b561858b258adfadf8339e93875bc0d4.jpg" alt="" />
            </a>                
		</li>                
		<li class="img-item">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01ed8d4e21fe64b563d6d6c05ad76f207a.jpg" alt="" />
            </a>                
		</li>                
		<li class="img-item">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/0151e8bbbed5ce5a2637e90f0031462e7c.jpg" alt="" />
            </a>                
		</li>            
	</ul>        
</div>        
<div class="logo-brand imgopacity" data-shownum="16">            
	<ul>                
		<li data-page="0">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/0132216eb633b1d2816a41ee0f71254bb4.jpg" alt="" />
            </a>                
		</li>                
		<li data-page="0">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01f36ddbfd7db68e783cdc3f6ca228f58b.jpg" alt="" />
            </a>                
		</li>
		<li data-page="0">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01bcbd9ec6c308dd0f60e4c85de08537f1.jpg" alt="" />
            </a>                
		</li>
		<li data-page="0">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/0132216eb633b1d2816a41ee0f71254bb4.jpg" alt="" />
            </a>                
		</li>
		<li data-page="0">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01bcbd9ec6c308dd0f60e4c85de08537f1.jpg" alt="" />
            </a>                
		</li>
		<li data-page="0">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01f36ddbfd7db68e783cdc3f6ca228f58b.jpg" alt="" />
            </a>                
		</li>
		<li data-page="0">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/0132216eb633b1d2816a41ee0f71254bb4.jpg" alt="" />
            </a>                
		</li>
		<li data-page="0">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01f36ddbfd7db68e783cdc3f6ca228f58b.jpg" alt="" />
            </a>                
		</li>
		<li data-page="0">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01bcbd9ec6c308dd0f60e4c85de08537f1.jpg" alt="" />
            </a>                
		</li>
		<li data-page="0">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01f36ddbfd7db68e783cdc3f6ca228f58b.jpg" alt="" />
            </a>                
		</li>
		<li data-page="0">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/0132216eb633b1d2816a41ee0f71254bb4.jpg" alt="" />
            </a>                
		</li>
		<li data-page="0">                    
			<a href="" target="_blank" title="">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01bcbd9ec6c308dd0f60e4c85de08537f1.jpg" alt="" />
            </a>                
		</li>            
	</ul>        
</div>
```

2.3


标识符：pc-home-hot-top

标题：PC：首页潮流上装

内容：


```
<div class="tpl-nav">                
	<div class="tpl-keywords">                    
		<a class="keywords0" title="" href="" target="_blank">
            <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/017be7cc88b521b7ebbcd6a71f4349eb7b.jpg" alt="" />
        </a>
        <a class="keywords1" title="" href="" target="_blank">
            <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01ed77a1c2c9d98aacaf5f90d74f865de4.jpg" alt="" />
        </a>                
	</div>                
	<div class="tpl-category clearfix">                    
		<a href="{{homeUrl}}" title="卫衣" target="_blank">卫衣</a>
        <a href="{{homeUrl}}" title="夹克" target="_blank">夹克</a>
        <a href="{{homeUrl}}" title="毛衣/针织" target="_blank">毛衣/针织</a>
        <a href="{{homeUrl}}" title="棉衣" target="_blank">棉衣</a>
        <a href="{{homeUrl}}" title="羽绒服" target="_blank">羽绒服</a>
        <a href="{{homeUrl}}" title="风衣" target="_blank">风衣</a>
        <a href="{{homeUrl}}" title="MADNESS" target="_blank">MADNESS</a>
        <a href="{{homeUrl}}" title="DC" target="_blank">DC</a>
        <a href="{{homeUrl}}" title="gxg.jeans" target="_blank">gxg.jeans</a>
        <a href="{{homeUrl}}" title="黑鲸" target="_blank">黑鲸</a>
        <a href="{{homeUrl}}" title="viishow" target="_blank">viishow</a>
        <a href="{{homeUrl}}" title="FYP" target="_blank">FYP</a>                
	</div>            
</div>            
<div class="tpl-brands imgopacity clearfix">                
	<ul>                    
		<li>                        
			<a title="" href="" target="_blank">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01a30bf3a6c3ee3ad4f843609b459683fc.jpg" alt="" />
            </a>                    
		</li>                    
		<li>                        
			<a title="" href="" target="_blank">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/018ca5fc999a69a404c6ecf37ca57d9a59.jpg" alt="" />
            </a>                    
		</li>                
	</ul>            
</div>            
```


2.4

标识符：pc-home-hot-bottom

标题：PC：首页潮流下装

内容：


```
<div class="tpl-nav">                
	<div class="tpl-keywords">                    
		<a class="keywords0" title="裤装" href="" target="_blank">
            <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/013eb545806c6c4b7acb8b4ba4455bb176.jpg" alt="" />
        </a>
        <a class="keywords1" title="新品VIP" href="" target="_blank">
            <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01456307d9fc3e62166b45b05356164a6b.jpg" alt="" />
        </a>                
	</div>                
	<div class="tpl-category clearfix">                    
		<a href="" title="休闲裤" target="_blank">休闲裤</a>
        <a href="" title="牛仔裤" target="_blank">牛仔裤</a>
        <a href="" title="运动裤" target="_blank">运动裤</a>
        <a href="" title="工装裤" target="_blank">工装裤</a>
        <a href="" title="束口裤" target="_blank">束口裤</a>
        <a href="" title="九分裤" target="_blank">九分裤</a>
        <a href="" title="多袋裤" target="_blank">多袋裤</a>
        <a href="" title="西裤" target="_blank">西裤</a>
        <a href="" title="COKEIN" target="_blank">COKEIN</a>
        <a href="" title="DUSTY" target="_blank">DUSTY</a>
        <a href="" title="NOTHOMME" target="_blank">NOTHOMME</a>
        <a href="" title="白卷BAIJUAN" target="_blank">白卷BAIJUAN</a>                
	</div>            
</div>            
<div class="tpl-brands imgopacity clearfix">                
	<ul>                        
		<li>                            
			<a title="" href="" target="_blank">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/0147b1d670f5e6391bd50b25517ebc9c65.jpg" alt="" />
            </a>
		</li>                        
		<li>                            
			<a title="" href="" target="_blank">
                <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/01c2ca174adf5e30c873a3e8016b800e1a.jpg" alt="" />
            </a>
		</li>                
	</ul>            
</div>
```



2.5

标识符：pc-footer-text

标题：PC：底部Footer文字条款


内容：


```
<div class="mod_service" clstag="h|keycount|btm|btmnavi_null01"> 
   <div class="grid_c1 mod_service_inner"> 
    <ul class="mod_service_list"> 
     <li class="mod_service_item"> 
      <div class="mod_service_unit"> 
       <h5 class="mod_service_tit mod_service_duo"> 多 </h5> 
       <p class="mod_service_txt"> 品类齐全，轻松购物 </p> 
      </div> </li> 
     <li class="mod_service_item"> 
      <div class="mod_service_unit"> 
       <h5 class="mod_service_tit mod_service_kuai"> 快 </h5> 
       <p class="mod_service_txt"> 多仓直发，极速配送 </p> 
      </div> </li> 
     <li class="mod_service_item"> 
      <div class="mod_service_unit"> 
       <h5 class="mod_service_tit mod_service_hao"> 好 </h5> 
       <p class="mod_service_txt"> 正品行货，精致服务 </p> 
      </div> </li> 
     <li class="mod_service_item"> 
      <div class="mod_service_unit"> 
       <h5 class="mod_service_tit mod_service_sheng"> 省 </h5> 
       <p class="mod_service_txt"> 天天低价，畅选无忧 </p> 
      </div> </li> 
    </ul> 
   </div> 
  </div> 
  <div class="mod_help" clstag="h|keycount|btm|btmnavi_null02"> 
   <div class="grid_c1 mod_help_inner"> 
    <div class="mod_help_list"> 
     <div class="mod_help_nav"> 
      <h5 class="mod_help_nav_tit"> 购物指南 </h5> 
      <ul class="mod_help_nav_con"> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">购物流程</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">会员介绍</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">生活旅行</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">常见问题</a> </li> 
      </ul> 
     </div> 
     <div class="mod_help_nav"> 
      <h5 class="mod_help_nav_tit"> 配送方式 </h5> 
      <ul class="mod_help_nav_con"> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">上门自提</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">211限时达</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">配送服务查询</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">配送费收取标准</a> </li> 
      </ul> 
     </div> 
     <div class="mod_help_nav"> 
      <h5 class="mod_help_nav_tit"> 支付方式 </h5> 
      <ul class="mod_help_nav_con"> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">货到付款</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">在线支付</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">分期付款</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">公司转账</a> </li> 
      </ul> 
     </div> 
     <div class="mod_help_nav"> 
      <h5 class="mod_help_nav_tit"> 售后服务 </h5> 
      <ul class="mod_help_nav_con"> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">售后政策</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">退款说明</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">返修/退换货</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">取消订单</a> </li> 
      </ul> 
     </div> 
     <div class="mod_help_nav"> 
      <h5 class="mod_help_nav_tit"> 特色服务 </h5> 
      <ul class="mod_help_nav_con"> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">夺宝岛</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">DIY装机</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">延保服务</a> </li> 
       <li> <a href="#" target="_blank" rel="noopener noreferrer">XE卡</a> </li> 
      </ul> 
     </div> 
    </div> 
   </div> 
  </div> 
  <div class="mod_copyright"> 
   <div class="grid_c1 mod_copyright_inner"> 
    <p class="mod_copyright_links" clstag="h|keycount|btm|btmnavi_null03"> <a href="#" target="_blank" rel="noopener noreferrer">关于我们</a> <span class="mod_copyright_split">|</span> <a href="#" target="_blank" rel="noopener noreferrer">联系我们</a> <span class="mod_copyright_split">|</span> <a href="#" target="_blank" rel="noopener noreferrer">联系客服</a> <span class="mod_copyright_split">|</span> <a href="#" target="_blank" rel="noopener noreferrer">合作招商</a> <span class="mod_copyright_split">|</span> <a href="#" target="_blank" rel="noopener noreferrer">商家帮助</a> <span class="mod_copyright_split">|</span> <a href="#" target="_blank" rel="noopener noreferrer">营销中心</a> </p> 
   </div> 
  </div> 
```


2.6

标识符：h5-home-big-img

标题：html5：首页走马灯大图


内容：

```
<li class="swiper-slide">                                    
	<a href="" rel="nofollow">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/014365ae72f06e68c48ba1566baecf2ca3.jpg" alt="" />
    </a>                                
</li>                                
<li class="swiper-slide">                                    
	<a href="" rel="nofollow">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/01e1ef638be664c48b2cff12ac2df669b9.jpg" alt="" />
    </a>                                
</li>                                
<li class="swiper-slide">                                    
	<a href="" rel="nofollow">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/013b92f998a13f679fc95d90ac4cb66e6f.jpg" alt="" />
    </a>                                
</li>
```

2.7

标识符：h5-home-banner-1

标题：html5：首页Banner图-1


内容：

```
<a href="" id="660775" name="" rel="nofollow">
    <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/019be8f0550695282ce0e4df698d3fcc19.jpg" alt="" />
</a>
```

2.8

标识符：h5-home-hot-category

标题：HTML5:首页热门分类


内容：

```
<li>                            
	<a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/011063f7c725099b0a3263716189d23650.jpg" alt="" /> 
    </a>                                                  
</li>                        
<li>                            
	<a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/011ed955f031d5fb868d33ec5b23126e3a.jpg" alt="" />   
    </a>                                                 
</li>                        
<li>                            
	<a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/011063f7c725099b0a3263716189d23650.jpg" alt="" /> 
    </a>                                                  
</li>                        
<li>                            
	<a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/011ed955f031d5fb868d33ec5b23126e3a.jpg" alt="" />   
    </a>                                                 
</li><li>                            
	<a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/011063f7c725099b0a3263716189d23650.jpg" alt="" /> 
    </a>                                                  
</li>                        
<li>                            
	<a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/011ed955f031d5fb868d33ec5b23126e3a.jpg" alt="" />   
    </a>                                                 
</li><li>                            
	<a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/011063f7c725099b0a3263716189d23650.jpg" alt="" /> 
    </a>                                                  
</li>                        
<li>                            
	<a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/011ed955f031d5fb868d33ec5b23126e3a.jpg" alt="" />   
    </a>                                                 
</li><li>                            
	<a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/011063f7c725099b0a3263716189d23650.jpg" alt="" /> 
    </a>                                                  
</li>                        
<li>                            
	<a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/011ed955f031d5fb868d33ec5b23126e3a.jpg" alt="" />   
    </a>                                                 
</li><li>                            
	<a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/011063f7c725099b0a3263716189d23650.jpg" alt="" /> 
    </a>                                                  
</li>                        
<li>                            
	<a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/011ed955f031d5fb868d33ec5b23126e3a.jpg" alt="" />   
    </a>                                                 
</li>
```

2.9

标识符：h5-home-banner-2

标题：HTML5:首页banner-2


内容：

```
<a href="" id="36565" name="" rel="nofollow">
    <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/0127c58fa36285867023956c8ae404b862.jpg" alt="" />
</a>
```


2.10

标识符：h5-home-hot-brand

标题：HTML5:首页热门品牌


内容：

```
<li class="brand">
    <a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/01cc288d428427b364d90a4f11ffa386da.jpg" alt="" />
    </a>                    
</li>                    
<li class="brand">                        
	<a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/01c8974023e2ffa1cab2379d46435aeb9b.jpg" alt="" />
    </a>                    
</li>                    
<li class="brand">
    <a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/011ff06f241dd5e9c8ecb0967d38a9a426.jpg" alt="" /> 
    </a>                    
</li>                    
<li class="brand">
    <a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/01cd938c716f1af66a932bc86fe7fd0873.jpg" alt="" />
    </a>                    
</li>                    
<li class="brand">
    <a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/01b003373ee1cec2660aba43e1128cdd23.jpg" alt="DC" />
    </a>                    
</li>                    
<li class="brand">
    <a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/019f125a2713ae74a849c3d8b58ab9abb6.jpg" alt="Genanx" />
    </a>                    
</li>                    
<li class="more">
    <a href="">
        <img class="lazyload" src="{{imgBaseUrl}}/images/lazyload.gif" data-src="{{imgBaseUrl}}/addons/fecyo/h5/0173088d664d59084d9dd61fa2d8b78908.png" alt="" />
    </a>                    
</li>
```

