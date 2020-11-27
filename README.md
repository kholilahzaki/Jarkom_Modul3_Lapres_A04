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




