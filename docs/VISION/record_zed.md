# Capture dan Record Video Menggunakan Zed Camera

Sebelum mengikuti langkah-langkah di bawah ini, clone repositori ini terlebih dahulu:
```
git clone https://github.com/dsyahput/Capture-and-Record-Video-using-Zed-Camera.git
```

## A. Prasyarat:

1. Install ZED SDK: Download dan instal ZED SDK dari situs web resmi Stereolabs [ZED SDK](https://www.stereolabs.com/docs/installation/linux).

2. Install OpenCV: Pastikan OpenCV sudah terinstall. Atau anda dapat mengikuti tutorial menginstal opencv dengan aktivasi cuda [DISINI](INSTALL/install_opencv.md).

## B. Build Program
Buat direktori build: Buka terminal dan navigasikan ke direktori yang berisi program dan file CMakeLists.txt, lalu buat direktori build:

``` bash
cd Capture-and-Record-Video-using-Zed-Camera
mkdir build
cd build
cmake ..
make
```
## C. Menjalankan Program
Setelah mem-build program, Anda dapat menjalankannya dengan perintah berikut:

```bash
./zed_camera_record
```

Tekan tombol 's' untuk mulai merekam video.         
Tekan tombol 'x' untuk menghentikan rekaman.    
Tekan tombol 'Esc' untuk keluar dari program.   

### Video akan disimpan di folder 'videos'.
