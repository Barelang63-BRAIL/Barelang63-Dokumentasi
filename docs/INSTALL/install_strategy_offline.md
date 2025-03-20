# Build Program Strategy Offline

# Sebelum melakukan build lakukan ini terlebih dahulu:
-  [Install Robot](install_all.md)
-  [Build Rtdb2](rtdb2_build.md)
-  [Install Cuda](cuda_and_cudnn.md)
-  [Install ZED SDK](zed_sdk_install.md)
-  [Install OpenCV](install_opencv.md)
-  [Build Basestation](install_Basestation.md) (Optional)
-  [Make robot_launch and robot_build](../RUNNING/builder_and_launcher.md) (Optional)

## Requirements
Pergi terlebih dahulu ke folder maen_boss,
Sebelum build program strategy perlu build folder dibawah ini terlebih dahulu (Pastikan sesuai urutan):
-  def
-  grid
-  control
-  potential
-  control
-  offline
-  joy (Optional)
-  heartbeat
-  amcl
-  omni
-  zed_ws
-  NucleoServer

## How to build
```{ .sh .copy }
    robot_build folder/ 
```

## Example to Build 
```{ .sh .copy }
    robot_build def/
```

## Jika Error build seperti ini
```
usage: robot_build [-h] package_name proc
robot_build: error: the following arguments are required: proc
```
Running ini:
```{ .sh .copy }
    robot_build def/ 8
```

## Install rtdb2 monitoring tools
```{ .sh .copy }
pip3 install lmdb msgpack-python
```