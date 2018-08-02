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

---
### Commands
`man [command]`

`which [command]`

`which ls > which.log`  
`which shutdown >> which.log`

`echo {1..1000}`

---
### NTPの設定
`sudo vi /etc/ntp.conf`

```bash:設定後
server 192.168.10.1
```

---
### rsysylog送信設定
`sudo vi /etc/rsyslog.conf`

```bash:設定後
*.* @192.168.10.l:514
```

### syslog確認
`logger test-message`


---
### ディスク操作
- パーティション確認  
`sudo parted -l`

- パーティショニング  
`sudo perted /dev/sdb`

`mklabel gpt`

`mkpart primary 0 100%`

`set 1 lvm on`

`quit`
