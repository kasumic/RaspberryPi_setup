# RaspberryPi Setup(Master)
## Server Informations
- IP Address: 192.168.10.1/24
- Enabled Services:
  * Internet Gateway
  * NTP Server
  * DHCP Server
  * Syslog Server
  
## Setup
---
### ネットワーク設定
`sudo vi /etc/dhcpcd.conf`
```
interface eth0
static ip_address=192.168.10.1/24
static domain_name_servers=8.8.8.8
```

---
### ホスト名の変更  
`sudo hostnamectl set-hostname ncg`

---
### レポジトリソースの変更  
`sudo vi /etc/apt/sources.list`

設定前
```bash:設定前
deb http://raspbian.raspberrypi.org/raspbian/ stretch main contrib non-free rpi
# Uncomment line below then 'apt-get update' to enable 'apt-get source'
#deb-src http://raspbian.raspberrypi.org/raspbian/ stretch main contrib non-free rpi
```

設定後
```bash:設定後
deb http://ftp.jaist.ac.jp/raspbian/ stretch main contrib non-free rpi
deb http://ftp.tsukuba.wide.ad.jp/Linux/raspbian/raspbian/ stretch main contrib non-free rpi
#deb http://raspbian.raspberrypi.org/raspbian/ stretch main contrib non-free rpi
# Uncomment line below then 'apt-get update' to enable 'apt-get source'
#deb-src http://raspbian.raspberrypi.org/raspbian/ stretch main contrib non-free rpi
```

ソース更新  
`sudo apt update`

---
### パッケージインストール  
`sudo apt install vim ntp`

---
### NTPサーバ構築  
`sudo vim /etc/ntp.conf`

設定前
```bash:設定前
pool 0.debian.pool.ntp.org iburst
pool 1.debian.pool.ntp.org iburst
pool 2.debian.pool.ntp.org iburst
pool 3.debian.pool.ntp.org iburst
```

設定後
```bash:設定後
#pool 0.debian.pool.ntp.org iburst
#pool 1.debian.pool.ntp.org iburst
#pool 2.debian.pool.ntp.org iburst
#pool 3.debian.pool.ntp.org iburst
pool ntp.nict.jp iburst
```

NTP同期受付設定
```bash:設定後
restrict 192.168.10.0 mask 255.255.255.0
```

サービス再起動  
`sudo systemctl restart ntp.service`

---
### syslogサーバ構築  
`sudo vim /etc/rsyslog.conf`

設定前
```bash:設定前
# provides UDP syslog reception
#module(load="imudp")
#input(type="imudp" port="514")
```

設定後
```bash:設定後
# provides UDP syslog reception
module(load="imudp")
input(type="imudp" port="514")
```

サービス再起動  
`sudo systemctl restart rsyslog.service`

---
### NAT Router  
net.ipv4.ip_forward  
`sudo iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE`
