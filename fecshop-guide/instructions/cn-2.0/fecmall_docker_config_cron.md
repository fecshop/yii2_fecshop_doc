Docker安装fecmall配置cron
===========================

如果是docker安装的fecmall，php是在容器里面，如果配置cron，
我们可以在宿主主机里面配置

下面是一个例子，供参考

在宿主主机里面执行：`crontab -e`,里面写入下面的内容

```
* * * * * cd /www/docker && /usr/local/bin/docker-compose  exec -T golang /www/golang/fec-go-shell >> /www/docker.log 2>&1
```

内容解读：

`* * * * *`:这个是定时的周期部分

`cd /www/docker`：这个是你的docker文件路径，譬如fecmall是：https://github.com/fecshop/yii2_fecshop_docker
，进行的安装，你需要改成你的 `yii2_fecshop_docker`所在的目录。

`/usr/local/bin/docker-compose`:宿主主机的`docker-compose`的对应的绝对路径

`docker-compose  exec -T golang /www/golang/fec-go-shell`:
这个命令就是在宿主主机中，执行golang这个docker容器中的脚本`/www/golang/fec-go-shell`,
如果您要执行`php`容器的某个脚本，可以将`golang`改成`php`，然后将你的脚本替换
掉`/www/golang/fec-go-shell`，就可以了

`>> /www/docker.log 2>&1`: cron执行的结果，写入到这个log文件中，您需要创建这个文件，
并设置可写，如果您不想写入log文件，则将其改成 `/dev/null` 即可


最后参数 `-T`必须加上，不然会报错：

```
Traceback (most recent call last):
  File "<string>", line 3, in <module>
  File "compose/cli/main.py", line 57, in main
  File "compose/cli/main.py", line 108, in perform_command
  File "compose/cli/main.py", line 353, in exec_command
  File ".tox/py27/lib/python2.7/site-packages/dockerpty/pty.py", line 338, in start
  File ".tox/py27/lib/python2.7/site-packages/dockerpty/io.py", line 32, in set_blocking
ValueError: file descriptor cannot be a negative integer (-1)
docker-compose returned -1
```


资料：https://github.com/docker/compose/issues/3352

OK，上面将原理已经写清楚，您可以按照这个操作即可。





















