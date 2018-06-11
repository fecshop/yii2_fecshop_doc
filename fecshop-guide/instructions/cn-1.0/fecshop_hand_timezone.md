Fecshop 如何设置时区 timeZone
========================




只需要在  @app/config/main.php中加入配置即可

> @app是统称，代表 @appfront  @apphtml5  @appserver等入口


```
return [
    'id'       => 'app-front',
    // 设置时区，查看php 支持的所支持的时区列表  ：http://www.php.net/manual/zh/timezones.php
    'timeZone' => 'UTC',
    'basePath' => dirname(__DIR__),
    ...
	
```
如果想设置东八区，就用  `Asia/Shanghai`

查看php 支持的所支持的时区列表  ：http://www.php.net/manual/zh/timezones.php







