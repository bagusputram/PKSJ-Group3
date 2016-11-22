#A. Pendahuluan

IDS (Intrusion Detection System) adalah sebuah sistem yang melakukan pengawasan terhadap traffic jaringan dan pengawasan terhadap kegiatan-kegiatan yang mencurigakan didalam sebuah sistem jaringan. Jika ditemukan kegiatan - kegiatan yang mencurigakan berhubungan dengan traffic jaringan maka IDS akan memberikan peringatan kepada sistem atau administrator jaringan. Dalam banyak kasus IDS juga merespon terhadap traffic yang tidak normal/ anomali melalui aksi pemblokiran seorang user atau alamat IP (Internet Protocol) sumber dari usaha pengaksesan jaringan.

IDS sendiri muncul dengan beberapa jenis dan pendekatan yang berbeda yang intinya berfungsi untuk mendeteksi traffic yang mencurigakan didalam sebuah jaringan. Beberapa jenis IDS adalah : yang berbasis jaringan (NIDS) dan berbasis host (HIDS). Ada IDS yang bekerja dengan cara mendeteksi berdasarkan pada pencarian ciri-ciri khusus dari percobaan yang sering dilakukan. Cara ini hampir sama dengan cara kerja perangkat lunak antivirus dalam mendeteksi dan melindungi sistem terhadap ancaman. Kemudian ada juga IDS yang bekerja dengan cara mendeteksi berdasarkan pada pembandingan pola traffic normal yang ada dan kemudian mencari ketidaknormalan traffic yang ada. Ada IDS yang fungsinya hanya sebagai pengawas dan pemberi peringatan ketika terjadi serangan dan ada juga IDS yang bekerja tidak hanya sebagai pengawas dan pemberi peringatan melainkan juga dapat melakukan sebuah kegiatan yang merespon adanya percobaan serangan terhadap sistem jaringan dan komputer.

Pada percobaan kali ini akan dilakukan deteksi intrusi pada ubuntu server dengan menggunakan hydra.

#B. Dasar Teori

Sesuai dengan penjelasan diatas, percobaan kali ini akan mendeteksi intrusi pada ubuntu server. Intrusi dilakukan dengan brute force attack menggunakan tool hydra. Berikut penjelasan tool yang akan digunakan pada percobaan kali ini :

1. VMWare Workstation 

	VMWare Workstation adalah software untuk virtual machine yang compatible dengan komputer Intel x86. Software ini memungkinkan pemakai untuk membuat satu atau lebih virtual machine dan menjalankannya secara serempak. Masing-masing virtual machine dapat menjalankan guest operating system-nya sendiri seperti Linux, Windows, BSD, dan lain-lain. Tetapi software ini tidak dapat menjalankan virtual machine yang dibuat oleh produk VMWare yang lain.
    
2. Ubuntu Server

	Linux Ubuntu Server adalah system operasi turunan dari Linux Ubuntu yang di desain khusus dengan kernel yang telah dikustomisasi untuk bekerja sebagai system operasi server. Kernel Linux Ubuntu Server di desain khusus untuk bisa bekerja dengan lebih dari satu proses (multiprocessor) dengan dukungan NUMA pada 100Hz internal timer frequency dan menggunakan pennjadwalan deadline I/O. 
    
    Linux Ubuntu Server memiliki lisensi open source dan gratis serta merupakan turunan dari distro linux debian sehingga memiliki keamanan yang cukup tinggi. Linux Ubuntu Server ini mempunyai kebutuhan minimum atau resource yang harus dipenuhi diantaranya adalah processor 300 MHz, Memory 64MB, Harddisk 500MB dan VGA 640×480. Namun untuk meningkatkan kinerja pada computer resource pada computer harus disediakan lebih tinggi.
    
