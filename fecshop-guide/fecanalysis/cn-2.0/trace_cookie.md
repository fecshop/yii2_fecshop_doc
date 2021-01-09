Cookie说明
=============

> 打点的js，会在浏览器留下cookie，这里对所有的cookie进行说明

1.js追踪cookie

`_fta` ：过期时间为100年,该cookie中存储生成的唯一标识码uuid，， 用来标示用户，另外，和_fto，协同判断是否是老用户

`_fto`： 过期时间为0.6天，也就是14.4小时，用户每次访问，都会更新过期时间， 如果用户超过14.4小时，在继续访问网站，会被认为是新的访问，用户访问的页面 会被认为是着陆页，另外用户会被认为第二次访问，设置cookie _ftreturn，标示成老客户

`_ftreturn`： 过期时间为100年，用来标示是否是老用户 ，通过 _fta 和_fto 协同判断是否是老用户来 判断是否是老客户

`_ftreferdomain`：过期时间为0.6天，也就是14.4小时，字段first_referrer_domain来自于该cookie，也就是用户的来源域名 ，从用户的着陆页的refer url取值，由于用户的着陆页有一定概率加载js失败， 会造成用户的第二个页面被系统判定成着陆页，这种情况会被当做redirect(直接访问处理)， 这种概率还是比较小，也只能这样来处理，这样处理的结果会让直接访问用户的数据偏大一些。

`_ftactivity`： 该cookie 和_ftreferdomain 设置相同的过期时间，记录用户首次访问网站（0.6天内的首次）着陆页的页面类型，目前有值    `sku_page`, `category_page`,  `search_page`,  `home_page`。

`_ftactivity_child`：和上面的`_ftactivity`对应，如果`_ftactivity`的值为`sku_page`,那么这里的值为sku的值，其他类似

`_ftreferurl`: 用户首次访问的来源url（完整的url）

`_fta_site_id`: website_id， 网站的唯一标示。

2.广告追踪cookie

`fid`: 广告的唯一标示，过期时间为15天

`fec_source`: 广告的渠道，过期时间为15天

`fec_medium`: 广告的子渠道，过期时间为15天

`fec_campaign`: 广告的活动，过期时间为15天

`fec_content`: 广告的推广员，过期时间为15天

`fec_design`: 广告的图片设计美工，过期时间为15天











