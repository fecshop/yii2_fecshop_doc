ERP订单处理简介
=========

> erp通过定时脚本，拖取各个商城平台的订单到erp数据库，
然后进行订单审核，生成包裹，包裹合并和拆分，包裹发货等等一系列工作，
进行订单的发货操作


### Erp订单处理流程


1.ERP订单数据拖取

定时脚本操作，通过api，将商城平台的订单，保存到erp的数据库中，详细参看
：[ERP订单数据拖取](fecmall_fecerp_order_pull.md)

2.ERP订单生成包裹

包裹，就是快递发货的单位，一般一个订单对应一个包裹，但是也存在一个订单几个包裹的情况，因此，通过该
功能生成包裹，详细参看：[ERP订单生成包裹](fecmall_fecerp_order_package_generate.md)

3.订单包裹管理

订单生成包裹后，我们可以在这里查看包裹，以及进行包裹的合并，包裹的进一步拆分
，包裹的快递方式，重量更新，以及包裹的删除等操作，详细参看：
[ERP订单包裹管理](fecmall_fecerp_order_package_manager.md)
 
 通过这里可以看到，订单和包裹的关系，是多对多的关系（虽然大多数实际情况是一对一的关系），
 一个订单可以有多个包裹，一个包裹同样可以里面包含多个订单的商品，包裹的拆分和合并就可以满足该情况。
 
4.ERP订单包裹发货
 
 包裹处理完成后，就可以进行包裹发货操作，这里填写包裹的重量，包裹的快递方式，运单号，快递费用等，进行包裹发货操作，
 您可以进行`包裹信息excel导出`,`包裹批量excel发货`操作
 ，详细参看：
[ERP订单包裹发货](fecmall_fecerp_order_package_dispatch.md)

5.ERP订单运单打印

详细参看：
[ERP订单运单打印](fecmall_fecerp_order_package_shipping_print.md)

6.ERP订单扩展其他平台

erp的订单部分，目前只对接了fecmall，但是您可以对接其他的商城平台，fecerp在架构上做了更好的支持，详细参看：
[ERP订单扩展其他平台](fecmall_fecerp_order_other_platform.md)




























