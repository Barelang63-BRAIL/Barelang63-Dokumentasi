# Capture and Record Video using Zed Camera

Sebelum mengikuti langkah-langkah di bawah ini, clone repositori ini terlebih dahulu:
```
git clone https://github.com/dsyahput/Capture-and-Record-Video-using-Zed-Camera.git
```

## A. Prasyarat:

Instal ZED SDK: Unduh dan instal ZED SDK dari situs web resmi Stereolabs ZED SDK.

Instal OpenCV: Pastikan OpenCV sudah terinstal. Jika belum, Anda dapat mengikuti petunjuk instalasi OpenCV sesuai dengan platform yang Anda gunakan.

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