3. Ubuntu 16.04 LTS

	Ubuntu adalah [sistem operasi] lengkap berbasis Linux, tersedia secara bebas dan mempunyai dukungan baik yang berasal dari komunitas maupun tenaga ahli profesional. Komunitas Ubuntu dibentuk berdasarkan gagasan yang terdapat di dalam filosofi Ubuntu:
     * bahwa perangkat lunak harus tersedia dengan bebas biaya
     * bahwa aplikasi perangkat lunak tersebut harus dapat digunakan dalam bahasa lokal masing-masing dan untuk orang-orang yang mempunyai keterbatasan fisik, dan
     * bahwa pengguna harus mempunyai kebebasan untuk mengubah perangkat lunak sesuai dengan apa yang mereka butuhkan.

  Perihal kebebasan inilah yang membuat Ubuntu berbeda dari perangkat lunak berpemilik (proprietary); bukan hanya peralatan yang Anda butuhkan tersedia secara bebas biaya, tetapi Anda juga mempunyai hak untuk memodifikasi perangkat lunak Anda sampai perangkat lunak tersebut bekerja sesuai dengan yang Anda inginkan.

	Nama Ubuntu diambil dari nama sebuah konsep ideologi di Afrika Selatan. “Ubuntu” berasal dari bahasa kuno Afrika, yang berarti “rasa perikemanusian terhadap sesama manusia”. Ubuntu juga bisa berarti “aku adalah aku karena keberadaan kita semua”. Tujuan dari distribusi Linux Ubuntu adalah membawa semangat yang terkandung di dalam Ubuntu ke dalam dunia perangkat lunak.
    
4. Brute Force Attack

	Brute force attack adalah salah satu metode password cracking dengan cara mencoba semua kemungkinan kombinasi password yang disimpan didalam file wordlist. Kelemahan dalam meretas password menggunakan metode brute force ini memakan banyak waktu dan resource tergantung oleh panjang dan kombinasi karakter password yang akan diretas. Sebuah password dapat dibongkar dengan menggunakan program yang mencoba membuka password yang sudah terenkripsi dengan menggunakan algoritma tertentu dengan mencoba semua kemungkinan. Salah satu tools yang biasa digunakan dalam password cracking adalah medusa, hydra, ataupun ncrack. Dalam percobaan, akan dilakukan teknik brute force attack menggunakan tools medusa.


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

1.Lakukan Update dan Upgrade Ubuntu server

Update dan upgrade terlebih dahulu ubuntu server agar mendapatkan daftar package paling baru dan dapat menginstall file-file yang dibutuhkan untuk menginstall OSSEC IDS

