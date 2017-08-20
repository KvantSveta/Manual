# Nginx

#### New install

**Dependencies**
```bash
sudo apt-get install libpcre++-dev 
sudo apt-get install zlib1g-dev
```

**Install**
```bash
./configure
make
sudo make install
```

**/usr/local/nginx/conf/nginx.conf**
```bash
server {
	#listen       8000;
	#listen       192.168.1.102:8080;
	listen       123.456.789.0:9999;
	#server_name  somename  alias  another.alias;
	allow all;
	#deny all;

	location / {
	    #proxy_pass http://192.168.1.10:5000;
	    proxy_pass http://10.8.0.6:5000;
	    proxy_store on;
	    proxy_set_header Host $host;
	    proxy_set_header X-Real-IP $remote_addr;
	    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	}
}
```

**Test conf file**
```bash
gixy /usr/local/nginx/conf/nginx.conf
```

**start**
```bash
/usr/local/nginx/sbin/nginx
```

**stop | quit | reopen | reload**
```bash
/usr/local/nginx/sbin/nginx -s [ stop | quit | reopen | reload ]
```

#### Install via apt-get

```bash
apt-get install nginx

nano /etc/nginx/sites-available/default
```

~~~
server {
    listen       80;
   server_name  sakurakumo.ru.net;

    if ($scheme = http) {
        return 301 https://$server_name$request_uri;
    }
}

server {
    listen       443 ssl;
    server_name  sakurakumo.ru.net;
    allow all;

    ssl on;
    ssl_certificate /etc/letsencrypt/live/sakurakumo.ru.net/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/sakurakumo.ru.net/privkey.pem;
    ssl_session_timeout 5m;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers "HIGH:!aNULL:!MD5 or HIGH:!aNULL:!MD5:!3DES";
    ssl_prefer_server_ciphers on;

    location / {
        proxy_pass http://10.8.0.6:80;
        proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
        proxy_redirect off;
        proxy_buffering off;
        proxy_set_header Host sakurakumo.ru.net;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        auth_basic "Restricted";
        auth_basic_user_file /etc/nginx/.htpasswd;
    }
}
~~~

#### Basic HTTP authorization

```bash
apt-get install apache2-utils

htpasswd -c /etc/nginx/.htpasswd web

New password:
Re-type new password:
Adding password for user web
```

**restart nginx**
```bash
systemctl start nginx.service 
```
