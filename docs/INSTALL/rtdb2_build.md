# Build RTDB2

## Apa itu Rtdb2 ?
Rtdb2 adalah package komunikasi antar robot dari MSL robocup

Library ini berasal dari: 
[rtdb2](https://github.com/RoboCup-MSL/rtdb2)

## How to build
Sebelum memulai build lakukan proses ini terlebih dahulu: [install robot](install_all.md)

```
- copy folder rtdb2 in hardisk barelang63
- cd rtdb2
- mkdir build
- cd build
- cmake -DCMAKE_BUILD_TYPE=Release ..
- sudo make install
```

## Install rtdb2 monitoring tools
```
pip3 install lmdb msgpack-python
```