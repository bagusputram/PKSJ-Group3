#A. Pendahuluan
#B. Dasar Teori
#C. Instalasi
## C.1. Instalasi Ubuntu Server
Ubuntu Server akan diinstall secara virtual menggunakan VMware yang sudah terinstall pada Windows 10. Sebelum menginstall Ubuntu Server tentu saja harus mendownload installer Ubuntu Servernya.
```
http://www.ubuntu.com/download/server
```
Setelah download selesai, langkah berikutnya adalah menginstall Ubuntu Server pada VMware.

1. Create a New Virtual Machine pada VMware Workstation kemudian akan muncul window baru seperti gambar dibawah ini

 [![u1.jpg](http://s5.postimg.org/msx07s85j/image.jpg)](https://postimg.org/image/ijsa5m4w3/)

 Untuk tipe konfigurasinya pilih Custom, karena akan ada yang harus diubah konfigurasinya. Kemudian klik Next

2. Pada window ini tidak perlu diubah konfigurasinya. Konfigurasinya kurang lebih seperti gambar dibawah ini. Klik Next untuk menuju windows selanjutnya.

 [![u2.jpg](http://s5.postimg.org/mhfjv0rpj/image.jpg)](https://postimg.org/image/nwh4jqssj/)

3. Pada window ini pilih lokasi installer yang sudah didownload sebelumnya.

 [![u3.jpg](https://s5.postimg.org/bvvoj0ldz/image.jpg)](https://postimg.org/image/a42po420z/)

 Klik Browse kemudian pilih lokasi installer Ubuntu Server. Setelah memilih lokasi installer klik Next untuk menuju window selanjutnya

4. Berikan nama untuk Virtual Machine yang akan dibuat.

 [![u4.jpg](https://s5.postimg.org/5w7xfd0lj/image.jpg)](https://postimg.org/image/hy3b9i9tv/)

 Berikan nama Virtual Machine yang akan dibuat sesuai keinginan. Jika ingin mengganti lokasi Virtual Machine yang akan diinstall bisa klik Browse kemudian pilih lokasi yang baru yang diinginkan. Klik Next untuk menuju windows selanjutnya.

5. Pilih jumlah processor dan juga core yang akan digunakan untuk menjalankan Virtual Machine ini

 [![u5.jpg](https://s5.postimg.org/od2c66gjr/image.jpg)](https://postimg.org/image/ue013935v/)

 Konfigurasi processor mengikuti processor yang digunakan pada komputer masing-masing. Supaya tidak terlalu memberatkan konfigurasi yang digunakan seperti gambar di atas.

6. Pilih jumlah memory yang akan digunakan

 [![u6.jpg](https://s5.postimg.org/4whmjnlfr/image.jpg)](https://postimg.org/image/jforl2ekj/)

 Konfigurasi memory disesuaikan dengan jumlah memory yang dimiliki komputer masing-masing. Komputer yang digunakan memiliki memory 8GB sehingga bila 1GB digunakan untuk menjalankan Virtual Machine tidak akan menjadi masalah.

7. Pilih tipe koneksi internetnya

 [![u7.jpg](https://s5.postimg.org/d39mb8bif/image.jpg)](https://postimg.org/image/6ct51socj/)

 Konfigurasikan seperti pada gambar di atas.

8. Pada window ini tidak perlu diubah konfigurasinya. Langsung klik next untuk menuju window selanjutnya

 [![u8.jpg](https://s5.postimg.org/w9res5hdz/image.jpg)](https://postimg.org/image/6e7o8yfk3/)

9. Pada window ini juga tidak diperlukan perubahan pada konfigurasinya. Klik next untuk menuju window selanjutnya.

 [![u9.jpg](https://s5.postimg.org/v8r6310ef/image.jpg)](https://postimg.org/image/lo7jg5b2b/)

10. Membuat Virtual Disk untuk Virtual Machine yang akan diinstall

 [![u10.jpg](https://s5.postimg.org/n4j1yadzb/U10.jpg)](https://postimg.org/image/5r8rjfio3/)

 Pilih sesuai gambar di atas untuk membuat Virtual Disk yang baru. Kemudian klik next

11. Pilih ukuran maksimum virtual disk yang diinginkan

 [![u11.jpg](https://s5.postimg.org/w0tu284lj/U11.jpg)](https://postimg.org/image/iwo9pjcjn/)

 Pada gambar di atas ukuran maksimum virtual disk adalah 20GB. Kemudian pilih Store virtual disk as single file untuk meningkatkan performa virtual disk yang akan dibuat.

12. Pada window ini nama virtual disk yang akan dibuat sama seperti penamaan Virtual Machine yang akan dibuat

 [![u12.jpg](https://s5.postimg.org/mubjexzd3/U12.jpg)](https://postimg.org/image/mubjexzcz/)

 Nama virtual disk bisa diganti sesuai keinginan. Untuk lebih mudahnya disamakan saja dengan nama Virtual Machinenya.

13. Pada window ini menampilkan seluruh konfigurasi untuk Virtual Machine yang akan dibuat.

 [![u13.jpg](https://s5.postimg.org/4sseh55c7/U13.jpg)](https://postimg.org/image/lgjwjn03n/)

 Klik next untuk memulai proses installasi Ubuntu Server

14. Lakukan proses installasi Ubuntu Server seperi menginstall ubuntu server pada komputer biasa.

 [![u14.jpg](https://s5.postimg.org/yyqsvxc93/U14.jpg)](https://postimg.org/image/jq0vi5ikj/)

15. Setelah Selesai akan muncul tampilan seperti pada gambar di bawah ini

 [![u15.jpg](https://s5.postimg.org/my5cv74uf/U15.jpg)](https://postimg.org/image/z00qpce2r/)

 Klik Continue untuk menjalankan Ubuntu Server

## C.2. Instalasi OSSEC
1. Lakukan Update dan Upgrade Ubuntu server
Update dan upgrade terlebih dahulu ubuntu server agar mendapatkan daftar package paling baru dan dapat menginstall file-file yang dibutuhkan untuk menginstall OSSEC IDS
```
sudo apt-get upgrade
sudo apt-get update
```

2. Install SSH
Pengguna dapat menginstall SSH agar dapat dengan mudah mengakses ubuntu server
```
sudo apt-get install ssh
```

3. Akses Ubuntu Server melalui SSH
Cek ip dari ubuntu server
```
ifconfig
```
Akses ip dengan memasukkan username dari ubuntu server
```
ssh username@ip
```

4. Install LAMP
-Install Apache
Install Apache terlebih dahulu sebagai web server
```
sudo apt-get install apache2
```
-Jalankan Apache
Jalankan service apache2 setelah penginstallan selesai agar web server dapat diakses
```
service apache2 start
```
-Install MySql
Install mySql untuk membuat database
```
sudo apt-get install mysql-server
```
-Install PHP
Install PHP pada ubuntu server
```
sudo apt-get install php5 php5-mysql php-pear php5-gd  php5-mcrypt php5-curl
```

5. Download file OSSEC
```
wget https://bintray.com/artifact/download/ossec/ossec-hids/ossec-hids-2.8.3.tar.gz
```

6. Install gcc
gcc digunakan ketika melakukan penginstallan ossec
```
sudo apt-get install gcc
```

7. Install make
make digunakan ketika menginstall database
```
sudo apt-get install make
```

8. Extract file OSSEC
```
tar -xzf ossec-hids-2.8.3.tar.gz
```

9. Install postgresql
```
sudo apt-get install postgresql
```

10. Install libpq-dev
```
sudo apt-get install libpq-dev
```

11. Install database
```
cd ossec-hids-2.8.3
cd src
make setdb
```

12. Install OSSEC
```
cd ../
./install.sh
```

13. Start OSSEC
```
/var/ossec/bin/ossec-control start
```

14. Konfigurasi database OSSEC
```
mysql_secure_installation
```
```
-Set root password? [Y/n] y
-Remove anonymous users? [Y/n] y
-Disallow root login remotely? [Y/n] y
-Remove test database and access to it? [Y/n] y
-Reload privilege tables now? [Y/n] y
```
```
mysql -u root -p
```
```
create database ossec;
grant all privileges on ossec.* to ossecuser@localhost identified by 'your_password';
flush privileges;
exit
```

15. Import schema MySql
```
mysql -u ossecuser -p ossec < src/os_dbd/mysql.schema
```

16. 

#D. Analisis Penyerangan
#E. Kesimpulan dan Saran