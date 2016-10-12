#A. Pendahuluan

SQL injection adalah serangan yang memanfaatkan kelalaian dari website yang mengijinkan user untuk menginputkan data tertentu tanpa melakukan filter terhadap malicious character. Inpputan tersebut biasanya di masukkan pada box search atau bagian - bagian tertentu dari website yang berinteraksi dengan database SQL dari situs tersebut. Perintah yang dimasukkan para attacker biasanya adalah sebiah data yang mengandung link tertentu yang mengarahkan para korban ke website khusus yang digunakan para attacker untuk mengambil data pribad korban. Untuk menghindari link berbahaya dari website yang telah terinfeksi serangan SQL injection, dapat menggunakan aplikasi tambahan seerti NoScript yang merupakaan Add-ons untuk aplikasi web browser Firefox.

Untuk uji coba kali ini akan dilakukan pada wordpress(local) dengan beberapa plugin(video player 1.5.18, leaguemanager 4.1.1) dan juga tool uji SQL injection(WPscan, sqlmap). Uji coba akan dilakukan pada sistem operasi Kali Linux.

#B. Dasar Teori

Sesuai dengan penjelasan diatas, pengujian SQL injection akan dilakukan pada sistem operasi Kali Linux. Website yang akan diuji yaitu wordpress yang diinstal pada local dengan beberapa plugin. Piranti yang digunakan untuk uji SQL injection antara lain WPscan, sqlmap dan beberapa tool lainnya. Mengenai piranti yang akan digunakan akan dijelaskan berikut ini :

###1.  Kali Linux

	Kali Linux adalah salah satu distribusi Linux tingkat lanjut untuk Penetration Testing dan audit keamanan. Distro ini dulunya adalah distro Backtrack, yang kemudian memutuskan mengganti nama distronya tersebut menjadi Kali Linux di versi terbarunya. Kali Linux ini akan dijadikan sebagai standarisasi distro Linux yang digunakan untuk percobaan penetrasi.

###2.  Ubuntu Server

	Linux Ubuntu Server adalah system operasi turunan dari Linux Ubuntu yang di desain khusus dengan kernel yang telah dikustomisasi untuk bekerja sebagai system operasi server. Kernel Linux Ubuntu Server di desain khusus untuk bisa bekerja dengan lebih dari satu proses (multiprocessor) dengan dukungan NUMA pada 100Hz internal timer frequency dan menggunakan pennjadwalan deadline I/O. 
    
    Linux Ubuntu Server memiliki lisensi open source dan gratis serta merupakan turunan dari distro linux debian sehingga memiliki keamanan yang cukup tinggi. Linux Ubuntu Server ini mempunyai kebutuhan minimum atau resource yang harus dipenuhi diantaranya adalah processor 300 MHz, Memory 64MB, Harddisk 500MB dan VGA 640×480. Namun untuk meningkatkan kinerja pada computer resource pada computer harus disediakan lebih tinggi.
    
###3.  Oracle VM VirtualBox

	Virtualbox adalah software gratis milik Oracle yang fungsi utamanya adalah mem-visualisasi-kan sebuah atau banyak Sistem Operasi (OS) di dalam Sistem Operasi utama kita. Misalnya anda memiliki sistem operasi windows namun ingin melakukan penelitian pada linux. Untuk menginstalasi dual boot perlu usaha sedikit extra, sedangkan dengan menggunakan VirtualBox, linux anda akan berjalan di dalam windows sehingga anda dapat sekaligus menggunakan windows.

###4.  VMWare Workstation
	
    VMWare Workstation adalah software untuk virtual machine yang compatible dengan komputer Intel x86. Software ini memungkinkan pemakai untuk membuat satu atau lebih virtual machine dan menjalankannya secara serempak. Masing-masing virtual machine dapat menjalankan guest operating system-nya sendiri seperti Linux, Windows, BSD, dan lain-lain. Tetapi software ini tidak dapat menjalankan virtual machine yang dibuat oleh produk VMWare yang lain.


