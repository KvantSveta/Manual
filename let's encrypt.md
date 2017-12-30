# Let's encrypt

**I**
```bash
systemctl stop nginx

cd letsencrypt

./letsencrypt-auto certonly --standalone -d sakurakumo.ru.net

systemctl start nginx
```

**II**
```bash
Close all nginx process via htop

lsof -i :443

cd letsencrypt

/letsencrypt-auto certonly --email NikeLambert@gmail.com

2
```