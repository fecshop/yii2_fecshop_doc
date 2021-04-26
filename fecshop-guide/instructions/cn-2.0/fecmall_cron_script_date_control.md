Fecmall cron脚本时间区间控制
==================

> 通过时间区间，进行处理数据的脚本等，譬如按照时间端更新库存，按照时间段进行订单推送，
都需要一个时间区间搜索数据空，而且这个时间段的数据只处理一次，不能重复执行，
另外，这个时间段的数据处理失败怎么办？如果时间段过早（譬如大于当前时间）造成数据漏了怎么办？
本部分是fecmall开发的services，帮助此问题的解决。

### 场景举例


推送Fecmall订单到ERP

1.第一次推送的开始时间设置x月前，作为订单过滤的开始时间

2.开始时间加上一个值，作为结束时间，譬如：
`BeginAt` `2021-04-26 10:10:10`  至  `EndAt` `2021-04-26 20:10:10` 

3.脚本执行完成后，下一次执行脚本的`EndAt`，作为下次脚本的`BeginAt`。

4.如果脚本执行报错，终端等失败，或者脚本未执行完成等，那么下次脚本cron执行将无法执行
，当超过某个阈值，才允许重新执行该时间段的脚本

5.计算出来的`EndAt`，有一个最大值，譬如当前时间 - 300（s）,作为`最大值`，当超过`最大值`则以该值作为
`EndAt`的值。

譬如：

`list($beginAt, $endAt) = Yii::$service->helper->scriptDate->getProcessBeginAndEndAt($this->scriptTypeName);`

得到过滤的开始和结束时间。

### Fecmall cron脚本时间区间控制

文件：@fecshop/services/helper/ScriptDate.php


1.初始化参数，您可以在您的init()方法中执行，也可以不执行，使用默认值

```
public function init()
{
    $this->scriptTypeName = 'orderPush';
    /**
     * initParam 函数参数说明
     * @param $init_begin_before_days | int,  第一次执行脚本，默认的数据开始时间
     * @param $date_interval | int, 如果没有传递参数，则使用默认的时间间隔，默认一个小时的间隔
     * @param $maxEndDateLimit ， 脚本结束时间，最大不能离当前时间多少s, 也就是说  脚本的end_at <= time() - $this->maxEndDateLimit, 如果超过这个值，那么强制让 end_at = time() - $this->maxEndDateLimit
     * @param $processTimeout， 脚本运行的超时时间，让超过3600，将会强制初始化数据，重新执行。
     */
    Yii::$service->helper->scriptDate->initParam(30, 3600*24*30, 300, 3600);
}

```

2.进行init创建

```
/**
 * 1.初始化脚本
 */
public function actionInitscript()
{
    $initStatus = Yii::$service->helper->scriptDate->initScript($this->scriptTypeName);
    if ($initStatus) {
        echo 'OK';
    }
}
```

如果该脚本第一次创建，或者上个脚本已经执行完成，那么`$initStatus`将会为true，
如果脚本已经创建未开始执行，或者正在执行，就会返回false。

3.开始执行

```
/**
 * 2.开始执行脚本
 */
public function actionProcessscript()
{
    $status = Yii::$service->helper->scriptDate->processScript($this->scriptTypeName);
    if ($status) {
        echo 'OK';
    }
}
```

执行脚本前，先执行该部分，表示已经开始处理脚本


4.在执行脚本中，得到当前脚本执行的开始和结束时间

```
list($beginAt, $endAt) = Yii::$service->helper->scriptDate->getProcessBeginAndEndAt($this->scriptTypeName);
if (!$beginAt || !$endAt) {
    
    return null;
}
```


5.脚本执行过程中，如果存在错误，可以写入数据表

多个错误都会持续写入表`script_date_control`的`error_info`字段，可以通过下面的代码执行

```
Yii::$service->helper->scriptDate->updateScriptErrorInfo($this->scriptTypeName, $errors);
```

6.脚本执行后，进行状态标记更改

```
/**
 * 3.完成执行脚本
 */
public function actionCompletescript()
{
    $status = Yii::$service->helper->scriptDate->completeScript($this->scriptTypeName);
    if ($status) {
        echo 'OK';
    }
}
```


7.您可以在外层shell进行控制，譬如：

7.1shell文件

```
#!/bin/sh
Cur_Dir=$(cd `dirname $0`; pwd)
# get product all count.
initStatus=`$Cur_Dir/../../../../yii jsterp/order/initscript`
if [ "$initStatus" = "OK" ]; then
  echo "##############ALL BEGINING###############";
  processStatus=`$Cur_Dir/../../../../yii jsterp/order/processscript`
  if [ "$processStatus" = "OK" ]; then
    echo "Begin process.."
    pagenum=`$Cur_Dir/../../../../yii jsterp/order/pagecount`
    echo "There are $pagenum pages to process"
    echo "##############ALL BEGINING###############";
    for (( i=1; i<=$pagenum; i++ ))
    do
      $Cur_Dir/../../../../yii jsterp/order/pushorder $i
      echo "Page $i done"
    done
  fi
  completeStatus=`$Cur_Dir/../../../../yii jsterp/order/completescript`
  echo "##############ALL COMPLETE###############";
fi



```

