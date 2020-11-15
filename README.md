# Lapres Modul 2 Jaringan Komputer

---

<ul>
    <li>05111840000039 - Sitti Chofifah</li>
    <li>05111840000139 - Dohan Pranata W </li>
</ul>

## Soal

### Nomer 1,2, dan 3

**Membuat sebuah website utama dengan alamat http://semeruyyy.pw yang memiliki alias http://www.semeruyyy.pw, dan subdomain http://penanjakan.semeruyyy.pw yang diatur DNS-nya pada MALANG dan mengarah ke IP Server PROBOLINGGO**

Buka UML server MALANG lakukan `apt-get update` dan install bind9 pada UML MALANG. Setelah itu lakukan `nano /etc/bind/named.conf.local`.
Konfigurasi server MALANG seperti gambar dibawah :
![1.1](asset/1.1.png)

Lalu di buat folder sesuai dengan `file` di konfigurasi sebelumnya
`mkdir /etc/bind/semeruyyy`
lalu lakukan `cp /etc/bind/db.local /etc/bind/semeruyyy/semerub11.pw` sesuai soal nomer 1,2,3 dimana di suruh buat alamat http://semeruyyy.pw\_ yang memiliki alias http://www.semeruyyy.pw, dan subdomain http://penanjakan.semeruyyy.pw dan diarhakan ke server PROBOLINGGO( "10.151.83.100").
![1.2](asset/1.2.png)

lalu lakukan restart bind9 dengan inputkan `service bind9 restart`

Untuk cek konfigurasi tersebut dapat melakukan ping ke alamt yang sudah kita buat melalui client GRESIk atau SIDOARJO dan jangan lupa untuk untuk menambah nameserver pada Client Server dengan :

> nano /etc/resolv.conf

dan tambahkan `nameserver "IP MALANG"` seperti gambar berikut
![1.3](asset/1.3.png)

dan lakukan ping di salah satu client `ping semerub11.pw` , `ping www.semerub11.pw` , dan `ping penanjakan.semerub11.pw` seperti gambar berikut yang dilakukan di client GRESIK :
![1.4](asset/1.4.png)

### Nomer 4

**Membuat reverse domain untuk domain utama**
Untuk membuat reverse domain utama inputkan `nano /etc/bind/named.conf.local` pada uml MALANG dan melakukan konfigurasi file tersebut dengan inputkan

> zone "83.151.10.in-addr.arpa" {
> type master;
> filr "/etc/bind/semeruyyy/83.151.10.in-addr.arpa";
> }

seperti gambar berikut :
![4.1](asset/4.1.png)

setelah itu copykan file db.local ke dalam file 83.151.10.in-addr.arpa pada folder jarkom dengan perintah `cp /etc/bind/db.local /etc/bind/jarkom/83.151.10.in-addr.arpa` setelah file tersebut di konfigurasi seperti gambar berikut :
![4.2](asset/4.2.png)

lalu restart bind9 dengan melakukan perintah `service bind9 restart` dan untuk mengeceknya pada salah satu clinet kita install dulu dnsutils dengan perintah apt-get install dnsutils lalu inputkan perintah `host -t PTR 10.151.83.100` pada salah satu client tersebut. Berikut hasilnya :
![4.3](asset/4.3.png)

### Nomer 5

**Membuat Server Slave di MOJOKERTO**
Konfigurasi Pada Server MALANG.
Edit file /etc/bind/named.conf.local dan disesuaikan dengan syntax berikut :
![5.1](asset/5.1.png)

Restart bind9 dengan melakukan perintah `service bind9 restart`
lalu lakukan konfigurasi pada server di mojokerto dengan menjalankan perintah `apt-get update` dan install bind9 pada server mojokerto.
Kemudian buka file `/etc/bind/named.conf.local` pada MOJOKERTO dan ditambhakan syntax seperti gambar berikut :
![5.2](asset/5.2.png)

dan restart bind9.

untuk testing pada nameserver di CLIENT arahkan ke ip mojokerto dan matikan bind9 pada malang. Lakukan ping ke semerub11.pw di CLIENT. Beikut gambarnya :
![5.3](asset/5.3.png)

### Nomer 6.

**Membuat sub domain http://gunung.semerub11.pw yang didelegasikan di server MOJOKERTO dan diarahkan ke server Probolinggo**
untuk mendelegasikan sub domain di server MOJOKERTO. Server malang kita konfigurasi dulu pada file semerub11.pw, dengan menambahkan

> ns1 IN A 10.151.83.99
> gunung IN A ns1

seperti gambar di bawah :
![6.1](asset/6.1.png)

selanjutnya konfigurasi file `/etc/bind/named.conf.options` seperti gambar di bawah :
![6.2](asset/6.2.png)

