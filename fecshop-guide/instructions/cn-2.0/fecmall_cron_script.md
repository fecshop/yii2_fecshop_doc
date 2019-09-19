Fecmall Cron 脚本
===============

> 需要在线上设置的定时脚本。脚本地址在@fecshop/shell路径下面



1.每天一次脚本：

computeProductFinalPrice.sh

2.时间间隔：将pending订单（创建时间）未支付超过30分钟的订单取消，并归还产品库存。

returnPendingProductQtyStock.sh

3.使用工具脚本

urlRewrite.sh url重写的脚本，这个脚本在url 重写不准确或者其他情况下需要
手动跑一次，用来纠正url 重写的数据问题

fullSearchSync.sh这个脚本是产品搜索生成mongodb产品相应语言的full Text Search表
的脚本。











