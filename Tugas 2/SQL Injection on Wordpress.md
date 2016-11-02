#A. Pendahuluan

SQL injection adalah serangan yang memanfaatkan kelalaian dari website yang mengijinkan user untuk menginputkan data tertentu tanpa melakukan filter terhadap malicious character. Inpputan tersebut biasanya di masukkan pada box search atau bagian - bagian tertentu dari website yang berinteraksi dengan database SQL dari situs tersebut. Perintah yang dimasukkan para attacker biasanya adalah sebiah data yang mengandung link tertentu yang mengarahkan para korban ke website khusus yang digunakan para attacker untuk mengambil data pribad korban. Untuk menghindari link berbahaya dari website yang telah terinfeksi serangan SQL injection, dapat menggunakan aplikasi tambahan seerti NoScript yang merupakaan Add-ons untuk aplikasi web browser Firefox.

Untuk uji coba kali ini akan dilakukan pada wordpress(local) dengan beberapa plugin(video player 1.5.18, leaguemanager 4.1.1) dan juga tool uji SQL injection(WPscan, sqlmap). Uji coba akan dilakukan pada sistem operasi Kali Linux.

#B. Dasar Teori

Sesuai dengan penjelasan diatas, pengujian SQL injection akan dilakukan pada sistem operasi Kali Linux. Website yang akan diuji yaitu wordpress yang diinstal pada local dengan beberapa plugin. Piranti yang digunakan untuk uji SQL injection antara lain WPscan, sqlmap dan beberapa tool lainnya. Mengenai piranti yang akan digunakan akan dijelaskan berikut ini :

1.  Kali Linux

	Kali Linux adalah salah satu distribusi Linux tingkat lanjut untuk Penetration Testing dan audit keamanan. Distro ini dulunya adalah distro Backtrack, yang kemudian memutuskan mengganti nama distronya tersebut menjadi Kali Linux di versi terbarunya. Kali Linux ini akan dijadikan sebagai standarisasi distro Linux yang digunakan untuk percobaan penetrasi.

2.  Ubuntu Server

	Linux Ubuntu Server adalah system operasi turunan dari Linux Ubuntu yang di desain khusus dengan kernel yang telah dikustomisasi untuk bekerja sebagai system operasi server. Kernel Linux Ubuntu Server di desain khusus untuk bisa bekerja dengan lebih dari satu proses (multiprocessor) dengan dukungan NUMA pada 100Hz internal timer frequency dan menggunakan pennjadwalan deadline I/O.

	Linux Ubuntu Server memiliki lisensi open source dan gratis serta merupakan turunan dari distro linux debian sehingga memiliki keamanan yang cukup tinggi. Linux Ubuntu Server ini mempunyai kebutuhan minimum atau resource yang harus dipenuhi diantaranya adalah processor 300 MHz, Memory 64MB, Harddisk 500MB dan VGA 640×480. Namun untuk meningkatkan kinerja pada computer resource pada computer harus disediakan lebih tinggi.

3.  Oracle VM VirtualBox

	Virtualbox adalah software gratis milik Oracle yang fungsi utamanya adalah mem-visualisasi-kan sebuah atau banyak Sistem Operasi (OS) di dalam Sistem Operasi utama kita. Misalnya anda memiliki sistem operasi windows namun ingin melakukan penelitian pada linux. Untuk menginstalasi dual boot perlu usaha sedikit extra, sedangkan dengan menggunakan VirtualBox, linux anda akan berjalan di dalam windows sehingga anda dapat sekaligus menggunakan windows.

4.  VMWare Workstation 
	
    VMWare Workstation adalah software untuk virtual machine yang compatible dengan komputer Intel x86. Software ini memungkinkan pemakai untuk membuat satu atau lebih virtual machine dan menjalankannya secara serempak. Masing-masing virtual machine dapat menjalankan guest operating system-nya sendiri seperti Linux, Windows, BSD, dan lain-lain. Tetapi software ini tidak dapat menjalankan virtual machine yang dibuat oleh produk VMWare yang lain.