###5.	Wordpress

	WordPress adalah sebuah aplikasi sumber terbuka (open source) yang sangat populer digunakan sebagai mesin blog (blog engine). WordPress dibangun dengan bahasa pemrograman PHP dan basis data (database) MySQL. PHP dan MySQL, keduanya merupakan perangkat lunak sumber terbuka (open source software).Selain sebagai blog, WordPress juga mulai digunakan sebagai sebuah CMS (Content Management System) karena kemampuannya untuk dimodifikasi dan disesuaikan dengan kebutuhan penggunanya. WordPress adalah penerus resmi dari b2/cafelog yang dikembangkan oleh Michel Valdrighi. Nama WordPress diusulkan oleh Christine Selleck, teman Matt Mullenweg. WordPress saat ini menjadi platform content management system (CMS) bagi beberapa situs web ternama seperti CNN, Reuters, The New York Times, TechCrunch, dan lainnya.

	Adapun plugin yang akan diinstal untuk diuji antara lain : video player 1.5.16, leaguemanager 3.9.11, MailPoet Newsletters 2.7.2.

###6.	WPscan

	WPScan adalah scanner keamanan yang memeriksa keamanan WordPress menggunakan metode “black box”. Fitur utama: pencacah username, multithreaded password bruteforcing, pencacah versi plugin WordPress dan pencacahan kerentanan sistem. Jika anda memiliki website menggunakan Wordpress, sangat disarankan untuk menyerang website anda sendiri dan kemudian melakukan perbaikan terhadap website anda sebelum hacker asli yang melakukannya.

###7.	sqlmap

	sqlmap adalah tools opensource yang mendeteksi dan melakukan exploit pada bug SQL injection secara otomatis. Dengan melakukan serangan SQL injection seorang attacker dapat mengambil alih serta memanipulasi sebuah database di dalam sebuah server.

#C. Instalasi Wordpress pada Ubuntu Server

