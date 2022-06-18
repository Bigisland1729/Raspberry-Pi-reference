<dl>
  <dt>2022/6/18時点</dt>
  <dt>環境</dt>
  <dd> 
    
  * 2017年 MacBook Pro
      
  * macOS Monterey Version12.4
      
  * Raspberry Pi 4 Model B
      
  * Raspberry Pi OS 64bit Bullseye</dd>
</dl>

>**Warning**
>
>`sudo raspi-config`の`legacy camera support`を***enable***に設定するとカメラモジュールが動かなくなることに注意

# カメラモジュールのテスト
VNC ViewerでIP Address、ユーザ名、パスワードを入力しRaspberry PiにVNC接続する

VNCのディスプレイ上でTerminalを起動し
```
libcamera-hello
```
を実行、問題がなければカメラの映像が5秒間表示される
