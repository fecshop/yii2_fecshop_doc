Fecmall-应用安装和加载原理
===========

当您申请成功开发者后就可以开发应用了

### Fecmall应用的安装原理

1.后台应用列表

在后台，应用中心，可以看到我的应用列表（如果没有，自行去fecmall应用市场添加应用）

对应的文件为：@fecshop/app/appadmin/modules/System/controllers/ExtensionmarketController.php

可以看到，应用的信息是通过`$info = Yii::$service->extension->remoteService->getMyAddonsInfo();`
,远程加载的应用市场系统的api，获取数据展示的

2.应用的安装

对应的文件为：@fecshop/app/appadmin/modules/System/controllers/ExtensionmarketController.php

```
public function actionInstall()
    {
        $namespace = Yii::$app->request->get('namespace');
        $packageName = Yii::$app->request->get('packageName');
        $folderName = Yii::$app->request->get('folderName');
        $addonName = Yii::$app->request->get('addonName');
        
        //  进行zip文件下载到指定的文件路径
        $zipFilePath = Yii::$service->extension->remoteService->downloadAddons($namespace, $packageName, $folderName, $addonName);
        if (!$zipFilePath) {
            echo  json_encode([
                'statusCode' => '300',
                'message'    => Yii::$service->page->translate->__('download remote addons fail'),
            ]);
            exit;
        }
        // 进行zip文件的解压
        $dest_dir = dirname($zipFilePath);
        if (!Yii::$service->helper->zipFile->unzip($zipFilePath, $dest_dir, true, true)) {
            echo  json_encode([
                'statusCode' => '300',
                'message'    => Yii::$service->page->translate->__('unzip addons fail'),
            ]);
            exit;
        }
        // 删除zip压缩包 
        unlink($zipFilePath);
        
        // 将addons信息写入数据库
        $data = Yii::$service->extension->remoteService->getAddonsInfoByNamespace($namespace);
        if (!is_array($data)) {
            echo  json_encode([
                'statusCode' => '300',
                'message'    => Yii::$service->page->translate->__('get remote addons info by namespace fail'),
            ]);
            exit;
        }
        // 将远程获取的数据，保存到数据库中。
        if (!Yii::$service->extension->newInstallInit($data)){
            echo  json_encode([
                'statusCode' => '300',
                'message'    => Yii::$service->page->translate->__('init new install addon to db fail'),
            ]);
            exit;
        }
        // 进行插件的安装
        if (!Yii::$service->extension->administer->install($namespace)) {
            $errors = Yii::$service->helper->errors->get();
            echo  json_encode([
                'statusCode' => '300',
                'message'    => Yii::$service->page->translate->__($errors),
            ]);
            exit;
        }
        // 进行插件的升级
        if (!Yii::$service->extension->administer->upgrade($namespace)) {
            $errors = Yii::$service->helper->errors->get();
            echo  json_encode([
                'statusCode' => '300',
                'message'    => Yii::$service->page->translate->__($errors),
            ]);
            exit;
        }
        // 输入安装成功信息。
        echo  json_encode([
            'statusCode' => '200',
            'message'    => Yii::$service->page->translate->__('addons install success'),
        ]);
        exit;
    }

```

这个是安装应用的方法，打开代码可以看到做了这些事情


1.进行zip文件下载到指定的文件路径

2.进行zip文件的解压

3.删除zip压缩包 

4.将addons信息写入数据库

5.将远程获取的数据，保存到数据库中

6.进行插件的安装

7.进行插件的升级

8.完成


对于插件的安装部分，是在config.php中指定相应的文件，详细参看： [Fecmall-应用Config文件](fecmall-addons-developer-config-example.md)




### Fecmall 应用插件初始化加载原理

1.打开数据库表`extensions`，这个就是应用插件表，里面记录应用的安装状态，以及配置文件路径
`extensions`


2.在配置config初始化的时候，会加载这个表的配置，然后合并到配置中（只加载状态为激活的应用，如果
某个应用在后台关闭，那么不会被加载）

3.应用文件夹中的`config.php`,是应用配置文件，也就是`extensions`
对应的`config_file_path`，这个文件是约定好的，应用的入口配置文件必须是`config.php`


4.在初始化过程中，Fecmall的安装的所有的应用（状态激活），都会被加载
，就会进行配置合并，最终出来的是合并后的配置

5.关于fecmall-2重写的规则和fecmall-1版本语法规则类似，
不同的是加入了应用市场，可以在线安装，方便操作

fecmall的一些重写规则可以参考下fecmall-1的文档: http://www.fecmall.com/doc/fecshop-guide/develop/cn-1.0/guide-fecshop-rewrite-func.html

















