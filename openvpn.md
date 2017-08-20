# Настройка OpenVPN

**На vscale сервере**
```bash
1) apt-get install openvpn easy-rsa

2) make-cadir ~/openvpn-ca

3) cd ~/openvpn-ca

4) nano vars
export KEY_COUNTRY="~~~"
export KEY_PROVINCE="~~~"
export KEY_CITY="~~~"
export KEY_ORG="~~~"
export KEY_EMAIL="~~~"
export KEY_OU="~~~"

export KEY_NAME="server"

5) source vars

6) ./clean-all

7) ./build-ca

8) ./build-key-server server

9) ./build-dh

10) openvpn --genkey --secret keys/ta.key

11) ./build-key client

12) cd ~/openvpn-ca/keys

13) cp ca.crt ca.key server.crt server.key ta.key dh2048.pem /etc/openvpn

14) gunzip -c /usr/share/doc/openvpn/examples/sample-config-files/server.conf.gz | tee /etc/openvpn/server.conf

15) nano /etc/openvpn/server.conf
tls-auth ta.key 0 # This file is secret
key-direction 0

cipher AES-256-CBC
auth SHA256

user nobody
group nogroup
```
~~push "redirect-gateway def1 bypass-dhcp"~~

```bash
push "dhcp-option DNS 208.67.222.222"
push "dhcp-option DNS 208.67.220.220"

16) nano /etc/sysctl.conf
net.ipv4.ip_forward=1

17) sysctl -p

18) systemctl start openvpn@server

19) systemctl enable openvpn@server

20) mkdir -p ~/client-configs/files

21) chmod 700 ~/client-configs/files

22) cp /usr/share/doc/openvpn/examples/sample-config-files/client.conf ~/client-configs/base.conf

23) nano ~/client-configs/base.conf
remote 123.456.789.0

user nobody
group nogroup

#ca ca.crt
#cert client.crt
#key client.key

cipher AES-256-CBC
auth SHA256

key-direction 1

24) nano ~/client-configs/make_config.sh
#!/bin/bash

# First argument: Client identifier

KEY_DIR=~/openvpn-ca/keys
OUTPUT_DIR=~/client-configs/files
BASE_CONFIG=~/client-configs/base.conf

cat ${BASE_CONFIG} \
    <(echo -e '<ca>') \
    ${KEY_DIR}/ca.crt \
    <(echo -e '</ca>\n<cert>') \
    ${KEY_DIR}/${1}.crt \
    <(echo -e '</cert>\n<key>') \
    ${KEY_DIR}/${1}.key \
    <(echo -e '</key>\n<tls-auth>') \
    ${KEY_DIR}/ta.key \
    <(echo -e '</tls-auth>') \
    > ${OUTPUT_DIR}/${1}.ovpn

25) chmod 700 ~/client-configs/make_config.sh

26) cd ~/client-configs

27) ./make_config.sh client

28) scp -P 222 root@123.456.789.0:/root/client-configs/files/client.ovpn ~/

29) systemctl start openvpn@server
```

**На клиенте**
```bash
1) sudo apt-get install openvpn

2) nano client.ovpn
script-security 2
up /etc/openvpn/update-resolv-conf
down /etc/openvpn/update-resolv-conf

3) sudo openvpn --config client.ovpn
```