5. Wordpress

	WordPress adalah sebuah aplikasi sumber terbuka (open source) yang sangat populer digunakan sebagai mesin blog (blog engine). WordPress dibangun dengan bahasa pemrograman PHP dan basis data (database) MySQL. PHP dan MySQL, keduanya merupakan perangkat lunak sumber terbuka (open source software).Selain sebagai blog, WordPress juga mulai digunakan sebagai sebuah CMS (Content Management System) karena kemampuannya untuk dimodifikasi dan disesuaikan dengan kebutuhan penggunanya. WordPress adalah penerus resmi dari b2/cafelog yang dikembangkan oleh Michel Valdrighi. Nama WordPress diusulkan oleh Christine Selleck, teman Matt Mullenweg. WordPress saat ini menjadi platform content management system (CMS) bagi beberapa situs web ternama seperti CNN, Reuters, The New York Times, TechCrunch, dan lainnya.

	Adapun plugin yang akan diinstal untuk diuji antara lain : video player 1.5.16, leaguemanager 3.9.11, MailPoet Newsletters 2.7.2.

6.	WPscan

	WPScan adalah scanner keamanan yang memeriksa keamanan WordPress menggunakan metode “black box”. Fitur utama: pencacah username, multithreaded password bruteforcing, pencacah versi plugin WordPress dan pencacahan kerentanan sistem. Jika anda memiliki website menggunakan Wordpress, sangat disarankan untuk menyerang website anda sendiri dan kemudian melakukan perbaikan terhadap website anda sebelum hacker asli yang melakukannya.

