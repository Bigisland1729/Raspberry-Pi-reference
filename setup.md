<dl>
  <dt>2022/6/18時点</dt>

  <dt>環境</dt>
  <dd>
	  
  * 2017年 MacBook Pro
    
  * macOS Monterey Version 12.4
		
  * Raspberry Pi Imager v1.7.2
	  
  * Raspberry Pi 4 Model B
	  
  * Raspberry Pi OS 64bit Bullseye</dd>
</dl>
  
# OSを入れる
SDカードにRaspberry Pi ImagerでOSを入れる

ホスト名、ユーザ名、ユーザのパスワード、Wifi、SSHの設定をすることができる(ステルスSSIDの場合項目にチェックを入れる)
  
設定しなければホスト名はraspberrypi.local

終わったらSDカードをアンマウントする
<img src=https://github.com/Bigisland1729/Raspberry-Pi-reference/blob/main/screen-shot-rpi-imager-v1.7.2.png width=500>

# SSH接続をする
```bash
ssh [ユーザ名]@[ホスト名]
```
でRaspberry PiにSSH接続する

*REMOTE HOST IDENTIFICATION HAS CHANGED*の場合 ~/.ssh/known_hostsを編集

# 静的IP Addressを設定する
`nano /etc/dhcpcd.conf`か`vi /etc/dhcpcd.conf`で /etc/dhcpcd.confに以下を追記

```
interface eth0
interface wlan0

ssid [ネットワークのSSID]

static ip_address=[静的IP Address]
static routers=[ルータのIP Address]
static domain_name_servers=[DNSのIP Address]
```

`cat /etc/dhcpcd.conf`で編集されたことを確認

# Raspberry Piに公開鍵を登録する
```bash
cd ~/.ssh
ssh-keygen -t [鍵のアルゴリズム]
```
で鍵のペアを生成(-tはed25519を推奨)

>Enter file in which to save the key (/Users/[ユーザ名]/.ssh/id_[鍵のアルゴリズム]):

と表示されるので生成したい鍵の名前を入力、入力せずEnterするとそのままの名前になる
  
鍵のパスフレーズを入力、必要なければそのままEnter

鍵が
>Your identification has been saved in /Users/ユーザ名/.ssh/[鍵名]
>
>Your public key has been saved in /Users/[ユーザ名]/.ssh/[鍵名].pub

の場所に生成されるので
`ls ~/.ssh | grep [鍵名]*`で鍵が生成されたことを確認

新たにターミナルのウィンドウを立ち上げ、
```bash
ssh-copy-id -i ~/.ssh/[鍵名].pub [ユーザ名]@[ホスト名]
```
でRaspberry Piに鍵を転送、求められるパスワードはRaspberry Piのユーザのパスワードを入力
  
```bash
ssh -i ~/.ssh/[鍵名] [ユーザ名]@[ホスト名]
```
で鍵でログインできることを確認
	
# SSHの鍵の簡略化及びポート番号とkeepaliveの設定
`nano ~/.ssh/config`か`vi ~/.ssh/config`で ~/.ssh/configに以下を追記

```bash
Host [設定名]
  HostName [ホスト名]
  User [Raspberry Piのユーザ名]
  IdentityFile /Users/[ユーザ名]/.ssh/[鍵名]
  Port [ポート番号]
  TCPKeepAlive yes
```

そして
```bash
ssh [設定名]
```
でSSH接続できることを確認

# SSHの設定
`sudo nano /etc/ssh/sshd_config`か`sudo vi /etc/ssh/sshd_config`で /etc/ssh/ssd_configの以下の部分をコメントアウトを外して編集
```
Port [ポート番号]
PermitRootLogin no
PasswordAuthentication no 
```
<dl>
  説明
	<dt>Port [ポート番号]</dt>
	<dd>SSH接続に使用するポート番号</dd>
  <dt>PermitRootLogin no</dt>
	<dd>rootログインを禁止</dd>
  <dt>PasswordAuthentication no</dt>
	<dd>パスワード認証の無効化</dd>
</dl>
	
```bash
sudo /etc/init.d/ssh restart
```
でSSHを再起動
```bash
ssh [ユーザ名]@[ホスト名]
```
で*Permission denied*となることを確認
```bash
ssh [設定名]
```
のみで接続可能となる

# VNCの設定
```bash
sudo raspi-config
```
で `3 Interface Options`からVNCを有効化しRaspberry Piを再起動する

VNC ViewerでIP Address、ユーザ名、パスワードを入力し、VNC接続をする
