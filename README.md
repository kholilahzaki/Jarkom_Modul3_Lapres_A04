# Jarkom_Modul3_Lapres_A04

Kelompok A04:
-
#### I Gusti Agung Chintya Prema Dewi   (05111840000130)
#### Kholilah Zaki Lismia               (05111840000159)


## Teknis Pengerjaan
1. Default memori UML adalah 64M, kecuali :
   - SURABAYA : 256M
   - MALANG : 160M
   - MOJOKERTO : 128M
   - TUBAN : 128M
   
2. Menghitung dan menggunakan IP sesuai dengan NID Tuntap dan NID DMZ masing-masing kelompok

3. IP Tuntap : 10.151.72.21

4. IP Interface Router SURABAYA :
   - eth0 : 10.151.72.22
   - eth3 : 10.151.73.41
   - eth1 : 192.168.0.1
   - eth2 : 192.168.1.1
   
5. IP Server (SUBNET 2) :
   - MALANG : 10.151.73.42
   - MOJOKERTO : 10.151.73.43
   - TUBAN : 10.151.73.44
  
## Soal:
Anri adalah seorang mahasiswa tingkat akhir yang sedang mengerjakan TA mengenai DHCP dan Proxy. Bu Meguri sebagai dosen pembimbing Anri memberikan tugas pertamanya

**1.** Yaitu untuk membuat topologi jaringan demi kelancaran TA-nya dengan kriteria sebagai berikut:

<p align="center"><img width="auto" src="https://user-images.githubusercontent.com/61299072/100396599-3d71a980-3078-11eb-9192-9e5ecbee41af.PNG"></p><br>

Anri sudah pernah mempelajari teknik Jaringan Komputer sehingga Anri dapat membuat topologi tersebut dengan mudah. Bu Meguri memerintahkan Anri untuk menjadikan SURABAYA 
sebagai router, MALANG sebagai DNS Server, TUBAN sebagai DHCP server, serta MOJOKERTO sebagai Proxy server, dan UML lainnya sebagai client. 
Bu Meguri berpesan pada Anri untuk menyusun topologi secara hati-hati dan memperhatikan gambar topologi yang diberikan Bu Meguri. 
Karena TUBAN jauh dari client, maka perlu adanya perantara agar bisa saling terhubung.

**2.** SURABAYA ditunjuk sebagai perantara (DHCP Relay) antara DHCP Server dan client. Kriteria lain yang diminta Bu Meguri pada topologi jaringan tersebut adalah:
   - Seluruh client **TIDAK DIPERBOLEHKAN** menggunakan konfigurasi IP Statis.
   - **3.** Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200.
   - **4.** Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.
   - **5.** Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP
   - **6.** Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client pada subnet 3 mendapatkan peminjaman IP selama 10 menit.
   
Bu Meguri adalah dosbing yang suka overthinking. Ia tidak ingin jaringan lokalnya terhubung ke internet secara langsung. Sehingga ia memberi tugas tambahan 
pada Anri untuk membuatkan Proxy sebagai penghubung jaringan lokal ke internet. Ada beberapa ketentuan yang harus dipenuhi dalam pembuatan Proxy ini.

Pertama, akses ke proxy hanya bisa dilakukan oleh Anri sendiri sebagai user TA.

**7.** User autentikasi milik Anri memiliki format:

  <p align="center">- User : userta_yyy</p>
  <p align="center">- Password : inipassw0rdta_yyy</p>
  <b>Keterangan : yyy adalah nama kelompok masing-masing. Contoh: userta_c01</b><br>

Anri sudah menjadwal pengerjaan TA-nya

**8.** Setiap hari Selasa-Rabu pukul 13.00-18.00. Bu Meguri membatasi penggunaan internet Anri hanya pada jadwal yang telah ditentukan itu saja. 
Maka diluar jam tersebut, Anri tidak dapat mengakses jaringan internet dengan proxy tersebut. Jadwal bimbingan dengan Bu Meguri adalah

**9.** Setiap hari Selasa-Kamis pukul 21.00 - 09.00 keesokan harinya (sampai Jumat jam 09.00). Agar Anri bisa fokus mengerjakan TA,

**10.** Setiap dia mengakses google.com, maka akan di redirect menuju monta.if.its.ac.id agar Anri selalu ingat untuk mengerjakan TA🙂.
Untuk menandakan bahwa Proxy Server ini adalah Proxy yang dibuat oleh Anri,

