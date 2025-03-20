# Robot Builder dan Robot Launcher

Pada robot, terdapat lingkungan khusus yang berisi executable package, header file, library, dan berbagai komponen lainnya dari package yang digunakan, seperti omni_vision, zed, amcl, nucleo, maupun strategi_node. Saat dokumentasi ini ditulis, lingkungan robot tersebut berada di dalam folder ``/opt/offline``.

Untuk mempermudah proses build serta menjalankan executable yang terdapat dalam lingkungan khusus ini, dibuat dua executable, yaitu robot_build dan robot_launcher. Kedua executable ini dikembangkan menggunakan Python Nuitka.

## Apa itu Nuitka??
Nuitka adalah compiler Python yang mengoptimalkan kode dan ditulis menggunakan Python. Nuitka mengubah kode Python menjadi executable. Dalam kasus ini, Nuitka digunakan untuk membuat executable yang berfungsi membuild kode C++ yang memiliki file CMakeLists.txt serta menjalankan executable package pada robot.

Untuk menginstal Nuitka, jalankan perintah berikut di Terminal:
```
pip3 install nuitka
```

## Robot Builder
Seperti yang telah dijelaskan sebelumnya, executable ``robot_build`` berfungsi untuk build package yang terdapat pada robot. Berikut adalah contoh kode Python untuk implementasi ``robot_build``:
```py
#!/usr/bin/python3

import subprocess
import argparse

def cmake_build(folder, nproc):
    subprocess.run(['cmake', folder, '-B', '/opt/offline/build/'+folder])
    subprocess.run(['cmake', '--build', '/opt/offline/build/'+folder, '-j'+ str(nproc)])
    subprocess.run(['cmake', '--install', '/opt/offline/build/'+folder])


if __name__ == "__main__":
    parser = argparse.ArgumentParser(description='CMake builder script')
    parser.add_argument('package_name', type=str, help='package_name')
    parser.add_argument('proc', type=str, help='nproc')
    args = parser.parse_args()

    cmake_build(args.package_name, args.proc)

```

Simpan kode di atas dengan nama ``robot_builder.py``.

Kode Python ini berfungsi sebagai script untuk membuild package menggunakan CMake secara otomatis ke dalam folder ``/opt/offline/build.``

### Mengonversi robot_builder.py Menjadi Executable
Untuk mengonversi script Python robot_build.py menjadi executable menggunakan Nuitka, jalankan command berikut di terminal:
```
python3 -m nuitka robot_builder.py -o robot_build
```
Tunggu hingga proses selesai. Jika berhasil, perintah ini akan menghasilkan file ``robot_build``, yang merupakan executable.

### Memindahkan Executable agar Dapat Digunakan Secara Global
Agar executable ini dapat digunakan di seluruh sistem tanpa harus menjalankannya dari direktori tertentu, pindahkan ke folder ``/usr/bin/`` dengan command berikut:
```
sudo mv robot_build /usr/bin/
```

### Cara Menggunakan robot_build
Setelah dipindahkan ke ``/usr/bin/``, Anda dapat menjalankan ``robot_build`` dari mana saja dengan command berikut:
```
robot_build nama_package 8
```
> Catatan: Gantilah 8 dengan jumlah core yang ingin digunakan saat proses build untuk meningkatkan kecepatan kompilasi.

## Robot Launcher

Executable ``robot_launch`` berfungsi untuk menjalankan executable pada package robot yang telah dibuild, pada saat doukumentasi in ditulis berikut script python untuk membuat executable ``robot launcher``.
```py
#!/usr/bin/python3
import subprocess
import argparse
import yaml
from icecream import ic
# Replace 'executable_name' with the path to your executable
# Replace 'arg1', 'arg2', etc. with your actual arguments

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description='program launcher script')
    parser.add_argument('program_name', type=str, help='program_name')
    try:
        with open("/opt/offline/config/rtdb_file.yaml", 'r') as file:
            data = yaml.safe_load(file)
            
        args = parser.parse_args()
        executable_path = args.program_name
        arguments_1 = ['--agent_id', str(data['id']), '--rtdb_config_file',
               data['rtdb_config_file'], '--network_name',  data['network_name']]
        # Launch the executable with arguments
        subprocess.run([executable_path] + arguments_1, check=True)
    except subprocess.CalledProcessError as e:
        print(f"Error: {e}")
```

Script ``robot_launcher.py`` dibuat untuk mempermudah menjalankan executable package robot dengan otomatis mengisi parameter yang diperlukan untuk menghubungkan package tersebut ke [RTDB2](../INSTALL/rtdb2_build.md). Pada saat dokumentasi ini ditulis, executable package robot memerlukan argumen tambahan agar dapat berfungsi dengan benar. Oleh karena itu, script ini membaca konfigurasi dari file ``rtdb_file.yaml`` yang berada di path ``/opt/offline/config/``, sehingga parameter yang dibutuhkan akan terisi secara otomatis tanpa harus memasukkannya secara manual saat menjalankan executable package.

### Mengonversi robot_launcher.py Menjadi Executable
Sama seperti ``robot_build``, untuk menjadikan ``robot_launcher.py`` sebagai file executable, jalankan command berikut di terminal:
```sh
python3 -m nuitka robot_launcher.py -o robot_launch
```

### Memindahkan Executable agar Dapat Digunakan Secara Global
Setelah proses selesai, pindahkan file executable ke ``/usr/bin/`` agar dapat diakses dari mana saja:
```
sudo mv robot_launch /usr/bin/
```

### Cara Menggunakan robot_launch
Setelah dipindahkan ke ``/usr/bin/``, Anda dapat menjalankan ``robot_launch`` dari mana saja dengan command berikut:
```
robot_launch /opt/offline/bin/offline_node
```
> Catatan: Gantilah path ``/opt/offline/bin/offline_node`` dengan path executable yang ingin dijalankan sesuai dengan kebutuhan Anda.


