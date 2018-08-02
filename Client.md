# RaspberryPi Setup(Client)
## Server Informations
- IP Address: 192.168.10.2/24
- Enabled Services:
  * NTP Client
  * Syslog Client
  
## Setup
---
### ホスト名の変更  
`sudo hostnamectl set-hostname ncgX`

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
