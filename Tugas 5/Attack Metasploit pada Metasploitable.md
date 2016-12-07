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

4. 

#D. Attack Exploit
#E. Analasis Attack
#F. Kesimpulan dan Saran