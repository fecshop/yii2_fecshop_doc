Fecmall Fecbdc多商户分销-分销商和平台月结脚本
========================


> 以月为单位，统计分销商和平台利润的脚本

### 分销商分成计算逻辑

1.此脚本跑之前，必须先跑该脚本：[分销商和平台利润计算脚本](fecmall-fecbdc-script-distribute-profit.md)

因为月结脚本，使用的是该脚本计算的结果数据，在这个基础上，继续跑的数据。

2.该脚本计算完后，将结果写入数据表中，分销商，平台商都可以查看


### 脚本计算

```
cd ./addons/fecmall/fecbdc/shell

# 操作1
sh monthStatisticsDistributeAndPlatformProfit.sh  # 默认跑上一月的数据
# 操作2
sh monthStatisticsDistributeAndPlatformProfit.sh 2020 01 #跑2020年1月份的数据

```

您可以在需要月结的时候，跑这个脚本


