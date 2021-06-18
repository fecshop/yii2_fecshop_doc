ERP订单扩展其他平台
============

> 目前erp对接了fecmall商城，如果您想要对接其他的商城平台，譬如magento，shopify等，
您可以参看该部分，熟悉对接框架逻辑，方便的对您您自己的商城平台，
框架层面，支持扩展独立插件包的方式，进行其他的站点平台的添加。


### 订单数据对接内容


1.`商城平台`的订单数据，erp通过脚本拖取，保存到erp

2.erp订单状态，物流信息，同步到商城`商城平台`


### 订单对接框架逻辑解析

此部分是通过代码层面，对其原理进行解析。



cron计划任务执行console入口脚本，通过api获取`商城平台`的订单，然后保存到erp数据库中

目前订单部分的对接内容


1.脚本文件：`addons/fecmall/fecerp/shell/order.sh`，在下面的脚本加入了注释，也就是 `////`开头的部分，您参看
注释了解shell的代码的具体作用。

```
#!/bin/sh
Cur_Dir=$(cd `dirname $0`; pwd)
# get product all count.
//// 获取商城的页数，因为每一页的个数为1，因此，这里的页数等于site总个数（因为erp对接的是多个商城，因此需要每个商城单独处理）
sitepagenum=`$Cur_Dir/../../../../yii base/site/pagecount`  

echo "There are $sitepagenum pages to process"
echo "##############ALL BEGINING###############";
for (( i=1; i<=$sitepagenum; i++ ))
do
    //// 获取当前页的商城siteId（每一页只有一个数据）
    siteId=`$Cur_Dir/../../../../yii base/site/getsiteid $i`
    echo "##############ORDER PULL BEGINING###############";
    //// 脚本控制部分，通过时间区间获取订单，将时间区间写入表，状态为初始状态
    initStatus=`$Cur_Dir/../../../../yii base/order/initscript $siteId`
    //// 如果Script初始化成功，则执行
    if [ "$initStatus" = "OK" ]; then
        echo "begin process script [siteId: $siteId ]...";
        //// 更改Script状态为 process
        processStatus=`$Cur_Dir/../../../../yii base/order/processscript $siteId`
        if [ "$processStatus" = "OK" ]; then
            echo "Begin process..."
            hasError="OK"
            //// 获取订单的总个数（这里是通过api访问商城平台获取的订单总数）
            pagenum=`$Cur_Dir/../../../../yii base/order/pagecount $siteId`
            echo "There are $pagenum[order] pages to process"
            if [ -n "$pagenum" ]; then
                //// 根据分页，循环处理
                for (( j=1; j<=$pagenum; j++ ))
                do
                    //// 拖取 商城平台 当前页的订单数据，并保存到数据库
                    pullorderStatus=`$Cur_Dir/../../../../yii base/order/pullorder $siteId $j`
                    echo "pullorderStatus: $pullorderStatus"
                    //// 拖取 商城平台 当前页的订单 成功
                    if [ "$pullorderStatus" = "OK" ]; then
                        echo "Page $j done"
                    else
                        hasError="ERROR"  //// 拖取 商城平台 当前页的订单 成功
                    fi
                done
                //// 如果执行成功，则Script标记为完成。
                if [ "$hasError" = "OK" ]; then
                    completeStatus=`$Cur_Dir/../../../../yii base/order/completescript $siteId`
                    echo "completeStatus...";
                fi
            fi
        fi
    fi
    echo "##############ORDER PULL COMPLETE###############";

    echo "##############ORDER STATUS BEGINING###############";    
    initStatus=`$Cur_Dir/../../../../yii base/orderstatus/initscript $siteId`
    if [ "$initStatus" = "OK" ]; then
        echo "begin process script [siteId: $siteId ]...";
        processStatus=`$Cur_Dir/../../../../yii base/orderstatus/processscript $siteId`
        if [ "$processStatus" = "OK" ]; then
            echo "Begin process..."
            hasError2="OK"
            pagenum=`$Cur_Dir/../../../../yii base/orderstatus/pagecount $siteId`
            echo "There are $pagenum[orderstatus] pages to process"
            if [ -n "$pagenum" ]; then
                for (( j=1; j<=$pagenum; j++ ))
                do
                    updateorderStatus=`$Cur_Dir/../../../../yii base/orderstatus/updateorder $siteId $j`
                    echo "updateorderStatus: $updateorderStatus"
                    if [ "$updateorderStatus" = "OK" ]; then
                        echo "Page $j done"
                    else
                        hasError2="ERROR"
                        echo "[[Page $j]] ERROR"
                    fi
                done
                if [ "$hasError2" = "OK" ]; then
                    completeStatus=`$Cur_Dir/../../../../yii base/orderstatus/completescript $siteId`
                    echo "completeStatus...";
                fi
            fi
        fi
    fi
    echo "##############ORDER STATUS COMPLETE###############";
done
echo "##############ALL COMPLETE###############";

```



2.脚本控制

订单数据拖取，是通过时间区间进行查询拖取的，当次执行完成后的endAt时间戳，就是下一次执行脚本的beginAt时间戳