**11.** Bu Meguri meminta Anri untuk mengubah error page default squid menjadi seperti berikut:

<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100397246-38fac000-307b-11eb-90f5-19f62756f807.PNG"></p><br>

**Note** : File error page bisa diunduh dengan cara `wget 10.151.36.202/ERR_ACCESS_DENIED.` 
Tidak perlu di extract, cukup cp -r

**12.** Karena Bu Meguri dan Anri adalah tipe orang pelupa, maka untuk memudahkan mereka, Anri memiliki ide ketika menggunakan proxy cukup dengan mengetikkan domain janganlupa-ta.yyy.pw dan memasukkan port 8080. 

***Keterangan:*** yyy adalah nama kelompok masing-masing. Contoh: janganlupa-ta.c01.pw

Bantu Anri menyelesaikan TA nya dibawah bimbingan Bu Meguri!👩🏻‍🎓

***Catatan:*** Jika tidak bisa dan menyerah untuk setup DHCP Server pada TUBAN (dengan relay pada SURABAYA), maka setup DHCP pada SURABAYA (tanpa DHCP Relay). Pastinya nilai tidak akan maksimal.

## Jawaban:

### 1.
-------------------------
**Membuat topologi.sh sesuai dengan gambar pada soal**

- Pada PuTTY tuliskan syntax berikut pada file topologi.sh
```
# Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,'10.151.72.21' eth1=daemon,,,switch1 eth2=daemon,,,switch3 eth3=daemon,,,switch2 mem=256M &

# Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=160M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &
xterm -T TUBAN -e linux ubd0=TUBAN,jarkom umid=TUBAN eth0=daemon,,,switch2 mem=128M &

# Klien
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch1 mem=64M &
xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch1 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch3 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch3 mem=64M &
```

<p align="center"><img width="auto" src="https://user-images.githubusercontent.com/61299072/100535187-42d21e00-3249-11eb-86b3-7e957baa52dc.PNG"></p><br>

- Setelah itu ketik bash topologi.sh, dan setelah UML nya terbuka, lakukan setting sysctl seperti pada modul pengenalan UML, lalu setting interface masing-masing UML seperti berikut

**SURABAYA (Router/DHCP Relay)**
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100535729-25ec1980-324e-11eb-80d7-04a6ad668a3a.PNG"></p><br>

<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100535730-25ec1980-324e-11eb-8d70-f1fe1482bfdc.PNG"></p><br>

**TUBAN (DHCP Server)**
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100535732-2684b000-324e-11eb-9796-2e6cf7e41648.PNG"></p><br>

**MALANG (DNS Server)**
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100535727-24225600-324e-11eb-94e8-09e10ab2cea4.PNG"></p><br>

**MOJOKERTO (Proxy Server)**
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100535728-25538300-324e-11eb-8a3a-effd170a0162.PNG"></p><br>

- Kemudian ketik `service networking restart` pada setiap UML

### 2. 
-----------------------------
**Membuat DHCP Relay pada Surabaya**

- Lakukan `apt-get update`

- Install isc-dhcp-relay dengan perintah `apt-get install isc-dhcp-relay`

- Setelah itu, buka file /etc/default/isc-dhcp-relay dan edit menjadi
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100535869-39e44b00-324f-11eb-9f9f-aeae3b1c74dd.PNG"></p><br>

Keterangan:
-
- `SERVERS="10.151.73.44"` menggunakan IP TUBAN karena nantinya akan di relay mengarah ke UML Tuban
- `INTERFACES="eth1 eth2 eth3"` karena agar Surabaya mendapat peran selayaknya sebagai DHCP Server

### 3, 4, 5, 6
----------------------------
**Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200.**

**Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.**

**Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP**

**Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client pada subnet 3 mendapatkan peminjaman IP selama 10 menit.**

- Lakukan `apt-get update`

- Install isc-dhcp-server dengan perintah `apt-get install isc-dhcp-server`

- Setelah itu edit file /etc/default/isc-dhcp-server sebagai berikut
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100536094-d0fdd280-3250-11eb-9d54-5a10de35ed0f.PNG"></p><br>

Keterangan:
- 
- `INTERFACES="eth0"` karena agar TUBAN dapat terhubung ke Router/DHCP Relay yaitu SURABAYA


