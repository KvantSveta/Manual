# Ufw

```bash
добавление сервисов, которым разрешено
sudo ufw allow 22
#sudo ufw allow ssh
sudo ufw allow 80
#sudo ufw allow http
sudo ufw allow 443
#sudo ufw allow https
sudo ufw allow 1194

расширенное правило с указанием порта
sudo ufw allow in on eth1 to any port 5432

влючение фаервола
sudo ufw enable

отображение правил
sudo ufw status

более подробный вывод
sudo ufw status verbose

включение логирования
sudo ufw logging on

политика по умолчанию: исходящие разрешить, входящие - запретить
sudo ufw default allow outgoing 
sudo ufw default deny incoming

перезагрузка фаервола
sudo ufw reload
```

**On vscale**
```bash
ufw default allow outgoing 
ufw default deny incoming

ufw allow 22/tcp
ufw allow 80
ufw allow 443
ufw allow 1194

ufw logging on

ufw enable

ufw status verbose
```

**On RPi**
```bash
sudo ufw default allow outgoing 
sudo ufw default deny incoming

sudo ufw allow 22/tcp
sudo ufw allow 80
sudo ufw allow 443
sudo ufw allow 1194

sudo ufw logging on

sudo ufw enable

sudo ufw status verbose
```