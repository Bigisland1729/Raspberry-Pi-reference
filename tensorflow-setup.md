<dl>
  <dt>2022/6/18時点</dt>
  <dt>環境</dt>
  <dd>
    
  * Python 3.9.2
    
  * Pythonライブラリ: **[初期状態](https://github.com/Bigisland1729/Raspberry-Pi-reference/blob/main/pylib-versions.txt)**
  
  * Raspberry Pi 4 Model B
      
  * Raspberry Pi OS 64bit Bullseye</dd>
</dl>

# Tensorflow Lite及びその周辺をインストール(ver 2.9.0)
Tensorflow Liteのインストール
```
sudo apt install swig libjpeg-dev zlib1g-dev python3-dev unzip wget python3-pip curl git cmake make
sudo pip3 install numpy==1.22.3
curl -OL https://github.com/PINTO0309/TensorflowLite-bin/releases/download/v2.9.0/tflite_runtime-2.9.0-cp39-none-linux_aarch64.whl
sudo pip3 install --upgrade tflite_runtime-2.9.0-cp39-none-linux_aarch64.whl
```

インストールされたことの確認
```
python -c 'import tflite_runtime as tflite;print(tflite.__version__)'
```

**参照**

https://github.com/PINTO0309/TensorflowLite-bin

# Tensorflow及びその周辺をインストール(ver 2.9.0)
Tensorflowのインストール
```
sudo apt-get install -y libhdf5-dev libc-ares-dev libeigen3-dev gcc gfortran libgfortran5 libatlas3-base libatlas-base-dev libopenblas-dev libopenblas-base libblas-dev liblapack-dev cython3 libatlas-base-dev openmpi-bin libopenmpi-dev python3-dev python-is-python3
sudo pip3 install pip --upgrade
sudo pip3 install keras_applications==1.0.8 --no-deps
sudo pip3 install keras_preprocessing==1.1.2 --no-deps
pip3 install -U --user six wheel mock # local
curl -L https://github.com/PINTO0309/Tensorflow-bin/releases/download/v2.9.0/tensorflow-2.9.0-cp39-none-linux_aarch64.whl -o tensorflow-2.9.0-cp39-none-linux_aarch64.whl
sudo pip3 uninstall tensorflow
sudo -H pip3 install tensorflow-2.9.0-cp39-none-linux_aarch64.whl
```

インストールされたことの確認
```
python -c 'import tensorflow as tf;print(tf.__version__)'
```

**参照**

https://github.com/PINTO0309/Tensorflow-bin