restart bind9.
Konfigurasi server MOJOKERTO. Buka file /etc/bind/named.conf.options
![6.4](asset/6.4.png)

Lanjut membuat directory delegasi mkdir /etc/bind/delegasi
Kemudian edit nano /etc/bind/delegasi/gunung.semerub11.pw
![6.5](asset/6.5.png)

Selanjutnya lakukan test ping gunung.semerub11.pw di gresik
![6.6](asset/6.6.png)

### Nomer 7

**Membuat subdomain dengan nama http://naik.gunung.semeruyyy.pw, main ini diarahkan ke IP Server PROBOLINGGO.**

Lakukan edit file nano /etc/bind/delegasi/gunung.semerub11.pw pada mojokerto dan tambahkan konfigurasi

> naik IN A 10.151.83.100

![7.1](asset/7.1.png)

Selanjutnya lakukan test ping naik.gunung.semerub11.pw di gresik :
![7.2](asset/7.2.png)

### Nomer 8

**Membuat domain http://semeruyyy.pw memiliki Document Root pada /var/www/semeruyyy.pw.**

Lakukan perintah `cd /etc/apache2/sites-available` di Probolinggo
Kemudian edit file nano semerub11.pw dan tambahkan konfigurasi seperti gamabr dibawah ini :
![8.1](asset/8.1.png)

Selanjutnya pindah ke directory /var/www

Kemudian gunakan perintah wget 10.151.36.202/semeru.pw.zip untuk mendownload file yang sudah disediakan pada soal praktikum dan selanjutnya jangan lupa untuk unzip file

Setelah semua sudah selesai, buka browser dan akses semerub11.pw
![8.2](asset/8.2.png)

### Nomer 9

**Menggunakan mod rewrite agar urlnya menjadi http://semeruyyy.pw/home.**

Untuk menggunakan mod rewrite menuju ke file rootnya semerub11.pw yaitu dengan

> cd /var/www/semerub11.pw

lalu ubah file .htacces nya dengan menggunakan `nano .htaccess` dan ubha file tersebut seperti gambar berikut :
![9.1](asset/9.1.png)

lalu cek di browser seperti gambar berikut :
![9.2](asset/9.2.png)

### Nomer 10 dan 11

**Web http://penanjakan.semeruyyy.pw akan digunakan untuk menyimpan assets file yang memiliki documentRoot pada /var/www/penanjakan.semeruyyy.pw dan memiliki struktur folder sebagai berikut:**
/var/www/penanjakan.semeruyyy.pw

<ul>
<li>/public/javascripts
<li>/public/css
<li>/public/images
<li> /errors
</ul>

**Pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan**

Unzip dulu file yag sudah di download di folder `var/www/` yaitu `penanjakna.semeru.pw.zip` lalu rename namanya menjadi `penanjakna.semerub11.pw.zip`.

lalu Pindah ke directory `/etc/apache2/` sites-available dengan perintah `cd /etc/apache2/sites-available` Copy file default menjadi file penanjakan.semerub11.pw, Buka file penanjakan.semerub11.pw, lalu tambahkan

> ServerName penanjakan.semerub12.pw
> ServerAlias www.penanjakan.semerub12.pw

Kemudian ubah DocumentRoot menjadi /var/www/penanjakan.semerub11.pw seperti gambar berikut :
![10.1](asset/10.1.png)

lalu jalankan `a2ensite penanjakan.semerub11.pw` untuk mengaktifkan web dan restart apache2.

lalu buka alamat `penanjakan.semerub11.pw` di browser
![10.2](asset/10.2.png)

setelah itu untuk setting access buka kembali file konfigurasi penanjakan.semerub11.pw dengan `nano /etc/apache2/sites-available/penanjakan.semerub11.pw` lalu tambahkan

> <Directory /var/www/penanjakan.semerub12.pw/public>
> Options +Indexes
> \</Directory>

dan untuk folder di dalam public yang tidak boleh di access dapat menambahakan

> <Directory /var/www/penanjakan.semerub12.pw/public/images>
> Options -Indexes
>
> \</Directory>
> <Directory /var/www/penanjakan.semerub12.pw/public/css>
> Options -Indexes
> \</Directory>
>
> <Directory /var/www/penanjakan.semerub12.pw/public/javascripts>
> Options -Indexes
> \</Directory>

Seperti gambar berikut :
![11.1](asset/11.1.png)

lalu restart apaceh2 dengan `service apache2 restart` lalu cek di browser da hasilnya seperti berikut :
![11.2](asset/11.2.png)
![11.3](asset/11.3.png)

### Nomer 12

**Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada folder /errors untuk mengganti error default 404 dari Apache.**

Pindah ke directory `etc/apache2/sites-available` pada probolinggo kemudian buka file penanjakan.semerub11.pw dengan `nano penanjakan.semerub11.pw`dan tambahkan konfigurasi

