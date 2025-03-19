# Cara debug STM32

## Cara membaca data input/sensor pada STM32

1. Pertama, koneksikan ST-LINK STM32 anda dengan PC/Laptop anda.
2. Untuk board Nucleo-F767ZI STM32, memiliki ST-LINK internal sendiri jadi kita disini tinggal mengkoneksikan boardnya ke-PC lewat ST-LINK nya.
![Alt Text](../images/stm32_folder/Nucleo-F767ZI.png)
STM32 F407-DISC juga memiliki ST-LINK internalnya sendiri 
![Alt Text](../images/stm32_folder/stm32-F407.png)
3. Jika tidak menggunakan ST-LINK internal dikarenakan rusak atau tidak ada, bisa menggunakan ST-LINK external. Bisa dilihat caranya [disini](ST-LINK.md)
4. Disini sebagai contoh kita akan membaca input dari button yang ada pada STM-nya. Seperti biasa, buatlah projek STM32 baru sesuai dengan board STM32 yang digunakan,
disini saya menggunakan STM32 F407-DISC.
![Alt Text](../images/stm32_folder/debug_stm1.png)
5. Lalu lihatlah pin Pushbutton yang ada pada STM yang anda gunakan pada file .ioc nya, seperti contoh disini pin Pushbutton saya berada pada PA0
![Alt Text](../images/stm32_folder/debug_stm2.png)
6. Pergi ke file main.c nya, dan buatlah variable untuk menyimpan input dari button, bisa menggunakan int atau bool. Disini saya membuat nama variablenya 'Tes'
![Alt Text](../images/stm32_folder/debug_stm3.png)
7. Pada loop-nya (disini while), buat fungsi readnya. Karena disini pin pushbuttonnya PA0, artinya port nya A dan pin-nya 1.
![Alt Text](../images/stm32_folder/debug_stm4.png)
8. Lalu klik tombol debug (ber-logo kumbang), dan klik ok
![Alt Text](../images/stm32_folder/debug_stm5.png)
![Alt Text](../images/stm32_folder/debug_stm6.png)
Jika cubeIDE nya meminta persetujuan pergantian perspective, tekan saja OK.
9. Lalu klik "Live Expression" (berlogo kacamata berwarna hitam), lalu masukkan variable yang ingin kita baca, seperti contoh disini kita ingin membaca "tes".
klik "Add new expression", dan masukkan nama variablenya
![Alt Text](../images/stm32_folder/debug_stm7.png)
![Alt Text](../images/stm32_folder/debug_stm8.png)
tekan enter
10. Kemudian tekan "resume" atau tekan tombol f8, lalu lihat perubahan value data "tes" sambil kamu menekan pushbuttonnya
![Alt Text](../images/stm32_folder/debug_stm9.png)
jika tombol tidak ditekan
![Alt Text](../images/stm32_folder/debug_stm10.png)
jika tombol ditekan
![Alt Text](../images/stm32_folder/debug_stm11.png)

Nah sekarang cobalah menggunakan pushbutton/sensor dari external (luar board)!
