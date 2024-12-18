# Autodistill: Auto Label Custom Dataset

![-](../images/autodistill/1.jpeg)

Autodistill adalah sebuah framework yang memungkinkan pengguna melakukan proses auto-labelling pada dataset sesuai kebutuhan. Proses ini dirancang untuk mempercepat workflow pengolahan data dengan cara mengotomatisasi tugas pelabelan yang biasanya membutuhkan waktu lama jika dilakukan secara manual. Dengan Autodistill, pengguna dapat fokus pada pengembangan model dan analisis data tanpa terbebani oleh proses pelabelan dataset yang berulang dan melelahkan.

berikut langkah-langkah untuk melakukan auto labeling pada dataset:

## 1. Setup Environment

Sangat dianjurkan untuk menggunakan environment Python, seperti Anaconda atau Python Virtual Environment. Hal ini bertujuan untuk menghindari konflik antar package pada lingkungan utama, serta memastikan instalasi yang lebih bersih dan terorganisasi.

Gunakan Jupyter Notebook atau platform lain yang mendukung file IPython Notebook (.ipynb) untuk mempermudah proses implementasi.

Jika environment telah disiapkan, langkah selanjutnya adalah menginstal package yang diperlukan. Berikut daftar package utama yang perlu diinstal:

- [PYTORCH](https://pytorch.org) - Jika menggunakan GPU, pastikan untuk menginstal [CUDA](../INSTALL/cuda_and_cudnn.md) pada perangkat tersebut, kemudian instal versi PyTorch yang mendukung CUDA untuk memanfaatkan akselerasi GPU dalam pelatihan model.
- Autodistill - Instal package Autodistill yang diperlukan untuk proses auto-labeling. Autodistill mendukung berbagai jenis tugas, seperti object detection atau instance segmentation.

Gunakan command berikut untuk menginstal semua package yang diperlukan. Untuk PyTorch, pastikan versi CUDA yang Anda gunakan sesuai dengan perangkat Anda.

```py
# Instal Autodistill dan dependensinya
!pip3 install autodistill
!pip3 install autodistill-yolov8 autodistill-grounding-dino
!pip3 install roboflow

# Instal PyTorch dengan dukungan CUDA (sesuaikan dengan versi cuda yang terdapat pada perangkat anda)
!pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124
```

## 2. Auto - label the Dataset

Jika environment dan package telah disiapkan, proses auto-labeling dapat dimulai. Pastikan dataset Anda telah disiapkan dalam bentuk direktori yang berisi gambar-gambar yang ingin diberi label. Tidak diperlukan struktur folder yang rumit, cukup directory sederhana dengan gambar di dalamnya.

### Contoh Implementasi
Berikut adalah contoh kode untuk memulai proses auto-labeling:

```py
import os
import shutil
from autodistill.detection import CaptionOntology
from autodistill_grounding_dino import GroundingDINO

# Definisikan Caption Ontology
ontology = CaptionOntology({
    "orange soccer ball": "Ball", 
    "black box with number inside a soccer goal": "Obstacle"
})

# Tentukan lokasi dataset dan folder output
IMAGES = r"E:\autodistill\images\obs"  # Path ke direktori gambar
DATASET_DIR_PATH = r"E:\autodistill\output"  # Path untuk output label

# Hapus folder output jika sudah ada
if os.path.exists(DATASET_DIR_PATH):
    shutil.rmtree(DATASET_DIR_PATH)

# Inisialisasi model dan proses pelabelan
base_model = GroundingDINO(ontology=ontology)
dataset = base_model.label(
    input_folder=IMAGES,
    extension=".png",  # Ekstensi gambar (ubah jika diperlukan)
    output_folder=DATASET_DIR_PATH
)

```

### Penjelasan Kode
#### a. Caption Ontology
CaptionOntology digunakan untuk mendefinisikan label berdasarkan deskripsi dari objek di dalam gambar. Contoh:

- `orange soccer ball` dilabeli sebagai `Ball`.
- `black box with number inside a soccer goal` dilabeli sebagai `Obstacle`.

Anda dapat menyesuaikan CaptionOntology dengan deskripsi objek sesuai kebutuhan proyek Anda.

#### b. Direktori Input dan Output

- `IMAGES`: Path ke folder yang berisi gambar yang akan dilabeli.
- `DATASET_DIR_PATH`: Path untuk menyimpan output hasil pelabelan.

#### c. Ekstensi File

Parameter `extension=".png"` dapat diubah sesuai dengan format gambar Anda, misalnya `.jpg` atau `.jpeg`.

#### d. Proses Auto-labeling

Metode `base_model.label()` akan memproses gambar di direktori input dan menghasilkan label di direktori output.


## 3. Output File
Setelah proses auto-labeling selesai, Autodistill akan menghasilkan dataset yang telah diberi label. Dataset tersebut biasanya langsung disusun dalam format train dan validation (train-val split) di dalam direktori output yang telah Anda tentukan.

### Langkah Selanjutnya:

#### a. Periksa Dataset dengan Tool Tambahan

Gunakan tool seperti [LabelImg](https://github.com/HumanSignal/labelImg.git) atau [Roboflow](https://roboflow.com) untuk memeriksa dan memverifikasi hasil auto-labeling.

- Auto-labeling dapat menghasilkan kesalahan, terutama untuk objek kompleks. Oleh karena itu, langkah review sangat disarankan.

#### b. Edit Dataset Jika Diperlukan

Jika terdapat kesalahan pelabelan, Anda dapat melakukan koreksi secara manual dengan alat yang disebutkan di atas.