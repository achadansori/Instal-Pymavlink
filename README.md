# Instal-Pymavlink-Penship
https://www.ardusub.com/developers/pymavlink.html

# Update list of available packages
sudo apt update
sudo apt -y upgrade

# Install some dependencies
sudo apt install -y python3-pip

# Install mavproxy module and everything else needed
pip3 install mavproxy

Kesalahan yang sama terjadi lagi, yaitu "Permission denied" saat mencoba mengakses port serial `/dev/ttyTHS1`. Berikut adalah beberapa langkah tambahan yang dapat Anda coba:

1. Pastikan Jetson Nano Anda terhubung dengan Pixhawk melalui port serial `/dev/ttyTHS1`. Jika tidak, ganti dengan port serial yang benar.

2. Periksa apakah pengguna saat ini memiliki izin untuk mengakses port serial dengan menjalankan perintah berikut:
   ```
   ls -l /dev/ttyTHS1
   ```

   Pastikan pengguna yang Anda gunakan memiliki izin untuk membaca/tulis pada perangkat serial. Izin yang benar harus menunjukkan pengguna dan grup yang sesuai (misalnya, `root dialout`) dan hak akses `rw` (membaca dan menulis).

3. Jika izin pada port serial tidak benar, Anda dapat mengubahnya dengan menjalankan perintah berikut:
   ```
   sudo chmod a+rw /dev/ttyTHS1
   ```

   Ini akan memberikan izin membaca/tulis ke semua pengguna pada port serial. Pastikan untuk menggunakan perangkat serial yang benar dalam perintah tersebut.

4. Pastikan tidak ada proses lain yang menggunakan port serial. Anda dapat memeriksa proses yang sedang berjalan dengan perintah `sudo lsof /dev/ttyTHS1`. Jika ada proses yang sedang menggunakan port serial tersebut, Anda perlu menghentikan proses tersebut atau mengubah pengaturan program agar tidak menggunakan port serial yang sedang digunakan.

Setelah mencoba langkah-langkah ini, periksa kembali apakah Anda dapat mengakses port serial `/dev/ttyTHS1` dan menjalankan program Anda tanpa kesalahan "Permission denied".





Maaf, tampaknya perintah `lsof` tidak tersedia di sistem Anda. Perintah tersebut biasanya digunakan untuk melihat proses yang sedang menggunakan suatu file atau perangkat.

Sebagai alternatif, Anda dapat mencoba menggunakan perintah `fuser` untuk melihat proses yang menggunakan perangkat serial. Silakan coba jalankan perintah berikut:

```
sudo fuser /dev/ttyTHS1
```

Jika perangkat serial `/dev/ttyTHS1` sedang digunakan oleh proses lain, perintah ini akan menampilkan ID proses yang terkait. Anda dapat menggunakan ID proses tersebut untuk menghentikan proses tersebut atau menelusuri lebih lanjut mengapa perangkat serial sedang digunakan.

Jika `fuser` juga tidak tersedia di sistem Anda, Anda mungkin perlu menginstal paket yang sesuai untuk perintah tersebut. Di sebagian besar distribusi Linux, Anda dapat menginstal paket `lsof` atau `psmisc` untuk mendapatkan utilitas `lsof` dan `fuser`. Anda dapat menggunakan manajer paket yang sesuai untuk menginstal paket-paket tersebut (misalnya, `apt-get` untuk Debian atau Ubuntu).

Jika Anda masih mengalami kesulitan atau memiliki pertanyaan lebih lanjut, silakan beri tahu saya, dan saya akan dengan senang hati membantu Anda.




Terima kasih atas informasinya. Berdasarkan keluaran `fuser`, terlihat bahwa ada dua proses yang menggunakan perangkat `/dev/ttyTHS1`. Proses-proses tersebut memiliki ID 8034 dan 31505.

Untuk menghentikan proses-proses tersebut, Anda dapat menggunakan perintah `kill` diikuti dengan ID proses. Misalnya, untuk menghentikan proses dengan ID 8034, jalankan perintah berikut:

```
sudo kill 8034
```

Lakukan hal yang sama untuk ID proses 31505 jika perlu.

Setelah menghentikan proses-proses tersebut, coba jalankan program Anda kembali dan periksa apakah masalahnya teratasi.

Jika Anda masih mengalami kesulitan atau memiliki pertanyaan lebih lanjut, silakan beri tahu saya. Saya siap membantu Anda.
