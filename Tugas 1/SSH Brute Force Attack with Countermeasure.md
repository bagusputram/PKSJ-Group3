# A. Pendahuluan

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

## Langkah Uji Penetrasi dengan SSH Brute Force Tools

# D. Uji Penetrasi 2

### 1. Langkah Konfigurasi DenyHosts

### 2. Langkah Konfigurasi SSH Server

### 3. Langkah Uji Penetrasi dengan SSH Brute Force Tools

# E. Kesimpulan dan Saran