# Robot Installation

## Command to Download Packages for Regional, Offline, etc.

Install Required Libraries from GitHub:

- [ArduinoJSON](https://github.com/bblanchon/ArduinoJson.git)
- [CppLinuxSerial](https://github.com/gbmhunter/CppLinuxSerial.git)
- [LibInterpolate](https://github.com/CD3/libInterpolate.git)
- [BehavioTreeCpp](https://github.com/BehaviorTree/BehaviorTree.CPP.git) versi 4.1
- [IcecreamCPP] (Copy from Barelang63 hard drive)


## How to Install Libraries from GitHub
To clone the repository, use the following command:
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
Repeat this process for each library you clone.

## Install Libraries for the Robot:
Run the following command to install the necessary libraries:
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