1. Update Ubuntu Server
	Pastikan ubuntu server yang akan digunakan untuk menginstall telah terupdate dengan menggunakan syntax
    
    `sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get autoremove`
    
    [![1.png](https://s12.postimg.org/5q2xee01p/image.png)](https://postimg.org/image/vlmnxl1vd/)
    
2. Install Apache2
	Install apache2 sebagai web server sehingga client dapat mengakses wordpress melalui web browser
    
    `sudo apt-get install apache2`
    
    [![2.png](https://s12.postimg.org/76efwj2yl/image.png)](https://postimg.org/image/9aysxm4l5/)
    
    [![3.png](https://s12.postimg.org/xfzifbovx/image.png)](https://postimg.org/image/kbty2mwu1/)
    
3. Install MySql
	Install mySql sebagai database untuk menyimpah data yang dimiliki oleh wordpress
    
    `sudo apt-get install mysql-server mysql-client`
    
    [![4.png](https://s12.postimg.org/bi31lj9vh/image.png)](https://postimg.org/image/ckd842sop/)
    
    [![6.png](https://s12.postimg.org/gjafmwhbx/image.png)](https://postimg.org/image/erhgrzxyx/)
    
4. Konfigurasi MySql
	Setelah dilakukan penginstalan mySql dibutuhkan pengaturan mySql dengan cara sebagai berikut
    
    `sudo mysql_secure_installation`
    
    [![8.png](https://s12.postimg.org/q6dxwmabh/image.png)](https://postimg.org/image/71aomuvnd/)
    
    Ketika ada pertanyaan mengenai pengaturan yang ada, ikuti pengaturan seperti dibawah ini

	-Enter current password for root (enter for none): Type root password
    
    [![10.png](https://s12.postimg.org/cdzj0zjjx/image.png)](https://postimg.org/image/kw8z5bq2h/)
    
	-Change the root password? **N**
	-Remove anonymous users? **Y**
    
    [![11.png](https://s12.postimg.org/f9h7llcxp/image.png)](https://postimg.org/image/3kd7xmlyx/)
    
	-Disallow root login remotely? **Y**
    
    [![12.png](https://s12.postimg.org/h2k49wy4d/image.png)](https://postimg.org/image/uw8gyyqpl/)
    
	-Remove test database and access to it? **Y**
    
    [![13.png](https://s12.postimg.org/xeu5zncfx/image.png)](https://postimg.org/image/s3f9exqd5/)
    
	-Reload privilege tables now? **Y**
    
5. Konfigurasi Database
	Setelah dilakukan konfigurasi pada mySql maka dibutuhkan konfigurasi database dengan cara sebagai berikut
    
    `mysql -u root -p`
    
    [![23.png](https://s12.postimg.org/dx43xg4vx/image.png)](https://postimg.org/image/aq9kdtkft/)
    
    Buat database dengan nama **wpdb**;
    
    `CREATE DATABASE wpdb`
    
    [![24.png](https://s12.postimg.org/kouj0atvh/image.png)](https://postimg.org/image/3obmrmgu1/)
    
    Membuat pengguna database dengan nama **wpuser**
    
    `CREATE USER wpuser@localhost IDENTIFIED BY 'new_password_here';`
    
    [![25.png](https://s12.postimg.org/porz88zi5/image.png)](https://postimg.org/image/qr25qsibd/)
    
    Lalu buat hak akses terhadap user yang baru saja dibuat
    
    `GRANT ALL ON wpdb.* to wpuser@localhost;`
    
    [![26.png](https://s12.postimg.org/7n8uag5h9/image.png)](https://postimg.org/image/clwcoz9a1/)
    
    Terakhir jalankan command agar memperbaharui pengaturan database
    
    `FLUSH PRIVILEGES;`
    
    [![27.png](https://s12.postimg.org/tnp6r2o59/image.png)](https://postimg.org/image/slf08j5bt/)
    
    `EXIT`
    
6. Install php dan plugin
	Install php terlebih dahulu
    
    `sudo apt-get install php5 libapache2-mod-php5`
    
    [![14.png](https://s12.postimg.org/b46azof5p/image.png)](https://postimg.org/image/8zlxyldix/)
    
    Lalu jalankan command dibawah untuk menginstall plugin untuk php5
    
    `sudo apt-get install php5 libapache2-mod-php5 php5-mysql php5-curl php5-gd php5-intl php-pear php5-imagick php5-imap php5-mcrypt php5-memcache php5-ming php5-ps php5-pspell php5-recode php5-sqlite php5-tidy php5-xmlrpc php5-xsl`
    
    [![16.png](https://s12.postimg.org/4g9pd2vnh/image.png)](https://postimg.org/image/ltjzrxqyh/)
    
7. Install Wordpress
	Jalankan command dibawah untuk mendapatkan wordpress terbaru
    
    `cd /tmp/ && wget http://wordpress.org/latest.tar.gz`
    
    Extract file yang baru saja didownload
    
    `tar -xvzf latest.tar.gz`
    
    Agar pengguna baru tidak bingung dengan tampilan index maka diharapkan user untuk mengahpus index.html
    
    `sudo rm /var/www/html/index.html`
    
    Lalu copy semua file yang telah diextract tadi ke dalam folder web server
    
    `sudo mv wordpress/* /var/www/html/`
    
    Copy pengaturan wp-config yang telah ada
    
    `sudo cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php`
    
8. Konfigurasi wp-config
	Setelah dilakukan instalasi wordpress maka diperlukan konfigurasi pada wordpress agar terkoneksi dengan database server
    
    `sudo vi /var/www/html/wp-config.php`
    
    Ubah konfigurasi agar seperti gambar dibawah
    
9. Konfigurasi Permission Folder
	Terakhir adalah merubah permission folder wordpress agar dapat dilakukan perubahan data
    
    `sudo chown -R www-data:www-data /var/www/html/`
    `sudo chmod -R 755 /var/www/html/`
    
    Lalu restart webserver apache2
    
    `service restrart apache2`
    
10. Konfigurasi Wordpress melalui Browser

#D. Instalasi Wordpress pada Kali Linux

1. Instalasi XAMPP

	Untuk menjalankan Wordpress dibutuhkan sebuah webserver. Webserver yang akan digunakan disini adalah XAMPP karena telah mengandung SQL Server sebagai database server. Adapun langkah - langkah yang perlu dilakukan untuk instalasi XAMMPP antara lain :

		1. Download XAMPP
			Download XAMPP pada www.apachefriends.org/download.html. Download versi terbaru dari XAMPP untuk linux pada halaman tersebut.

			<Gambar : install XAMPP\1>

		2. Chmod Installer
			Ubah permission file installer dengan cara mengetikkan command berikut pada terminal.

			chmod +x xampp-linux-x64-7.0.9-1-installer.run

			<Gambar : install XAMPP\2>

		3. Run Installer
			Run installer XAMPP dengan cara mengetikkan command berikut pada terminal.

			./xampp-linux-x64-7.0.9-1-installer.run

			<Gambar : install XAMPP\3>

		4. Proses Instalasi
			Ikuti petunjuk instalasi yang tersedia dengan mengklik next.

			<Gambar : install XAMPP\4>

			<Gambar : install XAMPP\5>

			<Gambar : install XAMPP\6>

			<Gambar : install XAMPP\7>

			<Gambar : install XAMPP\8>

		5. Jalankan semua server
			Setelah XAMPP berhasil terinstall maka akan muncul UI XAMPP. Jalankan semua server dengan mengklik Start All pada tab Manage Servers

			<Gambar : install XAMPP\9>

2. Instalasi Wordpress
	
	Sebelum instalasi wordpress kita perlu menyiapkan database yang akan digunakan untuk wordpress tersebut. Selain itu kita perlu menyiapkan file wordpress yang akan diinstall. Adapun langkah - langkah installasinya adalah sebagai berikut :

	1. Download Wordpress
		Download wordpress dengan format .zip pada 

		https://wordpress.org/download/

		<Gambar : install Wordpress\1>

	2. Persiapkan Database
		Buka localhost/phpmyadmin pada browser kemudian klik new. Isikan nama database sesuai yang diinginkan. Disini database akan dinamai dengan nama "wp". Kemudian klik go.

		<Gambar : install Wordpress\2>

		<Gambar : install Wordpress\3>

	3. Persiapan Instalasi
		Pindahkan file installer wordpress(.zip) pada folder Download ke /opt/lampp/htdocs. Kemudian extract file .zip tersebut.

		<Gambar : install Wordpress\4>

	4. Mulai Instalasi
		Buka localhost/wordpress pada browser. Kemudian klik let's go.

		<Gambar : install Wordpress\5>

	5. Melakukan Koneksi dengan Database
		Setelah mengklik let's go, anda akan dimintai database yang akan digunakan pada wordpress ini. Isikan form sesuai dengan database yang telah dibuat. Password dapat dikosongkan jika memang tidak terdapat password pada database.

		<Gambar : install Wordpress\6>

	6. Wp-Config
		Jika diminta membuat file wp-config.php, copykan text yang disediakan kemudian buat file baru pada /opt/lampp/htdocs/wordpress dengan nama wp-config.php . Setelah selesai klik "Run the install".

		<Gambar : install Wordpress\7>

		<Gambar : install Wordpress\8>

	7. Site Informastion
		Setelah itu isikan form Informasi mengenai site wordpress anda. Kemudian klik "Install WorPress".

		<Gambar : install Wordpress\9>

	8. Install Success!
		Ketika Instalasi selesai akan menampilkan halaman seperti berikut :

		<Gambar : install Wordpress\10>

		Kemudian anda bisa langsung mengakses dashboard dengan login sesuai username dan password yang telah diisikan tadi.

		<Gambar : install Wordpress\11>

3. Instalasi Plugin
	Plugin yang akan diuji disini antara lain Worpress Video Player v1.5.18, LeagueManager v4.1.1, ... ,... . Cara instalasi plugin semua sama pada wordpress. Adapun cara instalasi pluginnya yaitu :

	1. Download Plugin 
		Untuk plugin video player 1.5.18 dapat di download di :

		https://wordpress.org/plugins/player/

		<Gambar : install plugin\1>

		Untuk plugin LeagueManage 4.1.1 dapat di download di :

		https://wordpress.org/plugins/leaguemanager/

		<Gambar : install plugin\6>

	2. Instalasi
		Untuk memulai install plugin, buka dashboard wordpress kemudian klik Plugins - Add New.

		<Gambar : install plugin\2>

		Kemudian klik Upload Plugin

		<Gambar : install plugin\3>

	3. Pilih plugin
		Pilih plugin yang akan diinstal pada directory Downloads. Instalasi plugin sebaiknya dilakukan satu per satu.

		<Gambar : install plugin\4>

		<Gambar : install plugin\9>

		Kemudian klik Install Now

	4. Finish Install
		Ketika selesai instalasi klik Activate Plugin.

		<Gambar : install plugin\5>

		<Gambar : install plugin\10>

	5. Lakukan langkah yang sama untuk semua Plugin yang ingin diinstal

4. Instalasi Tool SQL Injection
	
	Karena sistem operasi yang digunakan adalah Kali Linux, maka sqlmap dan WPscan telah terinstall. Untuk masing - masing tool mungkin diperlukan update database dari tool tersebut. Update akan dilakukan secara otomatis ketika kita menjalankan perintah pada tool tersebut.

#E. Uji SQL Injection
	
	1. Pengujian dengan WPscan

		Adapun uji yang akan dilakukan adalah fullscan wordpress, mencari username dari wordpress tersebut, mencoba brute force password dan mencari plugin yang vulnerable.

		Hasil Pengujian :

		a. Fullscan Wordpress
			Fullscan dilakukan dengan command.

			wpscan --url localhost/wordpress

			Hasil :

			<Gambar : hasil uji WP Scan\1>

			<Gambar : hasil uji WP Scan\2>

			<Gambar : hasil uji WP Scan\3>

		b. Mencari Username
			Untuk scanning username dilakukan dengan command.

			wpscan --url localhost/wordpress --enumerate u

			Hasil :

			<Gambar : hasil uji WP Scan\4>

		c. Brute Force password 
			Untuk melakukan brute force password, terlebih dahulu buatlah file yang berisikan list password yang kira - kira merupakan password user wordpress dengan cara :

			nano password.txt

			<Gambar : hasil uji WP Scan\5>

			Kemudian isikan list password perkiraan.

			<Gambar : hasil uji WP Scan\6>

			Setelah file password disiapkan, kemudian ketikkan command berikut :

			wpscan --url localhost/wordpress --wordlist ~/password.txt --thread 10

			<Gambar : hasil uji WP Scan\7>

			Hasil :

			<Gambar : hasil uji WP Scan\8>

			Jika ada password yang cocok maka bagian password akan terisi seperti gambar diatas.

		d. Scan Vulnerable Plugin
			Untuk melakukan scan pada plugin hanya perlu dilakukan dengan mengtikkan command berikut :

			wpscan --url localhost/wordpress --enumerate p

			<Gambar : hasil uji WP Scan\9>

			Hasil :

			<Gambar : hasil uji WP Scan\10>

			<Gambar : hasil uji WP Scan\11>

			Nama plugin yang terdapat tanda seru berwarna merahnya merupakan plugin yang vulnerable.


#F. Kesimpulan dan Saran



