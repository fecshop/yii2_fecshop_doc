Docker用Let's Encrypt部署HTTPS
===========================

参考资料：https://www.jianshu.com/p/5afc6bbeb28c

1.生成证书
```
docker pull quay.io/letsencrypt/letsencrypt:latest
```

```
docker run --rm -p 80:80 -p 443:443 \
    -v /etc/letsencrypt:/etc/letsencrypt \
    quay.io/letsencrypt/letsencrypt auth \
    --standalone -m 2358269014@qq.com --agree-tos \
    -d jedidh.com -d www.jedidh.com -d m.jedidh.com -d img.jedidh.com -d img1.jedidh.com -d img2.jedidh.com -d img3.jedidh.com -d img4.jedidh.com -d img5.jedidh.com
```

不知道为什么上面只能添加一个，只能一个一个的添加，因此依次执行


```
docker run --rm -p 80:80 -p 443:443 \
    -v /etc/letsencrypt:/etc/letsencrypt \
    quay.io/letsencrypt/letsencrypt auth \
    --standalone -m 2358269014@qq.com --agree-tos \
    -d jedidh.com
```


```
docker run --rm -p 80:80 -p 443:443 \
    -v /etc/letsencrypt:/etc/letsencrypt \
    quay.io/letsencrypt/letsencrypt auth \
    --standalone -m 2358269014@qq.com --agree-tos \
    -d www.jedidh.com
```


```
docker run --rm -p 80:80 -p 443:443 \
    -v /etc/letsencrypt:/etc/letsencrypt \
    quay.io/letsencrypt/letsencrypt auth \
    --standalone -m 2358269014@qq.com --agree-tos \
    -d m.jedidh.com
```


```
docker run --rm -p 80:80 -p 443:443 \
    -v /etc/letsencrypt:/etc/letsencrypt \
    quay.io/letsencrypt/letsencrypt auth \
    --standalone -m 2358269014@qq.com --agree-tos \
    -d img.jedidh.com
```


```
docker run --rm -p 80:80 -p 443:443 \
    -v /etc/letsencrypt:/etc/letsencrypt \
    quay.io/letsencrypt/letsencrypt auth \
    --standalone -m 2358269014@qq.com --agree-tos \
    -d img2.jedidh.com
```



```
docker run --rm -p 80:80 -p 443:443 \
    -v /etc/letsencrypt:/etc/letsencrypt \
    quay.io/letsencrypt/letsencrypt auth \
    --standalone -m 2358269014@qq.com --agree-tos \
    -d img3.jedidh.com
```



```
docker run --rm -p 80:80 -p 443:443 \
    -v /etc/letsencrypt:/etc/letsencrypt \
    quay.io/letsencrypt/letsencrypt auth \
    --standalone -m 2358269014@qq.com --agree-tos \
    -d img4.jedidh.com
```


执行完成后，就去生成文件

```
ls /etc/letsencrypt/live/
img2.jedidh.com  img4.jedidh.com  jedidh.com    www.jedidh.com
img3.jedidh.com  img.jedidh.com   m.jedidh.com
```

2.修改yml文件

```
web:
    image: nginx:latest
    ports:
      - "80:80"
      - "443:443"
    restart: always
    volumes:
      - ./app:/www/web
      - ./services/web/nginx/conf:/etc/nginx
      - ./services/web/nginx/logs:/www/web_logs
      - /etc/letsencrypt:/etc/letsencrypt
    networks:
        - code-network
    depends_on:
      - php
```

也就是添加端口443，和映射文件  `- /etc/letsencrypt:/etc/letsencrypt`


3.修改nginx配置文件

现在需要在nginx做配置，配置如下,fecshop docker中 `vim ./services/web/nginx/conf/conf.d/default.conf`

