# Lapres Modul 2 Jaringan Komputer

---

<ul>
    <li>05111840000039 - Sitti Chofifah</li>
    <li>05111840000139 - Dohan Pranata W </li>
</ul>

## Soal

#### Nomer 1,2, dan 3

**_Membuat sebuah website utama dengan alamat http://semeruyyy.pw_ yang memiliki alias http://www.semeruyyy.pw, dan subdomain http://penanjakan.semeruyyy.pw yang diatur DNS-nya pada MALANG dan mengarah ke IP Server PROBOLINGGO**

Buka UML server MALANG lakukan `apt-get update` dan install bind9 pada UML MALANG. Setelah itu lakukan `nano /etc/bind/named.conf.local`.
Konfigurasi server MALANG seperti gambar dibawah :
![1.1](asset/soal_1/1.1.png)
Lalu di buat folder sesuai dengan `file` di konfigurasi sebelumnya
`mkdir /etc/bind/semeruyyy`
lalu lakukan `cp /etc/bind/db.local /etc/bind/semeruyyy/semerub11.pw` sesuai soal nomer 1,2,3 dimana di suruh buat alamat http://semeruyyy.pw\_ yang memiliki alias http://www.semeruyyy.pw, dan subdomain http://penanjakan.semeruyyy.pw dan diarhakan ke server PROBOLINGGO( "10.151.83.100").
![1.2](asset/soal_1/1.2.png)