- Setelah itu edit file /etc/dhcp/dhcpd.conf seperti berikut
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100536242-d871ab80-3251-11eb-974b-0887009dcc59.PNG"></p><br>

<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100536244-da3b6f00-3251-11eb-9b31-2c8383e373da.PNG"></p><br>

Keterangan:
-
- `subnet 192.168.0.0 netmask 255.255.255.0` 192.168.0.0 merupakan ip dari subnet 1
- `range 192.168.0.10 192.168.0.100;` dan `range 192.168.0.110 192.168.0.200;` merupakan jumlah range IP yang akan didapatkan oleh client yang ada pada subnet 1 **(No. 3)**
- lalu pada `subnet 192.168.1.0 netmask 255.255.255.0` yang merupakan ip dari subnet 3, terdapat `range 192.168.1.50 192.168.1.70;` yang artinya client pada subnet 3 akan mendapatkan range IP dari 192.168.1.50 - 192.168.1.70 **(No. 4)**
- `option domain-name-servers 202.46.129.2, 10.151.73.42;` artinya client akan mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP **(No. 5)**
- `default-lease-time 300;` dan `max-lease-time 300;` yang terdapat pada subnet 1 artinya client di subnet 1 akan mendapat peminjaman alamat IP selama 5 menit (300 detik) **(No. 6)**
- `default-lease-time 600;` dan `mas-lease-time-600;` yang terdapat pada subnet 3 artinya client di subnet 3 akan mendapat peminjaman alamat Ip selama 10 menit (600 detik) **(No. 6)**


- Setelah itu simpan dan lakukan restart dhcp server dengan `service isc-dhcp-server restart`
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100536734-17553080-3255-11eb-9d11-1e4532804f77.PNG"></p><br>

- Lakukan testing pada semua UML Klien, tapi ubah terlebih dahulu settingan interface pada setiap UML klien seperti berikut
<p align="center"><img width="auto" src="https://user-images.githubusercontent.com/61299072/100536773-64d19d80-3255-11eb-8873-41d6126545cd.png"></p><br>

- Setelah itu lakukan `service networking restart` pada setiap UML klien. Dan lakukan testing dengan perintah `cat /etc/resolv.conf` dan `ifconfig` pada setiap UML klien

###  Gresik (Subnet 1)
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100536863-fe994a80-3255-11eb-8d68-8f9ab8c81bfc.PNG"></p><br>

<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100536864-ff31e100-3255-11eb-800a-75a460bee14b.PNG"></p><br>

### Sidoarjo (Subnet 1)
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100536867-00fba480-3256-11eb-8d94-1effc4976ba8.PNG"></p><br>

<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100536868-00fba480-3256-11eb-941f-1b26d60201a5.PNG"></p><br>

### Banyuwangi (Subnet 3)
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100536858-fc36f080-3255-11eb-966f-653b227ff8a5.PNG"></p><br>

<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100536861-fe00b400-3255-11eb-84d0-ab3cc0aeffda.PNG"></p><br>

### Madiun (Subnet 3)
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100536865-ffca7780-3255-11eb-8b3d-93447048027e.PNG"></p><br>

<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100536866-00630e00-3256-11eb-99c0-d9db0c31fdd8.PNG"></p><br>

### 7, 8, 9, 10, 11
--------------------------------------------
**Membuat user autentikasi**

**Jadwal akses Selasa-Rabu pukul 13.00-18.00.**

**Jadwal bimbingan Selasa-Kamis pukul 21.00 - 09.00 keesokan harinya (sampai Jumat jam 09.00).**

**Saat mengakses google.com, maka akan di redirect menuju monta.if.its.ac.id**

**Mengubah error page default squid**

- Pada MOJOKERTO lakukan `apt-get update`

- Lalu install squid dengan perintah `apt-get install squid`

- Setelah itu lakukan `mv /etc/squid/squid.conf /etc/squid/squid.conf.bak`

- Lalu edit file /etc/squid/squid.conf seperti berikut **(belom ada gambarnya yang bener)**

- Untuk membuat user autentikasi, terlebih dahulu install apache2-utils dengan perintah `apt-get install apache2-utils`

- Kemudian ketikkan `htpasswd -c /etc/squid/passwd userta_a04` untuk membuat akun baru dan masukkan `inipassw0rdta_a04` sebagai passwordnya **(No. 7)**
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100537118-52a52e80-3258-11eb-8380-fdc1cf442842.PNG"></p><br>

