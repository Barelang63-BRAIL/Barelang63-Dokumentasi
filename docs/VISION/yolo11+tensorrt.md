# **YOLO11 + TensorRT: Optimasi Model YOLO11 dengan TensorRT pada Perangkat NVIDIA GPU**

![-](../images/yolo11+tensorrt/yolo+tensorrt_banner.png)

Penggunaan TensorRT untuk melakukan inferensi model YOLO bertujuan untuk mengoptimalkan proses menjalankan model tersebut. Dengan TensorRT, proses inferensi dapat berjalan lebih cepat dan efisien. TensorRT sendiri merupakan framework yang dirancang khusus oleh NVIDIA untuk mengakselerasi kinerja model deep learning pada perangkat dengan GPU NVIDIA.

> 📌 Untuk proses training custom model YOLO11, Anda dapat merujuk ke dokumentasi berikut: 👉 [YOLO Custom Model](yolo_custom_dataset.md).

> 📌 Untuk proses inferensi model YOLO11 menggunakan TensorRT dengan bahasa pemrograman Python, silakan merujuk ke dokumentasi resmi dari Ultralytics yang informatif dan mudah diikuti: 👉 [Ultralytics - TensorRT Integration](https://docs.ultralytics.com/integrations/tensorrt/).

## 🛠️ Build Repository `TensorRT-YOLO` untuk Inferensi YOLO11 Menggunakan C++

Dalam dokumentasi ini, implementasi inferensi model YOLO11 + TensorRT dilakukan menggunakan bahasa pemrograman C++. Anda dapat menggunakan repository berikut sebagai referensi utama:

👉 [https://github.com/laugh12321/TensorRT-YOLO.git](https://github.com/laugh12321/TensorRT-YOLO.git).

Namun, sebelum melakukan build, Anda perlu terlebih dahulu menginstal TensorRT. Berikut langkah-langkah instalasinya:

### ✅ Langkah Instalasi TensorRT

#### 1. Unduh TensorRT dari situs resmi NVIDIA
👉 [https://developer.nvidia.com/tensorrt/download](https://developer.nvidia.com/tensorrt/download)

Disarankan untuk mengunduh file berformat `.tar` agar proses instalasi lebih sederhana.

#### 2. Ekstrak File TensorRT
Setelah selesai mengunduh, ekstrak file `.tar` TensorRT tersebut. Untuk kemudahan, disarankan mengganti nama folder hasil ekstraksi menjadi lebih sederhana, misalnya `tensorrt`.

Selanjutnya, pindahkan folder tersebut ke direktori `/usr/local` dengan perintah berikut:
```
sudo mv tensorrt /usr/local
```

#### 3. Menyalin File `trtexec` ke `/usr/bin`
Di dalam folder `tensorrt/bin`, terdapat file bernama `trtexec`. File ini sangat penting karena digunakan untuk mengonversi model ke format TensorRT. Agar dapat diakses secara global melalui terminal, Anda disarankan untuk menyalin file ini ke direktori `/usr/bin`:
```
cd /usr/local/tensorrt/bin
sudo cp trtexec /usr/bin
```
#### 4. Menambahkan Path Library TensorRT
Tambahkan path library TensorRT ke dalam file `~/.bashrc` agar dikenali oleh sistem:

```
export LD_LIBRARY_PATH=/usr/local/tensorrt/targets/x86_64-linux-gnu/lib:$LD_LIBRARY_PATH
```

Setelah itu, jalankan:
```
source ~/.bashrc
```

Dengan ini, proses instalasi TensorRT telah selesai.

### ✅ Langkah Build Repository `TensorRT-YOLO`
Sebelum melakukan proses build repository, terdapat beberapa penyesuaian yang perlu dilakukan. Berikut langkah-langkah lengkapnya:

#### 1. Penyesuaian File CMakeLists.txt
Buka file `CMakeLists.txt` yang terdapat di root direktori repository, Pastikan Anda menyesuaikan path TensorRT sesuai dengan lokasi instalasi di sistem Anda.

Contoh visualisasi bagian yang perlu disesuaikan:
![-](../images/yolo11+tensorrt/tensorrt_cmake.png)

#### 2. Menambahkan Path CUDA ke Environment
Sebelum build, tambahkan environment CUDA agar dikenali oleh sistem anda dapat menambahkannya pada file `~/.bashrc`. Sesuaikan path-nya dengan versi CUDA yang terinstal di perangkat Anda:
```
export PATH=/usr/local/cuda-12.6/bin:$PATH
export CUDACXX=/usr/local/cuda-12.6/bin/nvcc
export LD_LIBRARY_PATH=/usr/local/cuda-12.6/lib64:$LD_LIBRARY_PATH
```
> 🔍 Catatan: Versi CUDA (cuda-12.6) dapat berbeda tergantung sistem Anda. Pastikan versi tersebut sesuai dengan yang telah Anda instal.

#### 3. Build Repository
Setelah konfigurasi dilakukan, Anda dapat membangun proyek dengan langkah berikut:
```
mkdir build
cd build
cmake ..
make
```
#### 4. Folder `lib`
Setelah proses build selesai, akan terbentuk folder `lib/` yang berisi beberapa file penting untuk proses inferensi:
```
└── lib/
     ├── libdeploy.so
     │     
     └── plugin/
              └── libcustom_plugins.so       
```

> -`libdeploy.so` adalah library utama yang digunakan untuk melakukan inferensi model YOLO dengan TensorRT.

> -`libcustom_plugins.so` dibutuhkan untuk menconvert model dengan fitur tambahan seperti OBB (Oriented Bounding Box), Pose Estimation, dan Instance Segmentation.

Dengan ini, proses build repository **TensorRT-YOLO** telah selesai dan siap digunakan.

## 🛠️ Build Examples pada Repository `TensorRT-YOLO`
Repository TensorRT-YOLO menyediakan berbagai contoh penggunaan (examples) untuk setiap jenis model yang didukung, seperti:

* Object Detection

* Oriented Bounding Box (OBB)

* Pose Estimation

* Instance Segmentation

Contoh-contoh ini sangat berguna sebagai referensi untuk membangun sistem computer vision sesuai kebutuhan Anda.

pada dokumentasi ini saya akan memberikan contoh membuild example untuk object detection

### 🎯 Build Example: Object Detection
Pada bagian ini, akan dijelaskan langkah-langkah membangun example untuk Object Detection.

#### 1. Masuk ke Direktori `detect`
Pada repository `TensorRT-YOLO`, di dalam folder `examples/` terdapat beberapa sub-direktori untuk masing-masing tipe model. Berikut struktur direktori secara umum:
```
examples/
├── classify/
├── detect/
├── mutli_thread/
├── obb/
├── pose/
├── segment/
└── Videopipe/
```

Untuk mulai membangun contoh Object Detection, masuk ke direktori `detect` dengan perintah:
```
cd examples/detect
```
#### 2. Sesuaikan File `CMakeLists.txt`
Di dalam direktori detect terdapat file `CMakeLists.txt` yang perlu disesuaikan. Pastikan path ke TensorRT dan deploy library telah sesuai dengan lokasi instalasi di sistem Anda.

Contoh bagian yang perlu disesuaikan ditunjukkan pada ilustrasi berikut:
![-](../images/yolo11+tensorrt/detect_cmake.png)

#### 3. Build Detect Example
Setelah penyesuain dilakukan, Anda dapat membangun proyek dengan langkah berikut:
```
mkdir build
cd build
cmake ..
make
```
Hasil build berupa executable bernama `detect` akan disimpan di direktori `bin/`.

#### 4. Konversi Model ke Format TensorRT
Sebelum menjalankan inferensi menggunakan executable `detect`, Anda memerlukan model dalam format `.engine` yang digunakan oleh TensorRT.

Biasanya, model YOLO tersedia dalam format `.pt` (PyTorch). Oleh karena itu, Anda perlu melakukan konversi secara bertahap:
```
.pt → .onnx → .engine
```

Anda dapat mengonversi model `.pt` menggunakan pacckage `Ultralytics` dengan mengikuti dokumentasi yang tersedia di sini 👉 [YOLO Custom Model](yolo_custom_dataset.md), atau menggunakan paket tensorrt_yolo. Namun, pastikan Anda menginstalnya terlebih dahulu dengan perintah berikut:
```
pip install -U tensorrt_yolo
```

Kemudian jalankan perintah berikut untuk konversi:
```
trtyolo export -w models/yolo11n.pt -v yolo11 -o models -s
```
> 🔍 Keterangan:

> * `-w`: path ke file model `.pt`

> * `-v`: versi model YOLO yang digunakan (misalnya: `yolo11`)

> * `-o`: direktori output untuk menyimpan file `.onnx`

> * `-s`: menyimpan model `.onnx` setelah proses konversi

Jika Anda sudah memiliki model dalam format `.onnx`, konversi ke `.engine` dapat dilakukan dengan:
```
trtexec --onnx=models/yolo11n.onnx --saveEngine=models/yolo11n.engine --fp16
```
> ⚠️ Proses konversi ini bisa memakan waktu cukup lama, tergantung spesifikasi perangkat Anda. Harap tunggu hingga proses selesai.

#### 5. Menjalankan Executable
Setelah file `detect` dan file `.engine` berhasil dibuat, masuk ke direktori `bin/` lalu jalankan perintah berikut:
```
./detect -e ../models/yolo11n.engine -i ../images/testing.jpeg -o ../output -l ../labels.txt
```
> Keterangan parameter:

> `-e`: Path ke file `.engine`

> `-i`: Path ke gambar input

> `-o`: Direktori output hasil inferensi

> `-l`: File label kelas

Berikut adalah hasil dari inferensi pada gambar input:

![-](../images/yolo11+tensorrt/testing.jpeg)

## Tambahan
Untuk examples model OBB, Pose Estimation, dan Instance Segmentation, langkah-langkah build hampir sama. Namun, konversi file ke format TensorRT `.engine` membutuhkan tambahan command seperti berikut:
```
trtexec --onnx=models/yolo11n-obb.onnx --saveEngine=models/yolo11n-obb.engine --fp16 --staticPlugins=/path/to/your/TensorRT-YOLO/lib/plugin/libcustom_plugins.so --setPluginsToSerialize=/path/to/your/TensorRT-YOLO/lib/plugin/libcustom_plugins.so
```
Untuk informasi lebih lanjut, kunjungi repositori berikut: 

👉 [https://github.com/laugh12321/TensorRT-YOLO.git](https://github.com/laugh12321/TensorRT-YOLO.git).