当然，这个过程要考虑订单拖取的失败情况，时间区间的限制情况，等等，这个部分的控制是fecmall
的`Fecmall cron脚本时间区间控制`机制来完成的，原理详细参看：
[Fecmall cron脚本时间区间控制](https://www.fecmall.com/doc/fecshop-guide/instructions/cn-2.0/guide-fecmall_cron_script_date_control.html)


3.拖取订单数据的部分

通过shell代码：

```
pullorderStatus=`$Cur_Dir/../../../../yii base/order/pullorder $siteId $j`
```

了解到，对应console入口的 `base/order/pullorder`.

我们打开这个文件：`@fecerp\app\console\modules\Base\controllers\OrderController.php`

```
/**
     * @param $siteId | int 
     * @param $pageNum | int, 第x页数据
     * 拖取siteId对应的订单信息，进行保存。
     */
    public function actionPullorder($siteId, $pageNum)
    {
        $orderData = $this->getOrders($siteId, $pageNum);
        $orders = $orderData['coll'];
        if (!is_array($orders) || empty($orders)) {
            
            echo 'OK';exit;
            //return true;
        }
        // 初始化对应的order services
        //Yii::$service->orderapi->initServiceBySiteId($siteId) ;
        foreach ($orders as $order) {
            if (!Yii::$service->orderapi->saveOrder($order, $siteId)) {
                $errors = Yii::$service->helper->errors->get(', ');
                // 记录错误信息。
                Yii::$service->helper->scriptDate->updateScriptErrorInfo($this->scriptTypeName, $errors);
                
                var_dump($errors); exit;
                //return false;
            }
            
        }
        
        echo 'OK';exit;
        //return true;
    }
```

这个函数，进行订单数据的拖取，订单数据的保存，详细的代码执行，您需要自己查看代码


4.在文件：`@fecerp\app\console\modules\Base\controllers\OrderController.php`的函数

4.1代码分析

```
    public function getOrders($siteId, $pageNum=1)
    {
        Yii::$service->helper->scriptDate->initSiteId($siteId);
        // 初始化对应的order services
        Yii::$service->orderapi->initServiceBySiteId($siteId) ;
        
        
        return Yii::$service->orderapi->getApiOrders($siteId, $pageNum);
    }
```

初始化对应的order services： `Yii::$service->orderapi->initServiceBySiteId($siteId) ;`

打开@fecerp\service\Orderapi.php，找到这个函数，分析逻辑，可以看到主要作用是
初始化Orderapi service里面的 `$_orderApiService`
，譬如当Fecmall类型的站点，`$_orderApiService`对应的是`fecerp\services\orderapi\Fecmall.php`


4.2通过阅读代码，您可以得知
可以通过类变量`$orderApiServices`进行自定义文件路径
,譬如：

```
    $this->orderApiServices  =  [
        'magento' => '@fecerp/services/order/Magento'
    ]
```

当站点类型为`magento`的时候，`$_orderApiService`为'@fecerp/services/order/Magento'

4.3我们可以通过配置注入的方式，在自己的插件配置中，添加`orderApiServices`的配置项。



### 添加新的商城平台

上面了解了原理，我们这里添加新的商城平台，实例。

1.为新的商城平台（譬如：magento），添加站点，详细参看：[ERP站点配置管理](fecmall_fecerp_site_config.md)

3.在您的插件配置中，

在orderapi services中，注入配置`orderApiServices`


```
[
    'services' => [
        ...
        'orderapi' => [
            'orderApiServices' => [
                'magento' => '@myerp/services/order/Magento'
            ],
        ],
    ],
]
```

注意，这里的`magento`一定要和第1部分 `typeConfig`的`key`保持一致，可以看到他们的值都是
`magento`（大小写必须一致）。


4.实现@myerp/services/order/Magento.php

您可以参考 `@fecerp/services/order/Fecmall`

需要实现接口 `@fecerp\services\orderapi\OrderapiInterface`, 代码例子如下：

```

<?php
namespace myerp\services\orderapi;

use Yii;
use fecshop\services\Service;

/**
 * Order services.
 *
 * @property \fecshop\services\order\Item $item
 *
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class Magento extends Service implements OrderapiInterface
{
    
    public function init()
    {
        parent::init();
    }
    /**
     * @param $siteId | int，网站id
     * @param $pageNum | int，分页数
     * 通过api，得到订单信息（第x页）
     */
    public function getApiOrders($siteId, $pageNum=1)
    {
        
    }
    /**
     * @param $orderArr | array，订单的数组信息
     * @param $siteId | int
     * 保存订单信息
     */
    public function saveOrder($orderInfo, $siteId)
    {
        
    }
    /**
     * @param $order | array, 订单信息
     * 将订单状态的变动，更新到远程。
     */
    public function updateOrderStatus($order)
    {
    }
    
    
    
}




```

根据您的逻辑，实现里面的函数即可。



至此就完成了，当您执行order.sh的时候，如果执行到您新建的站点，站点是magento，就会执行
`myerp\services\orderapi\Magento`里面的函数。


这个部分，还是得靠自己都看代码看原理，独立插件包扩展性在框架层面是支持的。