```


server {
    listen     80  ;
    server_name admin.jedidh.com;
    root  /www/web/fecshop/appadmin/web;
    server_tokens off;
    include none.conf;
    index index.php index.html index.htm;
    access_log /www/web_logs/access.log wwwlogs;
    error_log  /www/web_logs/error.log  notice;
    location ~ \.php$ {
        fastcgi_pass   php:9000;
        fastcgi_index  index.php;
        include fcgi.conf;
    }
    location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {
        expires      30d;
    }
    location ~ .*\.(js|css)?$ {
        expires      12h;
    }
}

server {
    listen       80;
    server_name  www.jedidh.com;
    rewrite ^(.*)$ https://$host$1 permanent;
}


server {
    listen       80;
    server_name  jedidh.com;
    rewrite ^(.*)$ https://www.$host$1 permanent;
}

server {
    #listen     80  ;

	listen 443 ssl;
    ssl on;
    ssl_certificate /etc/letsencrypt/live/www.jedidh.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/www.jedidh.com/privkey.pem;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

	server_name www.jedidh.com;
    root  /www/web/fecshop/appfront/web;

	server_tokens off;
    include none.conf;
    index index.php index.html index.htm;
    access_log /www/web_logs/access.log wwwlogs;
    error_log  /www/web_logs/error.log  notice;
    location ~ \.php$ {
        fastcgi_pass   php:9000;
        fastcgi_index  index.php;
        include fcgi.conf;
    }

	location ~ /sitemap.xml
	{
		if ($host  ~ .*appfront.fecshop.es) {
			rewrite ^/sitemap\.xml /sitemap_es.xml last;
		}
	}

	location /fr/ {
        index index.php;
        if (!-e $request_filename){
            rewrite . /fr/index.php last;
        }
	}

    location /es/ {
        index index.php;
        if (!-e $request_filename){
            rewrite . /es/index.php last;
        }
	}

	 location /cn/ {
        index index.php;
        if (!-e $request_filename){
            rewrite . /cn/index.php last;
        }
    }

    location /de/ {
        index index.php;
        if (!-e $request_filename){
            rewrite . /de/index.php last;
        }
    }

    location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {
        expires      30d;
    }

    location ~ .*\.(js|css)?$ {
        expires      12h;
    }
}

server {
    listen       80;
    server_name  m.jedidh.com;
    rewrite ^(.*)$ https://$host$1 permanent;
}

server {
    #listen     80  ;
	listen 443 ssl;
    ssl on;
    ssl_certificate /etc/letsencrypt/live/m.jedidh.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/m.jedidh.com/privkey.pem;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

    server_name m.jedidh.com;
    root  /www/web/fecshop/apphtml5/web;
    server_tokens off;
    include none.conf;
    index index.php index.html index.htm;
    access_log /www/web_logs/access.log wwwlogs;
    error_log  /www/web_logs/error.log  notice;
    location ~ \.php$ {
        fastcgi_pass   php:9000;
        fastcgi_index  index.php;
        include fcgi.conf;
    }

    location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {
        expires      30d;
    }

    location /fr/ {
        index index.php;
        if (!-e $request_filename){
            rewrite . /fr/index.php last;
        }
    }
    location /es/ {
        index index.php;
        if (!-e $request_filename){
            rewrite . /es/index.php last;
        }
    }

    location /cn/ {
        index index.php;
        if (!-e $request_filename){
            rewrite . /cn/index.php last;
        }
    }

    location /de/ {
        index index.php;
        if (!-e $request_filename){
           rewrite . /de/index.php last;
        }
    }

    location ~ .*\.(js|css)?$ {
        expires      12h;
    }
    location /api {
        rewrite /api/([a-z][0-9a-z_]+)/?$ /api.php?type=$1;
    }
}


server {
    listen     80  ;

	listen 443 ssl;
    ssl on;
    ssl_certificate /etc/letsencrypt/live/img.jedidh.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/img.jedidh.com/privkey.pem;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

    server_name img.jedidh.com;
    root  /www/web/fecshop/appimage/common;
    server_tokens off;
    include none.conf;
    index index.php index.html index.htm;
    access_log /www/web_logs/access.log wwwlogs;
    error_log  /www/web_logs/error.log  notice;
	location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {
        expires      30d;
    }
}



server {
    listen     80  ;

	listen 443 ssl;
    ssl on;
    ssl_certificate /etc/letsencrypt/live/img2.jedidh.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/img2.jedidh.com/privkey.pem;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

    server_name img2.jedidh.com;
    root  /www/web/fecshop/appimage/appadmin;
    server_tokens off;
    include none.conf;
    index index.php index.html index.htm;
    access_log /www/web_logs/access.log wwwlogs;
    error_log  /www/web_logs/error.log  notice;
	location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {
        expires      30d;
    }
}

server {
    listen     80  ;

	listen 443 ssl;
    ssl on;
    ssl_certificate /etc/letsencrypt/live/img3.jedidh.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/img3.jedidh.com/privkey.pem;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

    server_name img3.jedidh.com;
    root  /www/web/fecshop/appimage/appfront;
    server_tokens off;
    include none.conf;
    index index.php index.html index.htm;
    access_log /www/web_logs/access.log wwwlogs;
    error_log  /www/web_logs/error.log  notice;
	location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {
        expires      30d;
    }
}


server {
    listen     80  ;

	listen 443 ssl;
    ssl on;
    ssl_certificate /etc/letsencrypt/live/img4.jedidh.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/img4.jedidh.com/privkey.pem;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

    server_name img4.jedidh.com;
    root  /www/web/fecshop/appimage/apphtml5;
    server_tokens off;
    include none.conf;
    index index.php index.html index.htm;
    access_log /www/web_logs/access.log wwwlogs;
    error_log  /www/web_logs/error.log  notice;
	location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {
        expires      30d;
    }
}



```

