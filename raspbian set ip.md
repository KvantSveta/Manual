# Raspbian

**set static ip address**
```bash
sudo nano /etc/dhcpcd.conf

interface eth0
static ip_address=192.168.1.111/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.1
```