7.	sqlmap

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
    
    [![18.png](https://s12.postimg.org/7cwqdd1h9/image.png)](https://postimg.org/image/uedbj414p/)
    
    [![19.png](https://s12.postimg.org/w7g87fmbh/image.png)](https://postimg.org/image/yc0l8iny1/)
    
    Extract file yang baru saja didownload
    
    `tar -xvzf latest.tar.gz`
    
    [![20.png](https://s12.postimg.org/cqvikwr7h/image.png)](https://postimg.org/image/5aw8z43i1/)
    
    [![21.png](https://s12.postimg.org/t3a5oduwt/image.png)](https://postimg.org/image/q970axsqh/)
    
    Agar pengguna baru tidak bingung dengan tampilan index maka diharapkan user untuk mengahpus index.html
    
    `sudo rm /var/www/html/index.html`
    
    Lalu copy semua file yang telah diextract tadi ke dalam folder web server
    
    `sudo mv wordpress/* /var/www/html/`
    
    [![22.png](https://s12.postimg.org/75doulfwd/image.png)](https://postimg.org/image/e8lka7lbt/)
    
    Copy pengaturan wp-config yang telah ada
    
    `sudo cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php`
    
    [![28.png](https://s12.postimg.org/r7ndd862l/image.png)](https://postimg.org/image/j25bf2htl/)
    
8. Konfigurasi wp-config
	Setelah dilakukan instalasi wordpress maka diperlukan konfigurasi pada wordpress agar terkoneksi dengan database server
    
    `sudo vi /var/www/html/wp-config.php`
    
    Ubah konfigurasi agar seperti gambar dibawah
    
    [![29.png](https://s12.postimg.org/oeu5t75q5/image.png)](https://postimg.org/image/zefd4sw55/)
    
9. Konfigurasi Permission Folder
	Terakhir adalah merubah permission folder wordpress agar dapat dilakukan perubahan data
    
    `sudo chown -R www-data:www-data /var/www/html/`
    
    [![30.png](https://s12.postimg.org/y0nq9hwvx/image.png)](https://postimg.org/image/jhgl833qx/)
    
    `sudo chmod -R 755 /var/www/html/`
    
    [![31.png](https://s12.postimg.org/u5oxko33x/image.png)](https://postimg.org/image/6rgy8ql6h/)
    
    Lalu restart webserver apache2
    
    `service restrart apache2`
    
10. Konfigurasi Wordpress melalui Browser
	Buka browser pada client lalu akses ip dari web server yang telah terinstall wordpress
    
    [![33.png](https://s12.postimg.org/64i1j7oal/image.png)](https://postimg.org/image/ci74mgt6h/)
    
    [![34.png](https://s12.postimg.org/lr9awl22l/image.png)](https://postimg.org/image/vbsxjgreh/)
    
    [![35.png](https://s12.postimg.org/5hj4torel/image.png)](https://postimg.org/image/lfrujtlmh/)
    
    Setelah melakukan instalasi awal maka pengguna dapat mengakses dashboard dari wordpress
    
    [![36.png](https://s12.postimg.org/rhzhaba2l/image.png)](https://postimg.org/image/ahgl1mx15/)
    
    [![37.png](https://s12.postimg.org/pep22na9p/image.png)](https://postimg.org/image/bxs3jrzy1/)

#D. Instalasi Wordpress pada Kali Linux

1. Instalasi XAMPP

	Untuk menjalankan Wordpress dibutuhkan sebuah webserver. Webserver yang akan digunakan disini adalah XAMPP karena telah mengandung SQL Server sebagai database server. Adapun langkah - langkah yang perlu dilakukan untuk instalasi XAMMPP antara lain :

	1. Download XAMPP
		Download XAMPP pada www.apachefriends.org/download.html. Download versi terbaru dari XAMPP untuk linux pada halaman tersebut.

		[![1. download XAMPP.png](https://s14.postimg.org/quscjmqtd/1_download_XAMPP.png)](https://postimg.org/image/5l4q8sail/)

	2. Chmod Installer
		Ubah permission file installer dengan cara mengetikkan command berikut pada terminal.

		'chmod +x xampp-linux-x64-7.0.9-1-installer.run'

		[![2. chmod installer XAMPP.png](https://s9.postimg.org/5uttl9o3z/2_chmod_installer_XAMPP.png)](https://postimg.org/image/r4hfw44ej/)

	3. Run Installer
		Run installer XAMPP dengan cara mengetikkan command berikut pada terminal.

		./xampp-linux-x64-7.0.9-1-installer.run

		[![3. install XAMPP.png](https://s15.postimg.org/bnsft2xq3/3_install_XAMPP.png)](https://postimg.org/image/kita3lmif/)

	4. Proses Instalasi
		Ikuti petunjuk instalasi yang tersedia dengan mengklik next.

		[![4. Install XAMPP progress.png](https://s21.postimg.org/l3ep22w6f/4_Install_XAMPP_progress.png)](https://postimg.org/image/atca2u6ar/)
		
        [![5. Install XAMPP progress 1.png](https://s17.postimg.org/k3t4iqfkf/5_Install_XAMPP_progress_1.png)](https://postimg.org/image/u145bsn63/)
		
        [![6. Install XAMPP progress 2.png](https://s21.postimg.org/ruggpsa2v/6_Install_XAMPP_progress_2.png)](https://postimg.org/image/jc70lg3k3/)
		
        [![7. Install XAMPP progress 3.png](https://s18.postimg.org/7ap7lram1/7_Install_XAMPP_progress_3.png)](https://postimg.org/image/hkrml00hh/)

		[![8. Install selesai.png](https://s16.postimg.org/q0jpv54qt/8_Install_selesai.png)](https://postimg.org/image/gsrhefxoh/)

	5. Jalankan semua server
		Setelah XAMPP berhasil terinstall maka akan muncul UI XAMPP. Jalankan semua server dengan mengklik Start All pada tab Manage Servers

		[![9. Aktifkan semua server XAMPP.png](https://s21.postimg.org/3t4ool0pz/9_Aktifkan_semua_server_XAMPP.png)](https://postimg.org/image/lvxrfswkj/)

2. Instalasi Wordpress
	
	Sebelum instalasi wordpress kita perlu menyiapkan database yang akan digunakan untuk wordpress tersebut. Selain itu kita perlu menyiapkan file wordpress yang akan diinstall. Adapun langkah - langkah installasinya adalah sebagai berikut :

	1. Download Wordpress
		Download wordpress dengan format .zip pada https://wordpress.org/download/

		[![1. download wordpress.png](https://s22.postimg.org/7doo2aqs1/1_download_wordpress.png)](https://postimg.org/image/m9n79w26l/)

	2. Persiapkan Database
		Buka localhost/phpmyadmin pada browser kemudian klik new. Isikan nama database sesuai yang diinginkan. Disini database akan dinamai dengan nama "wp". Kemudian klik go.

		[![2. Persiapan Database.png](https://s18.postimg.org/o2m8on6gp/2_Persiapan_Database.png)](https://postimg.org/image/fkcskazxx/)
		
        [![3. Database telah siap.png](https://s18.postimg.org/5yl7kluah/3_Database_telah_siap.png)](https://postimg.org/image/3u0ujisnp/)

	3. Persiapan Instalasi
		Pindahkan file installer wordpress(.zip) pada folder Download ke /opt/lampp/htdocs. Kemudian extract file .zip tersebut.

		[![4. Pindahkan file worpress ke opt lampp htdocs d.png](https://s13.postimg.org/gs7ktrt3b/4_Pindahkan_file_worpress_ke_opt_lampp_htdocs_d.png)](https://postimg.org/image/6uwk0plhf/)

	4. Mulai Instalasi
		Buka localhost/wordpress pada browser. Kemudian klik let's go.

		[![5. pada browser buka localhost wordpress.png](https://s14.postimg.org/lm6yw26i9/5_pada_browser_buka_localhost_wordpress.png)](https://postimg.org/image/trp0u7ur1/)

	5. Melakukan Koneksi dengan Database
		Setelah mengklik let's go, anda akan dimintai database yang akan digunakan pada wordpress ini. Isikan form sesuai dengan database yang telah dibuat. Password dapat dikosongkan jika memang tidak terdapat password pada database.

		[![6. Koneksi dengan database.png](https://s17.postimg.org/j66pkn7sv/6_Koneksi_dengan_database.png)](https://postimg.org/image/7tu42uz3v/)

	6. Wp-Config
		Jika diminta membuat file wp-config.php, copykan text yang disediakan kemudian buat file baru pada /opt/lampp/htdocs/wordpress dengan nama wp-config.php . Setelah selesai klik "Run the install".

		[![7. membuat file wp-config php.png](https://s12.postimg.org/9qlnhyc2l/7_membuat_file_wp_config_php.png)](https://postimg.org/image/f20k2ny55/)
		
        [![8. wp-config.png](https://s18.postimg.org/8nhh161ll/8_wp_config.png)](https://postimg.org/image/8aq2uzjbp/)

	7. Site Informastion
		Setelah itu isikan form Informasi mengenai site wordpress anda. Kemudian klik "Install WorPress".

		[![9. wordpress install info.png](https://s13.postimg.org/bd7lnpgef/9_wordpress_install_info.png)](https://postimg.org/image/49zq83ayr/)

	8. Install Success!
		Ketika Instalasi selesai akan menampilkan halaman seperti berikut :

		[![10. install berhasil.png](https://s10.postimg.org/noj7oe6qh/10_install_berhasil.png)](https://postimg.org/image/g8jy2lj11/)

		Kemudian anda bisa langsung mengakses dashboard dengan login sesuai username dan password yang telah diisikan tadi.

		[![11. tampilan dashboard wordpress.png](https://s16.postimg.org/j03j7xd9h/11_tampilan_dashboard_wordpress.png)](https://postimg.org/image/xjao9c6e9/)

3. Instalasi Plugin
	Plugin yang akan diuji disini antara lain Worpress Video Player v1.5.18, LeagueManager v4.1.1, ... ,... . Cara instalasi plugin semua sama pada wordpress. Adapun cara instalasi pluginnya yaitu :

	1. Download Plugin 
		Untuk plugin video player 1.5.18 dapat di download di : https://wordpress.org/plugins/player/

		[![1. download video player.png](https://s21.postimg.org/amdb9vqif/1_download_video_player.png)](https://postimg.org/image/60h71j4z7/)

		Untuk plugin LeagueManage 4.1.1 dapat di download di : https://wordpress.org/plugins/leaguemanager/

		[![6. plugin 2.png](https://s18.postimg.org/f824k0ifd/6_plugin_2.png)](https://postimg.org/image/609w3bbd1/)

	2. Instalasi
		Untuk memulai install plugin, buka dashboard wordpress kemudian klik Plugins - Add New.

		[![2. buka dashboard plugin add new.png](https://s3.postimg.org/dv3il64oz/2_buka_dashboard_plugin_add_new.png)](https://postimg.org/image/kybe0sa4f/)

		Kemudian klik Upload Plugin

		[![3. upload plugin.png](https://s14.postimg.org/9sbzq77mp/3_upload_plugin.png)](https://postimg.org/image/w49sjl6ql/)

	3. Pilih plugin
		Pilih plugin yang akan diinstal pada directory Downloads. Instalasi plugin sebaiknya dilakukan satu per satu.

		[![4. pilih plugin.png](https://s18.postimg.org/68ic696vt/4_pilih_plugin.png)](https://postimg.org/image/nlsml426t/)

		[![9. pilih plugin.png](https://s16.postimg.org/ujimuqmj9/9_pilih_plugin.png)](https://postimg.org/image/4b7i5d2fl/)

		Kemudian klik Install Now

	4. Finish Install
		Ketika selesai instalasi klik Activate Plugin.

		[![5. activate plugin.png](https://s15.postimg.org/47b0s4uxn/5_activate_plugin.png)](https://postimg.org/image/t0kkssdxz/)

		[![10. activate plugin.png](https://s14.postimg.org/fv2lhnv69/10_activate_plugin.png)](https://postimg.org/image/vgjx1m74d/)

	5. Lakukan langkah yang sama untuk semua Plugin yang ingin diinstal

4. Instalasi Tool SQL Injection
	
	Karena sistem operasi yang digunakan adalah Kali Linux, maka sqlmap dan WPscan telah terinstall. Untuk masing - masing tool mungkin diperlukan update database dari tool tersebut. Update akan dilakukan secara otomatis ketika kita menjalankan perintah pada tool tersebut.

#E. Instalasi Plugin pada Wordpress Ubuntu Server

1. Leagumanager 3.9.11
	
    Buka folder plugin pada wordpress terlebih dahulu
    
    `cd /var/www/html/wp-content/plugins`
    
	[![40.png](https://s12.postimg.org/fl7upu859/image.png)](https://postimg.org/image/cedb67np5/)
    
    Download plugin dengan command dibawah
    
    `sudo wget http://downloads.wordpress.org/plugin/leaguemanager.3.9.1.1.zip`
    
    [![41.png](https://s12.postimg.org/5pbd3xrr1/image.png)](https://postimg.org/image/gowkfji61/)
    
    Lalu extract file yang telah didownload tersebut
    
    `sudo unzip leaguemanager.3.9.1.1.zip`
    
    [![43.png](https://s12.postimg.org/6u5f9be7x/image.png)](https://postimg.org/image/4cto21ubd/)
    
    Aktifkan plugin pada menu add plugin didalam dashboard pengguna
    
    [![44.png](https://s12.postimg.org/pnr86bcfx/image.png)](https://postimg.org/image/6inywjxrt/)
    
2. Video Player 1.5.16
	
    Buka folder plugin pada wordpress terlebih dahulu
    
    `cd /var/www/html/wp-content/plugins`
    
    [![40.png](https://s12.postimg.org/fl7upu859/image.png)](https://postimg.org/image/cedb67np5/)
	
    Download plugin dengan command dibawah
    
    `sudo wget http://downloads.wordpress.org/plugin/player.1.5.16.zip`
    
    [![45.png](https://s12.postimg.org/4fdjovxz1/image.png)](https://postimg.org/image/dzx6brnax/)
    
    Lalu extract file yang telah didownload tersebut
    
    `sudo unzip player.1.5.16.zip`
    
    [![46.png](https://s12.postimg.org/5ixo0uim5/image.png)](https://postimg.org/image/hxkg16a49/)
    
    Aktifkan plugin pada menu add plugin didalam dashboard pengguna
    
    [![47.png](https://s12.postimg.org/m7z3wrf7h/image.png)](https://postimg.org/image/uq8k13lq1/)
    
3. MailPoet Newsletters 2.7.2
		
    Buka folder plugin pada wordpress terlebih dahulu
    
    `cd /var/www/html/wp-content/plugins`
    
	[![40.png](https://s12.postimg.org/fl7upu859/image.png)](https://postimg.org/image/cedb67np5/)
    
    Download plugin dengan command dibawah
    
    `sudo wget http://downloads.wordpress.org/plugin/wysija-newsletters.2.7.2.zip`
    
    [![48.png](https://s12.postimg.org/jf5wcqev1/image.png)](https://postimg.org/image/sa6qn93nd/)
    
    Lalu extract file yang telah didownload tersebut
    
    `sudo unzip wysija-newsletters.2.7.2.zip`
    
    Aktifkan plugin pada menu add plugin didalam dashboard pengguna
    
    [![50.png](https://s12.postimg.org/5o1faipx9/image.png)](https://postimg.org/image/97nd0bsmx/)
    

#F. Uji SQL Injection
	
1. Pengujian dengan WPscan

	Adapun uji yang akan dilakukan adalah fullscan wordpress, mencari username dari wordpress tersebut, mencoba brute force password dan mencari plugin yang vulnerable.

	Hasil Pengujian :

	- Fullscan Wordpress
		Fullscan dilakukan dengan command.

		wpscan --url localhost/wordpress

		Hasil :

		[![1. Scan full 1.png](https://s16.postimg.org/hbwcecypx/1_Scan_full_1.png)](https://postimg.org/image/qjokv25s1/)
		
        [![2. Scan full 2.png](https://s21.postimg.org/4kiq1za8n/2_Scan_full_2.png)](https://postimg.org/image/of4ro3pg3/)
		
        [![3. Scan full 3.png](https://s12.postimg.org/8cmnul7fh/3_Scan_full_3.png)](https://postimg.org/image/e0sylhbrt/)

	- Mencari Username
		Untuk scanning username dilakukan dengan command.

		wpscan --url localhost/wordpress --enumerate u

		Hasil :

		[![4. Scan Username.png](https://s18.postimg.org/5earvnqft/4_Scan_Username.png)](https://postimg.org/image/4orzjapw5/)

	- Brute Force password 
		Untuk melakukan brute force password, terlebih dahulu buatlah file yang berisikan list password yang kira - kira merupakan password user wordpress dengan cara :

		nano password.txt

		[![5. buat list password.png](https://s12.postimg.org/w55t3dj7h/5_buat_list_password.png)](https://postimg.org/image/dplc5z52x/)

		Kemudian isikan list password perkiraan.

		[![6. buat list password 2.png](https://s12.postimg.org/sfr6338gt/6_buat_list_password_2.png)](https://postimg.org/image/ux2xacsd5/)

		Setelah file password disiapkan, kemudian ketikkan command berikut :

		wpscan --url localhost/wordpress --wordlist ~/password.txt --thread 10

		[![7. brute force password pada seluruh username ya.png](https://s11.postimg.org/3v9va01n7/7_brute_force_password_pada_seluruh_username_ya.png)](https://postimg.org/image/4xk1sjkgf/)

		Hasil :

		[![8. password ditemukan.png](https://s4.postimg.org/am7hfkcv1/8_password_ditemukan.png)](https://postimg.org/image/7s4c24aop/)

		Jika ada password yang cocok maka bagian password akan terisi seperti gambar diatas.

	- Scan Vulnerable Plugin
		Untuk melakukan scan pada plugin hanya perlu dilakukan dengan mengtikkan command berikut :

		wpscan --url localhost/wordpress --enumerate p

		[![9. scan plugin.png](https://s22.postimg.org/xn8utqav5/9_scan_plugin.png)](https://postimg.org/image/726by68hp/)

		Hasil :

		[![10. hasil plugin.png](https://s9.postimg.org/g26flal6n/10_hasil_plugin.png)](https://postimg.org/image/z79ov1zuj/)
		
        [![11. hasil plugin 2.png](https://s21.postimg.org/bjzybfph3/11_hasil_plugin_2.png)](https://postimg.org/image/in7tr1uwj/)

		Nama plugin yang terdapat tanda seru berwarna merahnya merupakan plugin yang vulnerable.

2. Pengujian dengan SQLMAP
 Melakukan sql injection menggunakan sqlmap kepada beberapa plugin yang vulnerable pada wordpress
 a. Leaguemanager 3.9.1.1
 - command sqlmap untuk leaguemanager
 [![1.png](https://s5.postimg.org/ujykeztc7/image.png)](https://postimg.org/image/ii36kuk3n/)
 ketik enter untuk menjalankan perintah di atas.
 - Hasil setelah melakukan perintah di atas
 [![2.png](https://s5.postimg.org/5f7k1ktvr/image.png)](https://postimg.org/image/770iwhd8j/)
 - Mengecek database setelah berhasil melakukan injection
 [![16.png](https://s5.postimg.org/djpbh6c07/image.png)](https://postimg.org/image/j7vm82gcj/)
 jalankan perintah di atas
 [![17.png](https://s5.postimg.org/gf2eo1g07/image.png)](https://postimg.org/image/ae4pqytdv/)
 hasil dari perintah di atas.
 - Mencoba mendapatkan data user
  [![3.png](https://s5.postimg.org/qddpzntqf/image.png)](https://postimg.org/image/a2dm3ch8j/)
  jalankan perintah di atas
  [![4.png](https://s5.postimg.org/ozm34cuh3/image.png)](https://postimg.org/image/r46g5fw3n/)
  terdapat 36 table pada database wpdb. Selanjutnya mencari data user pada tabel wp_users
  [![5.png](https://s5.postimg.org/vrci77jgn/image.png)](https://postimg.org/image/xj5h242tf/)
  perintah di atas digunakan untuk mencari kolom-kolom pada tabel wp_users
  [![6.png](https://s5.postimg.org/s90iatikn/image.png)](https://postimg.org/image/vsmg0mlab/)
  mencari data pada kolom display_name, user_login, user_pass, dan user_email
  [![7.png](https://s5.postimg.org/b9rjvk7d3/image.png)](https://postimg.org/image/qv8vfijb7/)
  setelah dijalankan maka akan muncul data-data sesuai kolom yang dipilih
  [![9.png](https://s5.postimg.org/3wc5wlnbb/image.png)](https://postimg.org/image/crd074c3n/)

 b. CP Multi View Event Calender 1.1.4
 - command sqlmap untuk cp multi view event calender
 [![11.png](https://s5.postimg.org/q4l76un9j/image.png)](https://postimg.org/image/3snedgo5f/)
 ketik enter untuk menjalankan perintah di atas
 - Hasil setelah melakukan perintah di atas
 [![12.png](https://s5.postimg.org/46oqd2893/image.png)](https://postimg.org/image/mz0lgn4n7/)
 - Mengecek database setelah berhasil melakukan injection
 [![18.png](https://s5.postimg.org/bhou2xe13/image.png)](https://postimg.org/image/7lbi6xt1f/)
 jalankan perintah di atas
 [![19.png](https://s5.postimg.org/rtyvsnscn/image.png)](https://postimg.org/image/w33lutvlv/)
 hasil dari perintah di atas. Selanjutnya kita bisa membuka tabel pada database wpdb seperti pada Leaguemanager 3.9.1.1

#H. Kesimpulan dan Saran
Plugin dari CMS Worpress sangatlah banyak, plugin-plugin yang ada bisa menambah fitur dari website wordpress yang kita bangun, namun kerentanan terhadap sebuah serangan terhadap plugin-plugin yang disediakan oleh wordpress pun sangat tinggi. Apabila pengguna tidak secara berkala memeperbaharui versi dari plugin yang mereka sematkan pada website wordpress mereka, maka akan sangat mudah dilakukan penyerangan dengan memanfaatkan celah kerentanan plugin yang disematkan pada website wordpress. 

Pengguna diharuskan untuk selalu memperbaharui versi dari plugin yang terinstall didalam website wordpress yang dimiliki, dikarenakan pengembang akan memperbaharui aplikasi yang mereka bangun apabila telah ditemukan kerentanan dari aplikasi yang mereka bangun.


