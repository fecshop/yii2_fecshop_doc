Fecmall Rss订阅
==========

> 将产品信息生成xml格式的rss信息，供外部订阅


#### Fecmall Rss订阅

譬如：

http://fecshop.appfront.fancyecommerce.com/cms/rss/product

```
<?xml version="1.0" encoding="utf-8"?>
<rss version="2.0" xmlns:content="http://purl.org/rss/1.0/modules/content/" xmlns:wfw="http://wellformedweb.org/CommentAPI/" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:atom="http://www.w3.org/2005/Atom" xmlns:sy="http://purl.org/rss/1.0/modules/syndication/" xmlns:slash="http://purl.org/rss/1.0/modules/slash/" xmlns:georss="http://www.georss.org/georss" xmlns:geo="http://www.w3.org/2003/01/geo/wgs84_pos#" xmlns:media="http://search.yahoo.com/mrss/">
  <channel>
    <atom:link href="http://fecshop.appfront.fancyecommerce.com" rel="self" type="application/rss+xml"></atom:link>
    <generator>Fecmall Generator 2.15.0</generator>
    <docs>http://www.rssboard.org/rss-specification</docs>
    <title>fecmall rss feed title</title>
    <link>http://fecshop.appfront.fancyecommerce.com</link>
    <description>fecmall rss feed description</description>
    <language>en-US</language>
    <image>
      <url>http://img.fancyecommerce.com/media/upload/s/eu/seukemj98l87ist1591599212.png</url>
      <title>fecmall rss feed title</title>
      <link>http://fecshop.appfront.fancyecommerce.com</link>
      <width>379</width>
      <height>70</height>
      <description>fecmall rss image title</description>
    </image>
    <item>
      <title>test computer1111</title>
      <description>3333</description>
      <link>http://fecshop.appfront.fancyecommerce.com/test-computer1111-27289239</link>
      <author>fecmall terry</author>
      <guid>http://fecshop.appfront.fancyecommerce.com/test-computer1111-27289239 Thu, 10 Jun 2021 23:01:10 +0800</guid>
      <media:content url="http://img.fancyecommerce.com/media/catalog/product/f/yf/fyfvari26ef8m241612879330.jpg" medium="image">
        <media:title type="html">test computer1111</media:title>
      </media:content>
      <pubDate>Tue, 22 Jun 2021 01:55:47 +0800</pubDate>
    </item>
    <item>
      <title>999999</title>
      <description>4525432523523452234</description>
      <link>http://fecshop.appfront.fancyecommerce.com/weixin-test8787-98641834</link>
      <author>fecmall terry</author>
      <guid>http://fecshop.appfront.fancyecommerce.com/weixin-test8787-98641834 Wed, 12 May 2021 13:26:58 +0800</guid>
      <media:content url="http://img.fancyecommerce.com/media/catalog/product/f/z3/fz3dmlpqzhkwbh61618929078.png" medium="image">
        <media:title type="html">999999</media:title>
      </media:content>
      <pubDate>Tue, 22 Jun 2021 05:01:47 +0800</pubDate>
    </item>
    <item>
      <title>999999</title>
      <description>4525432523523452234</description>
      <link>http://fecshop.appfront.fancyecommerce.com/weixin-test8787-26697359</link>
      <author>fecmall terry</author>
      <guid>http://fecshop.appfront.fancyecommerce.com/weixin-test8787-26697359 Wed, 12 May 2021 13:26:57 +0800</guid>
      <media:content url="http://img.fancyecommerce.com/media/catalog/product/i/9u/i9uyqwaf7ss6o3f1618928080.png" medium="image">
        <media:title type="html">999999</media:title>
      </media:content>
      <pubDate>Tue, 22 Jun 2021 02:28:21 +0800</pubDate>
    </item>
</channel>
</rss>

```
目前该部分，是以扩展的方式实现，按照pinterest rss feed格式开发的

详细参看文档：[Fecmall扩展-Rss & Pinterest Feed](https://www.fecmall.com/doc/fecshop-guide/addons/cn-2.0/guide-fecmall-addons-rss-feed.html)






