上面除了做https，还做了http跳转到https

4.重启docker-compose

```
docker-compose restart
```

5.做renew证书，也就是定时更新证书（letsencrypt证书有效期为3个月）

创建文件 renew_letsencrypt.sh 和  renew_letsencrypt.sh.log

```
cd /www/web
touch renew_letsencrypt.sh
chmod 755 renew_letsencrypt.sh
touch renew_letsencrypt.sh.log
chmod 777 renew_letsencrypt.sh.log
```

填写脚本内容，`vim renew_letsencrypt.sh`

```
#!/bin/sh
cd /www/web/yii2_fecshop_docker
/usr/local/bin/docker-compose stop web
/usr/bin/docker run --rm -p 80:80 -p 443:443  -v /etc/letsencrypt:/etc/letsencrypt quay.io/letsencrypt/letsencrypt renew --standalone
/usr/local/bin/docker-compose start web
```

设置cron，`crontab -e`，加入：

```

* * * * *  /bin/bash /www/web/renew_letsencrypt.sh  >> /www/web/renew_letsencrypt.sh.log 2>&1
```

保存即可
，然后等几分钟，查看log文件是否有输出，
如果有如下输出，则说明成功，

```
Stopping yii2fecshopdocker_web_1 ... ^M
^[[1A^[[2K^MStopping yii2fecshopdocker_web_1 ... ^[[32mdone^[[0m^M^[[1BWarning: This Docker image will soon be switching to Alpine Linux.
You can switch now using the certbot/certbot repo on Docker Hub.
Saving debug log to /var/log/letsencrypt/letsencrypt.log

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/img.jedidh.com.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Cert not yet due for renewal

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/jedidh.com.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Cert not yet due for renewal

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/img4.jedidh.com.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Cert not yet due for renewal

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/www.jedidh.com.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Cert not yet due for renewal

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/img3.jedidh.com.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Cert not yet due for renewal

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/m.jedidh.com.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Cert not yet due for renewal

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/img2.jedidh.com.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Cert not yet due for renewal

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

```

现在我们改成一个月更新一次证书

设置cron，`crontab -e`，加入：

```

0 0 1 * *  /bin/bash /www/web/renew_letsencrypt.sh  >> /www/web/renew_letsencrypt.sh.log 2>&1
```

完成
