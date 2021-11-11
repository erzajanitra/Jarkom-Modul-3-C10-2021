# Jarkom-Modul-3-C10-2021

## Anggota Kelompok C10
| Nama | NRP |
| ------------- | ------------- |
| Christian Bennett Robin | 05111940000078  |
| Erza Janitradevi Nadine  | 05111940000153  |
| Akmal Zaki Asmara  | 05111940000154  |

## Soal dan Pembahasan
### No 1

### No 2

### No 3

### No 4

### No 5

### No 6

### No 7
Soal:
Luffy dan Zoro berencana menjadikan Skypie sebagai server untuk jual beli kapal yang dimilikinya dengan alamat IP yang tetap dengan IP [prefix IP].3.69 (7). 

Jawab:
Edit konfigurasi /etc/dhcp/dhcpd.conf di Jipangu, lalu tambahkan baris berikut:

```
...
host Skypie {
    hardware ethernet 3e:a0:f8:fb:39:c5;
    fixed-address 10.19.3.69;
}
```

Setelah itu edit konfigurasi /etc/network/interfaces di Client, seperti misalnya di Loguetown dan tambahkan baris berikut:

```
...
hwaddress ether 3e:a0:f8:fb:39:c5
```

Saat menyalakan node Skypie, didapatkan IPnya tetap, yaitu 10.19.3.69
![7](img/7.png)

### No 8

### No 9

### No 10

### No 11

### No 12 & 13
Soal: 
Saatnya berlayar! Luffy dan Zoro akhirnya memutuskan untuk berlayar untuk mencari harta karun di super.franky.yyy.com. Tugas pencarian dibagi menjadi dua misi, Luffy bertugas untuk mendapatkan gambar (.png, .jpg), sedangkan Zoro mendapatkan sisanya. Karena Luffy orangnya sangat teliti untuk mencari harta karun, ketika ia berhasil mendapatkan gambar, ia mendapatkan gambar dan melihatnya dengan kecepatan 10 kbps (12). Sedangkan, Zoro yang sangat bersemangat untuk mencari harta karun, sehingga kecepatan kapal Zoro tidak dibatasi ketika sudah mendapatkan harta yang diinginkannya (13).

Jawaban:
Edit konfigurasi /etc/squid/squid.conf di Water7 dan tambahkan baris berikut: 

```
...
acl USERS proxy_auth REQUIRED
acl USER1 proxy_auth luffybelikapalc10
acl USER2 proxy_auth zorobelikapalc10
acl BLACKLIST dstdomain .google.com
acl ext_block url_regex "/etc/squid/ext_block.txt"

delay_pools 2
delay_class 1 1
delay_access 1 allow USER2
delay_parameters 1 -1/-1
delay_class 2 1
delay_access 2 allow ext_block
delay_parameters 2 1250/1250
...

```

Pool dibagi menjadi 2 class untuk 2 konfigurasi. Class pertama dikonfigurasi untuk USER2 yaitu zorobelikapalc10. Agar bandwidthnya tidak dilimit seperti permintaan soal 13, maka delay_parameter pool 1 diatur agar menjadi -1/-1. Sedangkan class kedua dikonfigurasi agar bandwidthnya dilimit menjadi 10 kbps atau 1250 Bps seperti permintaan soal 12. Class kedua juga dikonfigurasi agar berlaku pada file yang extensionnya terdapat di dalam file /etc/squid/ext_block.txt yang berisi:

```
\.jpg$
\.png$
```

Saat login menggunakan luffybelikapalc10, maka user tersebut akan terlimit bandwidth download file .jpg dan .png nya seperti pada konfigurasi. Saat berusaha untuk mendownload file tersebut, user tersebut akan tertahan pada page ini karena sudah di limit bandwidthnya.
![12](img/12.png)

Sedangkan jika login menggunakan zorobelikapalc10, saat user berusaha untuk mendownload file yang bukan .jpg atau .png, download tersebut akan langsung selesai dan pindah ke page selanjutnya karena tidak di limit bandwidthnya.
![13](img/13.png)
