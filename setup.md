<dl>
  <dt>2022/6/18時点<dt>

  <dt>環境<dt>
  <dd>2017年 MacBook Pro
    
  macOS Monterey Version12.4<dd>
<dl>
  
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

```
interface eth0
interface wlan0

ssid [ネットワークのSSID]

static ip_address=[静的IP Address]
static routers=[ルータのIP Address]
static domain_name_servers=[DNSのIP Address]
```

```
cat /etc/dhcpcd.conf
```
で編集されたことを確認

# Raspberry Piに公開鍵を転送する
```
cd ~/.ssh
ssh-keygen -t [鍵のアルゴリズム]
```
で鍵のペアを生成(-tはed25519を推奨)

Enter file in which to save the key (/Users/[ユーザ名]/.ssh/id_[鍵のアルゴリズム]):

と表示されるので生成したい鍵の名前を入力、入力せずEnterするとそのままの名前になる
  
鍵のパスフレーズを入力、必要なければそのままEnter

鍵が
>Your identification has been saved in /Users/ユーザ名/.ssh/[鍵名]
>
>Your public key has been saved in /Users/[ユーザ名]/.ssh/[鍵名].pub
の場所に生成されるので
```
ls ~/.ssh | grep [鍵名]*
```
で鍵が生成されたことを確認
