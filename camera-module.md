<dl>
  <dt>2022/6/18時点</dt>
  <dt>環境</dt>
  <dd> 
    
  * 2017年 MacBook Pro
      
  * macOS Monterey Version 12.4
      
  * Raspberry Pi 4 Model B
      
  * Raspberry Pi OS 64bit Bullseye</dd>
</dl>

>**Warning**
>
>`sudo raspi-config`の`legacy camera support`を***enable***に設定するとカメラモジュールが動かなくなることに注意

# カメラモジュールのテスト
VNC ViewerでRaspberry PiにVNC接続する

VNCのディスプレイ上でTerminalを起動し
```
libcamera-hello
```
を実行、問題がなければカメラの映像が5秒間表示される

# Picamera2のインストール
Picamera2のインストール
```
sudo apt install -y libboost-dev
sudo apt install -y libgnutls28-dev openssl libtiff5-dev
sudo apt install -y libfmt-dev libdrm-dev
sudo apt install -y python3-pyqt5
sudo apt install -y meson
sudo pip3 install pyyaml ply
sudo pip3 install pyopengl

sudo apt-get --no-install-recommends install cmake libyaml-dev

sudo apt install libcap-dev
sudo pip install python-prctl
sudo pip install simplejpeg
sudo pip install piexif
sudo pip install pidng

cd
git clone --branch picamera2 https://github.com/raspberrypi/libcamera.git
cd libcamera
meson build -Dpycamera=enabled
ninja -C build -j 2
sudo ninja -C build install
cd
git clone https://github.com/tomba/kmsxx.git
cd kmsxx
git submodule update --init
meson build
ninja -C build -j 2
cd
git clone https://github.com/RaspberryPiFoundation/python-v4l2.git
git clone https://github.com/raspberrypi/picamera2.git
```
そして
`nano ~/.bashrc`か`vi ~/.bashrc`で~/.bashrcに以下を追記
```
export PYTHONPATH=/home/[ユーザ名]/picamera2:/home/[ユーザ名]/libcamera/build/src/py:/home/[ユーザ名]/kmsxx/build/py:/home/[ユーザ名]/python-v4l2
```

# Picamera2の動作確認

`touch picam2_test.py`で ~/picam2_test.pyを作成し、`nano picam2_test.py`か`vi picam2_test.py`で以下を記入

```python
from picamera2.picamera2 import *
import time

picam2 = Picamera2()
picam2.start_preview(Preview.QTGL)
preview_config = picam2.preview_configuration()
capture_config = picam2.still_configuration()
picam2.configure(preview_config)

picam2.start()
time.sleep(5)
picam2.switch_mode_and_capture_file(capture_config, 'test.jpg')
```
VNCのディスプレイ上でTerminalを起動し、以下を実行
```
python picam2_test.py
```
実行すると ~/test.jpgという画像ファイルが生成される

# 参照
https://github.com/raspberrypi/picamera2

https://zenn.dev/karaage0703/articles/96013d71ab764c

https://issueantenna.com/repo/raspberrypi/libcamera/issues/21