- Tambahkan perintah berikut pada /etc/squid/squid.conf
```
auth_param basic program /usr/lib/squid/ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Proxy
auth_param basic credentialsttl 2 hours
auth_param basic casesensitive on
acl USERS proxy_auth REQUIRED
http_access allow USERS
```

- Lakukan `service squid restart` kemudian hidupkan setting proxy
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100537285-b714bd80-3259-11eb-96c6-77d184ce041a.PNG"></p><br>

- Testing (buka pada mode incognito)
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100537206-fbec2480-3258-11eb-9e79-52d0b41bdae9.PNG"></p><br>

- Lalu untuk melakukan pembatasan waktu akses dapat mengedit file /etc/squid/acl.conf sebagai berikut
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100537238-35249480-3259-11eb-83c9-8a861293c25c.PNG"></p><br>

Keterangan:
-

- `acl AVAILABLE_WORKING time TW 13:00-18:00` agar waktu akses dibatasi dari hari Selasa-Rabu pukkul 13:00-18:00. `T`= Tuesday dan `W`= Wednesday **(No. 8)**

- `acl AVAILABLE_WORKING2 time TWH 21:00-23:59` dan `acl AVAILABLE_WORKING3 time WHF 00:00-09:00` mengapa dibuat seperti itu, karena start pada hari Selasa, Rabu dan Kamis dimulai dari pukul 21:00 dan berakhir di jam 23:29, sedangkan Rabu, Kamis, dan Jumat start dimulai pada jam 00:00 dan berakhir di jam 09:00, jadi ada perbedaan start di hari Selasa dan Jumat. **(No. 9)**


- Lalu tambahkan perintah sebagai berikut pada file /etc/squid/squid.conf
```
include /etc/squid/acl.conf

http_access allow AVAILABLE_WORKING
http_access allow AVAILABLE_WORKING_2
http_access allow AVAILABLE_WORKING_3
```

- Untuk **(No. 10)** agar saat membuka google.com akan ter-redirect ke http://monta.if.its.ac.id dapat ditambahkan perintah berikut pada file /etc/squid/squid.conf
```
acl REDIRSITE dstdomain google.com
deny_info http://monta.if.its.ac.id REDIRSITE
http_reply_access deny REDIRSITE
```
Keterangan:
-
- `acl REDIRSITE dstdomain google.com` untuk men-deny pengaksesan google.com
- `deny_info http://monta.if.its.ac.id REDIRSITE` untuk memberitahu bahwa deny dengan redirect ke http://monta.if.its.ac.id untuk REDIRSITE
- `http_reply_access deny REDIRSITE` untuk men-deny google.com terhadap REDIRSITE

- Lakukan `service squid restart` lalu testing
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100541915-ac6a2080-3279-11eb-852c-d1e1f6cbad41.PNG"></p><br>

<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100541918-ae33e400-3279-11eb-9309-2c88e195ad66.PNG"></p><br>

- Apabila kita hendak mengakses http://monta.if.its.ac.id diluar jam akses maka akan muncul error page seperti berikut
<p align="center"><img width="700" src="https://user-images.githubusercontent.com/61299072/100397246-38fac000-307b-11eb-90f5-19f62756f807.PNG"></p><br>

- untuk **(no. 11)** Untuk menandakan bahwa Proxy Server ini adalah Proxy yang dibuat oleh Anri, Bu Meguri meminta Anri untuk mengubah error page default squid menjadi seperti berikut :

![403](https://user-images.githubusercontent.com/52326074/99974165-24949a00-2dd3-11eb-8f25-9fd6efa16e09.jpg)

`Note` :

File error page bisa diunduh dengan cara `wget 10.151.36.202/ERR_ACCESS_DENIED`, tidak perlu di extract, cukup `cp -r`

- pertama masuk ke dalam folder error dengan mennjalankan perintah `cd /usr/share/squid/errors/English`
- kemudian jalankan perintah `ls` untuk mengetahui isi keseluruhan folder tersebut, kemudian cari file bernama `ERR_ACCESS_DENIED`
- lalu jalankan perintah `rm ERR_ACCESS_DENIED` untuk menghapus file tersebut
- selanjutnya download file berupa gambar error untuk menggantikan file yg sebelumnya dihapus dengan menjalankan perintah `wget 10.151.36.202/ERR_ACCESS_DENIED`
