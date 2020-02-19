FecMall Fecbdct 囤货系统安装
=================

###  Fecbdct 囤货系统安装



1.安装之前，必须安装Fecbbc多商户应用，Fecbdc多商户分销应用

2.后台应用中心，安装Fecbdct应用扩展

3.设置应用优先级`priority`

第2步骤在线安装应用后，需要设置fecbbc,fecbdc,fecbdct三个应用的优先级，登陆平台后台：`应用中心` --> `应用管理` --> `已安装应用`

fecbbc: `priority`  设置为 `1`

fecbdc: `priority` 设置为 `2`

fecbdct: `priority` 设置为 `3`


4.设置模板路径

4.1 Appfront设置store，为store添加模板路径

后台Appfront store：`网站配置`--> `appfront配置` --> `store配置`

> 注意：激活的store都需要设置，点击编辑，在编辑框 `第三方模板路径`中填写下面的内容

```
@fecbdct/app/appfront/theme/fecbdct,@fecbdc/app/appfront/theme/fecbdc,@fecbbc/app/appfront/theme/fecbbc
```



4.1 Apphtml设置store，为store添加模板路径

后台Apphtml5 store：`网站配置`--> `apphtml5配置` --> `store配置`

> 注意：激活的store都需要设置，点击编辑，在编辑框 `第三方模板路径`中填写下面的内容

```
@fecbdct/app/apphtml5/theme/fecbdct,@fecbdc/app/apphtml5/theme/fecbdc,@fecbbc/app/apphtml5/theme/fecbbc
```


5.至此就设置好了









