# Robot Installation

Instalasi Library yang Diperlukan dari GitHub:

- [ArduinoJSON](https://github.com/bblanchon/ArduinoJson.git)
- [CppLinuxSerial](https://github.com/gbmhunter/CppLinuxSerial.git)
- [LibInterpolate](https://github.com/CD3/libInterpolate.git)
- [BehavioTreeCpp](https://github.com/BehaviorTree/BehaviorTree.CPP.git) versi 4.1
- [IcecreamCPP] (Copy from Barelang63 hard drive)


## Cara Menginstal Library dari GitHub
untuk clone repository, gunakan perintah berikut:
```
git clone https://github.com/bblanchon/ArduinoJson.git
```
To build and install the cloned library, run:
```
cd <library_you_cloned>
mkdir build
cmake ..
sudo make install
```
Ulangi proses ini untuk setiap library yang di-kloning.

## Instalasi Library untuk Robot:
Jalankan perintah berikut untuk menginstal library yang diperlukan:
```
sudo apt-get install \
    net-tools \
    git \
    libboost-all-dev \
    libeigen3-dev \
    catch2 \
    nuitka \
    xsdcxx \
    liblmdb-dev \
    liblz4-dev \
    libxerces-c-dev \
    libmsgpack-dev \
    libzstd-dev \
    python3-pip \
    libzmq3-dev \
    libsqlite3-dev \
    libgtest-dev \
    libcgal-dev \
    libsisl-dev \
    libyaml-cpp-dev \
    libtcod-dev \
    libncurses5-dev \
    libncursesw5-dev
```
