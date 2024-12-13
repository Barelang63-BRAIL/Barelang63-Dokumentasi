# OPENCV DENGAN CUDA DAN CUDNN
## A. Install OpenCV dari Source dengan Aktivasi Cuda

Sebelum melakukan instalasi, pastikan CUDA dan CUDNN telah terinstal, lalu jika mau anda dapat menghapus Opencv bawaan yang terinstall pada sistem anda dengan command ini.
```
sudo rm -r /usr/include/opencv4/opencv2
```
berikut langkah-langkah mem-build Opencv dari source dengan aktivasi Cuda:

### 1. install dependencies yang diperlukan.
```{ .sh .copy }
sudo apt-get update
sudo apt-get install -y libgtk2.0-dev pkg-config build-essential cmake git \
    libatlas-base-dev gfortran python3-dev \
    libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev \
    libavcodec-dev libavformat-dev libswscale-dev
```

### 2. Clone repositori opencv dan opencv_contrib:
```{ .sh .copy }
git clone https://github.com/opencv/opencv.git
git clone https://github.com/opencv/opencv_contrib.git
```

### 3. Buat folder build pada folder opencv yang telah di clone.
```{ .sh .copy }
cd opencv
mkdir build
cd build
```

### 4. Build opencv dalam folder build yang telah dibuat, 
sebelum melakukan build periksa CUDA_ARCH_BIN yang terdapat pada sistem anda, dengan command:
```{ .sh .copy }
nvidia-smi --query-gpu=compute_cap --format=csv
```

masukan nilai dari CUDA_ARCH_BIN, berdasarkan output dari command line diatas. Build opencv dengan aktivasi Cuda dengan command dibawah ini: 

```{ .sh .copy }
cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D WITH_CUDA=ON \
-D WITH_CUDNN=ON \
-D OPENCV_DNN_CUDA=ON \
-D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules \
-D INSTALL_PYTHON_EXAMPLES=OFF \
-D INSTALL_C_EXAMPLES=OFF \
-D WITH_GTK=ON \
-D WITH_QT=OFF \
-D BUILD_EXAMPLES=ON \
-D CUDA_ARCH_BIN=8.6 \
-D WITH_FFMPEG=ON \
..
```

### 5. Jika proses build telah selesai install opencv.
```{ .sh .copy }
make -j$(nproc)
sudo make install
sudo ldconfig
```


## B. Membuat File opencv4.pc untuk OpenCV
File opencv4.pc berguna sebagai file konfigurasi yang digunakan oleh sistem build (seperti pkg-config) untuk menemukan informasi tentang pustaka OpenCV yang terinstal, sehingga memudahkan proses kompilasi dan linking proyek yang menggunakan OpenCV. Berikut langkah-langkahnya:

### 1. Buat File opencv4.pc
Buat file dengan nama opencv4.pc di direktori /usr/local/lib/pkgconfig/ atau /usr/lib/pkgconfig/. Gunakan editor teks seperti nano untuk membuat file ini:
```{ .sh .copy }
sudo mkdir -p /usr/local/lib/pkgconfig/
sudo nano /usr/local/lib/pkgconfig/opencv4.pc
```

### 2.  Isi File opencv4.pc
Isi file opencv4.pc seperti berikut, sesuaikan path pustaka (libdir) dan header (includedir) jika diperlukan dan isi versi opencv berdasarkan versi yang telah dinstall:
```{ .sh .copy }
prefix=/usr/local
exec_prefix=${prefix}
libdir=${exec_prefix}/lib
includedir=${prefix}/include/opencv4

Name: OpenCV
Description: Open Source Computer Vision Library
Version: 4.10.0
Libs: -L${libdir} -lopencv_core -lopencv_imgproc -lopencv_highgui -lopencv_imgcodecs -lopencv_videoio
Cflags: -I${includedir}

```
- prefix: Lokasi instalasi OpenCV di sistem (biasanya /usr/local).              
- libdir: Path ke direktori pustaka OpenCV (/usr/local/lib).                
- includedir: Path ke header OpenCV (/usr/local/include/opencv4).           
- Libs: Daftar pustaka yang ingin digunakan.            
- Cflags: Path ke header file yang diperlukan untuk kompilasi kode.         

### 3. Set Variabel PKG_CONFIG_PATH
Tambahkan direktori tempat file opencv4.pc berada ke variabel PKG_CONFIG_PATH, sehingga pkg-config dapat mendeteksinya:
```{ .sh .copy }
export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig/
```

Agar perubahan ini bersifat permanen, tambahkan perintah di atas ke dalam file .bashrc:
```{ .sh .copy }
echo 'export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig/' >> ~/.bashrc
source ~/.bashrc
```

### 4. Cek Versi dengan pkg-config
Setelah file opencv4.pc selesai dibuat, cek apakah OpenCV sudah terdeteksi oleh pkg-config dengan perintah berikut:
```{ .sh .copy }
pkg-config --modversion opencv4
```
Jika berhasil, perintah di atas akan menampilkan versi OpenCV, yaitu 4.10.0.