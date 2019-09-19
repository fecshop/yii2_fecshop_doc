Fecshop Admin Block Edit
====================

> 在appadmin block edit页面,也就是编辑页面，我们可以快速的生成编辑列表


### getEditArr - 得到编辑部分的配置

![](images/aaa2.png)

譬如打开 `@fecshop\app\appadmin\modules\Cms\block\article\Manageredit.php`
您会看到函数

```
public function getEditArr()
    {
        return [
            [
                'label'=>'标题',
                'name'=>'title',
                'display'=>[
                    'type' => 'inputString',
                    'lang' => true,
                ],
                'require' => 1,
            ],

            [
                'label'=>'Url Key',
                'name'=>'url_key',
                'display'=>[
                    'type' => 'inputString',
                ],
                'require' => 0,
            ],
        ...
        ];
    }
```

这个函数是为了更快的做编辑页面，也就是fecshop appadmin部分封装的方法，下面是对
这个配置函数里面的各个值的详细说明：

`label`: 【必填】标题

`name`: 【必填】对应到数据库字段

`require`: 【选填】是否必填

`display`: 【选填】显示的方式，下面有详细的说明

`display.lang`: 【选填】是否是多语言的方式显示，`true`代表多语言属性，不填写默认为 `false`

`display.type`: 【选填】`textarea` `select` `inputString` 三种方式，下面逐一说明

1.`inputString`

```
'display'=>[
    'type' => 'inputString',
    'lang' => true,    // 非多语言
],
```               

以`input输入框`的方式显示该编辑字段

2.`textarea`

```
'display'=>[
    'type' => 'textarea',
    'lang' => true,    // 多语言
    'rows'    => 14,   // 高度行数
    'cols'    => 110,  // 宽度
],
```                

以`textarea`文本内容的方式显示，并且是多语言的方式。

3.`select`

```
'display'=>[
    'type' => 'select',
    'data' => [
        1    => '激活',
        2    => '关闭',
    ],
],
```

以`select`的方式显示，`data`是select option部分的内容


原理：

您可以参看文件
`fecshop\app\appadmin\modules\AppadminbaseBlockEdit.php`
的方法：
`public function getEditBar($editArr = [])`

查看具体的实现原理。




