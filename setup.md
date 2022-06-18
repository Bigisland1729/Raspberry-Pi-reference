2022/6/18時点

# OSを入れる
SDカードにRaspberry Pi ImagerでOSを入れる

ホスト名, wifi, sshの設定をすることができる(ステルスSSIDの場合項目にチェックを入れる)

終わったらSDカードをアンマウントする

# SSH接続をする
```
ssh [ユーザ名]@[ホスト名].local
```
でRaspberry PiにSSH接続する

*REMOTE HOST IDENTIFICATION HAS CHANGED*の場合~/.ssh/known_hostsを編集(Macの場合)

# 静的IP Addressを設定する
```
nano /etc/dhcpcd.conf
```
か
```
vi /etc/dhcpcd.conf
```
で /etc/dhcpcd.confに以下を追記

interface eth0
interface wlan0

ssid [ネットワークのSSID]

static ip_address=[静的IP Address]
static routers=[ルータのIP Address]
static domain_name_servers=[DNSのIP Address]
