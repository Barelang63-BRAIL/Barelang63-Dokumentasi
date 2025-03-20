# Install Basestation

## Apa itu Basestation?
Basestation adalah aplikasi yang biasanya digunakan untuk memonitor/memberi perintah kepada robot pada saat pertandingan.

## Requirement
Ada beberapa library yang diperlukan untuk membuat Basestation:

- **QT5 / QT6**
- **VTK 9.* dengan dukungan QT yang diaktifkan**
- **[Rtbd2](../INSTALL/rtdb2_build.md)**

### Cara Build VTK 9.*
1. Salin folder VTK 9.* dari hardisk Barelang 63.
2. Ekstrak file tar VTK 9.*.
3. Masuk ke direktori VTK 9.*:
   ```sh
   mkdir build 
   cd build
   cmake .. -DVTK_GROUP_ENABLE_Qt=WANT -DVTK_QT_VERSION=5
   make -j$(nproc)
   sudo make install
   ```

### Cara Build Basestation
1. Salin folder Basestation dari hardisk Barelang 63.
2. Masuk ke Folder PROGRAM KRSBI BERODA dan copy file basestation.tar
3. Install di Terminal:
```
pip3 install nuitka
```
4. setelah copy file basestation.tar, lalu ekstrak file tersebut ke directory anda dan pergi ke directory basestation
5. Jalankan Perintah dibawah ini: 
```
python3 -m nuitka basestation_build.py -o basestation_build
```
```
python3 -m nuitka basestation_launch.py -o basestation_launch
```
6. setelah itu pindahkan executable basestation_launch dan basestation_build ke folder /usr/bin/ dengan command:
```
sudo mv basestation_build /usr/bin/
```
```
sudo mv basestation_launch /usr/bin/
```
7. kemudian kita bisa build basestation (Note 8 artinya sebanyak apa core cpu):   
```
basestation_build 8
```

## Menjalankan Basestation
Jalankan aplikasi Basestation dengan perintah berikut:
```sh
robot_launch build/basestation
```
untuk mengganti parameter running bisa menggunakan command berikut:
```
basestation_launch build/basestation --config_file /opt/offline/config/cfg.xml --network_name agent2 --id 50
```

Tampilan Basestation setelah dijalankan:
![Basestation UI](../images/basestation_folder/basestation.jpeg)
