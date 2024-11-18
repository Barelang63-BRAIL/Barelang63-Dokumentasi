# Dummy Monitor untuk Remote Desktop Tanpa Monitor Eksternal

Ketika melakukan remote desktop pada robot, biasanya dibutuhkan monitor eksternal agar tampilan dapat muncul. Namun, hal ini dapat diakali dengan menginstal dummy monitor pada Ubuntu. Dengan menggunakan dummy monitor, Anda dapat menjalankan remote desktop menggunakan aplikasi seperti NoMachine tanpa perlu menghubungkan monitor eksternal. Berikut adalah langkah-langkahnya:

## 1. Instalasi Paket Dummy Monitor

Untuk menyiapkan dummy monitor, Anda perlu menginstal packagenya. Jalankan perintah berikut untuk menginstallnya:
```{ .sh .copy }
sudo apt-get install xserver-xorg-video-dummy
```

## 2. Konfigurasi Xorg

Buat file konfigurasi Xorg untuk mengatur dummy monitor:
```{ .sh .copy }
sudo gedit /usr/share/X11/xorg.conf.d/xorg.conf
```

Tambahkan isi berikut ke file konfigurasi tersebut. Anda dapat menyesuaikan resolusi sesuai kebutuhan (disarankan menggunakan resolusi monitor yang digunakan untuk secara remote):
```
Section "Device"
    Identifier  "Configured Video Device"
    Driver      "dummy"
EndSection

Section "Monitor"
    Identifier  "Configured Monitor"
    HorizSync 31.5-48.5
    VertRefresh 50-70
EndSection

Section "Screen"
    Identifier  "Default Screen"
    Monitor     "Configured Monitor"
    Device      "Configured Video Device"
    DefaultDepth 24
    SubSection "Display"
    Depth 24
    Modes "1920x1080"
    EndSubSection
EndSection
```

## 3. Save file, Reboot dan Test