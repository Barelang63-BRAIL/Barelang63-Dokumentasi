# Build RTDB2

## What is Rtdb2 ?
Rtdb2 is Communication based on udp ussualy use in competition Middle Size League (MSL)

This Library is based on: https://github.com/RoboCup-MSL/rtdb2

## Requirements

This project uses some 3rd-party libraries:
- LZ4
- zstd
- LMDB
- Msgpack
- Xerces-c
- xsdcxx


## How to build
Before build this package please do instruction from this: [install robot](install_all.md)

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