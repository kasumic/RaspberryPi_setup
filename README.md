# rasberrypi_setup(Master)
## Server Informations
- IP Address: 192.168.10.1/24
- Enabled Services:
  * Internet Gateway
  * NTP Server
  * DHCP Server
  * Syslog Server
  
## Install Commands
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
### NTPサーバの設定  
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
