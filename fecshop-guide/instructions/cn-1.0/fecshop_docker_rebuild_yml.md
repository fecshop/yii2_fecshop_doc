Docker 修改yml文件后，重新创建docker container
=========================

当docker-compose up -d后，如果修改了yml文件，譬如将某个service的port更改后，想要重新创建docker container，那么可以通过下面的命令

```
docker-compose up -d --force-recreate
```


执行log：

```
docker-compose up -d --force-recreate
Recreating mypg_pgadmin4_1 ... 
Recreating mypg_pgsql_1 ... 
Recreating mypg_pgsql2_1 ... 
Recreating mypg_pgadmin4_1 ... done

```