[![1.png](https://s3.postimg.org/3trlyahg3/image.png)](https://postimg.org/image/46j04gzpr/)

```
sudo apt-get upgrade
sudo apt-get update
```

2.Install SSH

Pengguna dapat menginstall SSH agar dapat dengan mudah mengakses ubuntu server

[![2.png](https://s3.postimg.org/l8bu6kekz/image.png)](https://postimg.org/image/ll38cqwun/)

```
sudo apt-get install ssh
```

3.Akses Ubuntu Server melalui SSH

Cek ip dari ubuntu server

[![3.png](https://s3.postimg.org/4ylo3o3wz/image.png)](https://postimg.org/image/gay9lgclr/)

```
ifconfig
```

Akses ip dengan memasukkan username dari ubuntu server

[![4.png](https://s3.postimg.org/xodlxfe8j/image.png)](https://postimg.org/image/qxx4nzr2n/)

```
ssh username@ip
```

[![5.png](https://s3.postimg.org/b0ycr9yoj/image.png)](https://postimg.org/image/pk5hsortb/)

4.Install LAMP

-Install Apache

Install Apache terlebih dahulu sebagai web server

[![6.png](https://s3.postimg.org/qay7ygu6r/image.png)](https://postimg.org/image/yt7o2t0pb/)

```
sudo apt-get install apache2
```

-Jalankan Apache

Jalankan service apache2 setelah penginstallan selesai agar web server dapat diakses

[![7.png](https://s3.postimg.org/bg9mkaklv/image.png)](https://postimg.org/image/5s3bteg9b/)

```
service apache2 start
```

[![8.png](https://s3.postimg.org/9pqlit32r/image.png)](https://postimg.org/image/9pqlit32n/)

-Install MySql

Install mySql untuk membuat database

[![9.png](https://s3.postimg.org/wsh4hz4k3/image.png)](https://postimg.org/image/554f3vjdb/)

```
sudo apt-get install mysql-server
```

-Install PHP

Install PHP pada ubuntu server

[![10.png](https://s3.postimg.org/q3al1yj83/image.png)](https://postimg.org/image/9fj2zgogf/)

```
sudo apt-get install php5 php5-mysql php-pear php5-gd  php5-mcrypt php5-curl
```

5.Download file OSSEC

[![11.png](https://s3.postimg.org/syno8tn83/image.png)](https://postimg.org/image/syno8tn7z/)

```
wget https://bintray.com/artifact/download/ossec/ossec-hids/ossec-hids-2.8.3.tar.gz
```

6.Install gcc

gcc digunakan ketika melakukan penginstallan ossec

[![12.png](https://s3.postimg.org/xltqalakz/image.png)](https://postimg.org/image/pgbocfmbz/)

```
sudo apt-get install gcc
```

7.Install make

make digunakan ketika menginstall database

[![13.png](https://s3.postimg.org/9w4alwc7n/image.png)](https://postimg.org/image/dfq8bpexb/)

```
sudo apt-get install make
```

8.Extract file OSSEC

[![14.png](https://s3.postimg.org/uuf1xq1g3/image.png)](https://postimg.org/image/4yvbeizm7/)

```
tar -xzf ossec-hids-2.8.3.tar.gz
```

9.Install postgresql

[![16.png](https://s3.postimg.org/qb2tc7jkj/image.png)](https://postimg.org/image/ngznyrhe7/)

```
sudo apt-get install postgresql
```

10.Install libpq-dev

[![17.png](https://s3.postimg.org/5s7x755n7/image.png)](https://postimg.org/image/wdag2p80f/)

```
sudo apt-get install libpq-dev
```

11.Install database

[![15.png](https://s3.postimg.org/diepca7yr/image.png)](https://postimg.org/image/abk5snnin/)

```
cd ossec-hids-2.8.3
cd src
make setdb
```

12.Install OSSEC

[![18.png](https://s3.postimg.org/njjjlll1v/image.png)](https://postimg.org/image/njjjlll1r/)

[![19.png](https://s3.postimg.org/9edqjsc0j/image.png)](https://postimg.org/image/8ouy7fbgv/)

```
cd ../
./install.sh
```

[![20.png](https://s3.postimg.org/obm7ksp8z/image.png)](https://postimg.org/image/nyutem6z3/)

[![21.png](https://s3.postimg.org/cb0rk2hub/image.png)](https://postimg.org/image/6zluzcvrj/)

[![22.png](https://s3.postimg.org/oe637mswj/image.png)](https://postimg.org/image/l7bjo08gf/)

[![23.png](https://s3.postimg.org/c0t90q383/image.png)](https://postimg.org/image/u3mbrxz2n/)

[![24.png](https://s3.postimg.org/hqe2yrys3/image.png)](https://postimg.org/image/9xnf6sssv/)

[![25.png](https://s3.postimg.org/sehtxm8r7/image.png)](https://postimg.org/image/9m5yu1ccv/)

[![26.png](https://s3.postimg.org/ytguuafgz/image.png)](https://postimg.org/image/ux3iyauhb/)

[![27.png](https://s3.postimg.org/qchcjdas3/image.png)](https://postimg.org/image/qp8qpjt1r/)

[![28.png](https://s3.postimg.org/vcesrbger/image.png)](https://postimg.org/image/c7bjhk1qn/)

[![29.png](https://s3.postimg.org/atjwm92hf/image.png)](https://postimg.org/image/ffg0ulo0f/)

[![30.png](https://s3.postimg.org/upfw1sjir/image.png)](https://postimg.org/image/mjxu3mv9r/)

13.Start OSSEC

```
/var/ossec/bin/ossec-control start
```

[![31.png](https://s3.postimg.org/ktet25dqr/image.png)](https://postimg.org/image/q4tpmuztb/)

14.Konfigurasi database OSSEC

[![32.png](https://s3.postimg.org/8std1f6c3/image.png)](https://postimg.org/image/fw18h1brj/)

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

[![33.png](https://s3.postimg.org/u3qx5oogj/image.png)](https://postimg.org/image/v613o879r/)

```
mysql -u root -p
```

[![34.png](https://s3.postimg.org/la4m2bqvn/image.png)](https://postimg.org/image/uhwuj0xxr/)

[![35.png](https://s3.postimg.org/srdthjger/image.png)](https://postimg.org/image/vlgyuzikv/)

[![36.png](https://s3.postimg.org/3mmt44gyb/image.png)](https://postimg.org/image/5efrz10b3/)

```
create database ossec;
grant all privileges on ossec.* to ossecuser@localhost identified by 'your_password';
flush privileges;
exit
```

15.Import schema MySql

```
mysql -u ossecuser -p ossec < src/os_dbd/mysql.schema
```

16.Konfigurasi OSSEC

[![37.png](https://s3.postimg.org/c6671vpar/image.png)](https://postimg.org/image/658i4t2of/)

```
sudo nano /var/ossec/etc/ossec.conf
```

Copy pengaturan dibawah ini

[![38.png](https://s3.postimg.org/pblp7zj6b/image.png)](https://postimg.org/image/90llbo6of/)

```
<database_output>
        <hostname>127.0.0.1</hostname>
        <username>ossecuser</username>
        <password>your_pass</password>
        <database>ossec</database>
        <type>postgresql</type>
</database_output>
```

17.Enable database

[![39.png](https://s3.postimg.org/l3qwz8hqr/image.png)](https://postimg.org/image/91vj538i7/)

```
/var/ossec/bin/ossec-control enable database
/var/ossec/bin/ossec-control restart
```

18.Instalasi WEB-UI

[![40.png](https://s3.postimg.org/gvw4qhgb7/image.png)](https://postimg.org/image/lujn50k3z/)

[![41.png](https://s3.postimg.org/7cmfx0ssz/image.png)](https://postimg.org/image/yn7r4xvpr/)

[![42.png](https://s3.postimg.org/ze0hapy37/image.png)](https://postimg.org/image/kutc9b4y7/)

```
cd /var/www/html/
sudo wget https://github.com/ossec/ossec-wui/archive/master.zip
sudo unzip master.zip
sudo mv ossec-wui-master/ ossec/
```

19.Konfigurasi ownership

[![43.png](https://s3.postimg.org/w8fvkifgz/image.png)](https://postimg.org/image/6pnj7hvwv/)

```
sudo mkdir ossec/tmp/
sudo chown www-data: -R ossec/
sudo chmod 666 /var/www/html/ossec/tmp
sudo usermod -a -G ossec www-data
```

#D. Analisis Penyerangan
##D.1 Brute Force Attack
1. Attack dengan menggunakan hydra

[![45.png](https://s3.postimg.org/uw2rwd7f7/image.png)](https://postimg.org/image/i4olpuxn3/)

```
hydra -L username.txt -P password.txt 192.168.137.144 ssh -t 4
```

Maka OSSEC akan mencatat ada penyerangan dan menambahkan list host yang tidak bisa mengakses server

[![46.png](https://s3.postimg.org/t5jquvpw3/image.png)](https://postimg.org/image/i5yjj9zgv/) 


#E. Kesimpulan dan Saran
IDS(Intrusion Detection System) bisa memberikan peringatan kepada server administrator jika ada kegiatan-kegiatan yang mencurigakan di dalam sistem kita. Hal ini membantu Administrator dalam mengawasi sistem kita agar tidak terjadi hal-hal yang tidak diinginkan. Supaya lebih optimal IDS bisa dikombinasikan dengan Honeypot.