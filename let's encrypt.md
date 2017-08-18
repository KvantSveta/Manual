# Let's encrypt


```bash
systemctl stop nginx

cd letsencrypt

./letsencrypt-auto certonly --standalone -d sakurakumo.ru.net

systemctl start nginx
```