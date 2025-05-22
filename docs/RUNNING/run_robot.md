# Dokumentasi Menjalankan Program Robot

Untuk menjalankan program robot ini, Anda perlu membagi terminal menjadi 3 bagian, lalu jalankan perintah-perintah berikut secara berurutan:



## 1. Jalankan Vision System
Buka terminal pertama dan jalankan:

```bash
./vision.sh
```
## 2. Jalankan Lowlevel System
Buka terminal kedua dan jalankan:

```bash
./lowlevel.sh
```

## 3. Jalankan Strategy Robot 
Buka terminal ketiga dan jalankan:

```bash
robot_launcher /opt/offline/bin/offline_node
```

## 4. Jalankan Basestation
Gunakan Monitor PC Barelang63:

- WiFi sudah terhubung ke router barelang63
- Sudah berada di direktori folder basestation

```bash
basestation_launch build/basestation
```

## Optional Control Robot Joystick
Jika ingin menggunakan joystick maka run command dibawah ini saja:
```bash
robot_launcher /opt/offline/bin/joystick_reader
```