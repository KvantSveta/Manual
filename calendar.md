# Calendar

**set monday first weekday**

1)
```bash
gksu gedit /etc/default/locale

LANG="en_US.UTF-8"
LC_TIME="en_GB.UTF-8"
LC_PAPER="en_GB.UTF-8"
LC_MEASUREMENT="en_GB.UTF-8"

LC_TIME="en_GB.UTF-8"
```

2)
```bash
gksudo gedit /usr/share/i18n/locales/en_US
first_weekday 2
sudo locale-gen
```