> ErrorDocument 404 /errors/404.html
> ![12.1](asset/12.1.png)

Lalu buka browser dan akses penanjakan.semerub11.pw/"Input terserah yang penting tidak ada dalam root file"
contoh `penanjakan.semerub11.pw/a`
![12.2](asset/12.2.png)

### Nomer 13

**Untuk mengakses file assets javascript awalnya harus menggunakan url http://penanjakan.semeruyyy.pw/public/javascripts. Karena terlalu panjang maka dibuatkan konfigurasi virtual host agar ketika mengakses file assets menjadi http://penanjakan.semeruyyy.pw/js.**

ubah file konfigurasi penanjakan.semerub11.pw dengan `nano /etc/apache2/sites-available/penanjakan.semerub11.pw`
lalu tambahkan :

> Alias "/js" "var/www/penanjakan.semerub11.pw/public/javascripts"

![13.1](asset/13.1.png)

lalu buka browser dan ketikkan `penanjakan.semerub11.pw/js`
![13.2](asset/13.2.png)

### Nomer 14

**web http://naik.gunung.semeruyyy.pw sudah bisa diakses hanya dengan menggunakan port 8888. DocumentRoot web berada pada /var/www/naik.gunung.semeruyyy.pw. Dikarenakan web http://naik.gunung.semeruyyy.pw bersifat private**

Edit file pada probolinggo `nano /etc/apache2/ports.conf` dan tambahkan konfigurasi

> Listen 8888

![14.1](asset/14.1.png)

Kemudian pindah directory ke /etc/apache2/sites-available/

copy default menjadi file naik.gunung.semerub11.pw

Dan edit file naik.gunung.semerub11.pw dan tambahkan konfigurasi

> <VirtualHost \*:8888>
> ServerName naik.gunung.semerub11.pw
> ServerAlias www.naik.gunung.semerub11.pw

Dan ubah DocumentRoot menjadi /var/www/naik.gunung.semerub11.pw

![14.2](asset/14.2.png)

Selanjutnya Pindah ke directory /var/www dan lakukan wget 10.151.36.202/naik.gunung.semeru.pw.zip untuk mendownload file selanjutnya unzip file dan akses naik.gunung.semerub11.pw di browser
![14.3](asset/14.3.png)

### Nomer 15

**membuat web http://naik.gunung.semeruyyy.pw agar diberi autentikasi password dengan username “semeru” dan password “kuynaikgunung” supaya aman dan tidak sembarang orang bisa mengaksesnya.**

Pertama kita akan membuat username dengan perintah htpasswd -c /etc/apache2/.htpasswd semeru
Kemudian membuat password dengan perintah htpasswd /etc/apache2/.htpasswd kuynaikgunung
![15.1](asset/15.1.png)

Selanjutnya edit file etc/apache2/sites-enabled/naik.gunung.semerub11.pw untuk menambahkan authentication

> <Directory /var/www/naik.gunung.semerub11.pw>

     AuthType Basic
     AuthName "Restricted Content"
     AuthUserFile /etc/apache2/.htpasswd
     Require valid-user

> \</Directory>

![15.2](asset/15.2.png)
Kemudian buka browser dan akses naik.gunung.semerub11.pw

![15.3](asset/15.3.png)

### Nomer 16

**mengunjungi IP PROBOLINGGO, yang muncul bukan web utama http://semeruyyy.pw melainkan laman default Apache yang bertuliskan “It works!”. Karena dirasa kurang profesional, maka setiap mengunjungi IP PROBOLINGGO akan dialihkan secara otomatis ke http://semeruyyy.pw**

Untuk nomer 16 di server yang sudah kita buat kita tidak melakukan apa-apa karean ketika kita cek dengan menuliskan di browser 10.151.83.100 otomatis web akan langsung menuju ke semerub11.pw. sehingga untuk nomer 16 kita skip saja.
Berikut gambarnya :
![16.1](asset\16.1.png)

### Nomer 17

**Karena pengunjung pada/var/www/penanjakan.semeruyyy.pw/public/images sangat banyak maka semua request gambar yang memiliki substring “semeru” akan diarahkan menuju semeru.jpg.**

Pindah directory ke /var/www pada probolinggo
Edit file penanjakan.semerub11.pw/.htaccess seperti gambar dibawah ini
Dan edit file penanjakan.semerub11.pw seperti gambar dibawah:
![17.1](asset/17.1.png).
Lalu kita cek dengan menuliskan `penanjakan.semerub11.pw/public/images/dadwsemerusadawdaw` di browser

![17.2](asset/17.2.png)
ketika kita enter ankan keluar seprti ini :
![17/3](asset/17.3.png)

**SEKIAN LAPORAN RESMI DARI KELLOMPOK B11 JARINGAN KOMPUTER**
