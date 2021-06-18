ERP站点配置管理
===========

> 添加和管理站点的部分

### ERP站点

1.您可以在后台添加站点信息

![](fecerp21_1.jpg)


### 站点类型

在添加站点的时候，您可以看到这里有一个站点类型

![](fecerp21_2.jpg)


如果您想添加新的站点类型，您可以在您的插件配置中进行添加


1.添加商城站点类型

`@fecerp/config.php `配置文件中，您可以看到fecerp的默认`商城站点类型`

```
'services' => [
    ...
    'mallsite' => [
        'class' => 'fecerp\services\Mallsite',
        'typeConfig' => [
            [
                'key' => 'fecmall',
                'label' => 'Fecmall',
            ],
            [
                'key' => 'woocommerce',
                'label' => 'WooCommerce',
            ],
            [
                'key' => 'shopify',
                'label' => 'Shopify',
            ],
        ],
    ],
],
```

您可以在您的插件或者本地开发中，在services - mallsite 配置中，添加`typeConfig`的子项，譬如:


```
'services' => [
    ...
    'mallsite' => [
        'typeConfig' => [
            [
                'key' => 'magento',
                'label' => 'Magento',
            ],
        ],
    ],
],
```



2.添加完了子项，您在 `基础管理`  --> `基础管理`  --> `网站配置` 中，
进行`添加`站点, 在`类型`下拉条部分，可以看到您新建的站点类型

您可以添加您的站点信息。

3.站点类型，并不仅仅是在这里添加一个类型，您需要实现产品的对接，订单的对接等等一系列的工作
，这是一个插件级别的工作量。

