7.2console controller文件：

```
<?php
/**
 * FecShop file.
 *
 * @link http://www.fecshop.com/
 * @copyright Copyright (c) 2016 FecShop Software LLC
 * @license http://www.fecshop.com/license/
 */

namespace fecjst\app\console\modules\Jsterp\controllers;

use Yii;
use yii\console\Controller;

/**
 * @author Terry Zhao <2358269014@qq.com>
 * @since 1.0
 */
class OrderController extends Controller
{
    public $scriptTypeName;
    public $firstBeforedays = 30;
    public $numPerPage=10;
    protected $initBeginDateTimestamp;
    
    public function init()
    {
        $this->scriptTypeName = Yii::$service->jsterp->order->scriptTypeName;
        /**
         * initParam 函数参数说明
         * @param $init_begin_before_days | int,  第一次执行脚本，默认的数据开始时间
         * @param $date_interval | int, 如果没有传递参数，则使用默认的时间间隔，默认一个小时的间隔
         * @param $maxEndDateLimit ， 脚本结束时间，最大不能离当前时间多少s, 也就是说  脚本的end_at <= time() - $this->maxEndDateLimit, 如果超过这个值，那么强制让 end_at = time() - $this->maxEndDateLimit
         * @param $processTimeout， 脚本运行的超时时间，让超过3600，将会强制初始化数据，重新执行。
         */
        Yii::$service->helper->scriptDate->initParam(30, 3600*24*30, 300, 3600);
    }
    /**
     * 1.初始化脚本
     */
    public function actionInitscript()
    {
        $initStatus = Yii::$service->helper->scriptDate->initScript($this->scriptTypeName);
        if ($initStatus) {
            echo 'OK';
        }
    }
    /**
     * 2.开始执行脚本
     */
    public function actionProcessscript()
    {
        $status = Yii::$service->helper->scriptDate->processScript($this->scriptTypeName);
        if ($status) {
            echo 'OK';
        }
    }
    /**
     * 3.完成执行脚本
     */
    public function actionCompletescript()
    {
        $status = Yii::$service->helper->scriptDate->completeScript($this->scriptTypeName);
        if ($status) {
            echo 'OK';
        }
    }
    
    public function actionPagecount()
    {
        $orderData = $this->getOrders();
        if (!$orderData['count']) {
            echo "0";
        } else {
            echo ceil($orderData['count'] / $this->numPerPage);
        }
        
    }
    
    /**
     * 推送订单信息
     */
    public function actionPushorder($pageNum)
    {
        $orderData = $this->getOrders($pageNum);
        $orders = $orderData['coll'];
        
        if (!Yii::$service->jsterp->order->pushOrder($orders)) {
            $errors = Yii::$service->helper->errors->get(', ');
            // 记录错误信息。
            Yii::$service->helper->scriptDate->updateScriptErrorInfo($this->scriptTypeName, $errors);
            
            return false;
        }
        
        return true;
    }
    /**
     * 得到订单信息
     */
    public function getOrders($pageNum=1)
    {
        list($beginAt, $endAt) = Yii::$service->helper->scriptDate->getProcessBeginAndEndAt($this->scriptTypeName);
        if (!$beginAt || !$endAt) {
            
            return null;
        }
        $filter = [
            'where' => [
                ['>=', 'created_at', $beginAt],
                ['<', 'created_at', $endAt],
                ['in', 'order_status', [
                    Yii::$service->order->payment_status_confirmed
                ]],
            ],
            'asArray' => true,
            'pageNum' => $pageNum,
            'numPerPage' => $this->numPerPage,
        ];
        $orders = Yii::$service->order->coll($filter);
        
        return $orders;
    }
    
    
}
```


### 说明

1.ScriptDate service的默认值：

```
// 第一次执行脚本，默认的数据开始时间
public $init_begin_before_days = 30;
// 如果没有传递参数，则使用默认的时间间隔，默认一个小时的间隔
public $date_interval = 3600;
// 脚本结束时间，最大不能离当前时间多少s, 也就是说  脚本的end_at <= time() - $this->maxEndDateLimit, 如果超过这个值，那么强制让 end_at = time() - $this->maxEndDateLimit
public $maxEndDateLimit = 300;
// 脚本运行的超时时间，让超过3600，将会强制初始化数据，重新执行
public $processTimeout = 3600;
```

您可以通过`Yii::$service->helper->scriptDate->initParam(30, 3600*24*30, 300, 3600);`来设置默认值

2.存储数据的表：`script_date_control`



3.如果脚本执行过程中出现了错误，可以通过`Yii::$service->helper->scriptDate->updateScriptErrorInfo($this->scriptTypeName, $errors);`
写入表字段`error_info`,如果该字段为空，那么执行`completeScript($scriptTypeName)`函数将会失败
，譬如执行`$status = Yii::$service->helper->scriptDate->completeScript($this->scriptTypeName);`
将会返回false。



5.关于该部分的执行，可以参看扩展：http://addons.fecmall.com/92147744















