# Install OpenCV dari Source dengan Aktivasi Cuda

Sebelum melakukan instalasi, pastikan CUDA dan CUDNN telah terinstal, lalu jika mau anda dapat menghapus Opencv bawaan yang terinstall pada sistem anda dengan command ini.
```
sudo rm -r /usr/include/opencv4/opencv2
```
berikut langkah-langkah mem-build Opencv dari source dengan aktivasi Cuda:

### A. install deoendencies yang diperlukan.
```
sudo apt-get update
sudo apt-get install -y libgtk2.0-dev pkg-config build-essential cmake git \
    libatlas-base-dev gfortran python3-dev \
    libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev \
    libavcodec-dev libavformat-dev libswscale-dev
```

### B. Clone repositori opencv dan opencv_contrib:
```
git clone https://github.com/opencv/opencv.git
git clone https://github.com/opencv/opencv_contrib.git
```

### C. Buat folder build pada folder opencv yang telah di clone.
```
cd opencv
mkdir build
cd build
```

### D. Build opencv dalam folder build yang telah dibuat, 
sebelum melakukan build periksa CUDA_ARCH_BIN yang terdapat pada sistem anda, dengan command:
```
nvidia-smi --query-gpu=compute_cap --format=csv
```

masukan nilai dari CUDA_ARCH_BIN, berdasarkan output dari command line diatas. Build opencv dengan aktivasi Cuda dengan command dibawah ini: 

```
cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr \
-D WITH_CUDA=ON \
-D WITH_CUDNN=ON \
-D OPENCV_DNN_CUDA=ON \
-D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules \
-D INSTALL_PYTHON_EXAMPLES=OFF \
-D INSTALL_C_EXAMPLES=OFF \
-D WITH_GTK=OFF \
-D WITH_QT=OFF \
-D BUILD_EXAMPLES=ON \
-D CUDA_ARCH_BIN=8.6 \
-D WITH_FFMPEG=ON \
..
```

### E. Jika proses build telah selesai install opencv.
```
make -j$(nproc)
sudo make install
sudo ldconfig
```
