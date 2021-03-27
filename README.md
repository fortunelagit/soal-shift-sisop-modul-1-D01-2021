# soal-shift-sisop-modul-1-D01-2021
Khaela Fortunela 05111940000057

M Haikal Aria Sakti 05111940000088

David Ralphwaldo M 05111940000190

## Soal 1
## Soal 2
## Soal 3
Kuuhaku adalah orang yang sangat suka mengoleksi foto-foto digital, namun Kuuhaku juga merupakan seorang yang pemalas sehingga ia tidak ingin repot-repot mencari foto, selain itu ia juga seorang pemalu, sehingga ia tidak ingin ada orang yang melihat koleksinya tersebut, sayangnya ia memiliki teman bernama Steven yang memiliki rasa kepo yang luar biasa. Kuuhaku pun memiliki ide agar Steven tidak bisa melihat koleksinya, serta untuk mempermudah hidupnya, yaitu dengan meminta bantuan kalian. Idenya adalah :

a. Membuat script untuk mengunduh 23 gambar dari "https://loremflickr.com/320/240/kitten" serta menyimpan log-nya ke file "Foto.log". Karena gambar yang diunduh acak, ada kemungkinan gambar yang sama terunduh lebih dari sekali, oleh karena itu kalian harus menghapus gambar yang sama (tidak perlu mengunduh gambar lagi untuk menggantinya). Kemudian menyimpan gambar-gambar tersebut dengan nama "Koleksi_XX" dengan nomor yang berurutan tanpa ada nomor yang hilang (contoh : Koleksi_01, Koleksi_02, ...)

b. Karena Kuuhaku malas untuk menjalankan script tersebut secara manual, ia juga meminta kalian untuk menjalankan script tersebut sehari sekali pada jam 8 malam untuk tanggal-tanggal tertentu setiap bulan, yaitu dari tanggal 1 tujuh hari sekali (1,8,...), serta dari tanggal 2 empat hari sekali(2,6,...). Supaya lebih rapi, gambar yang telah diunduh beserta log-nya, dipindahkan ke folder dengan nama tanggal unduhnya dengan format "DD-MM-YYYY" (contoh : "13-03-2023").

c. Agar kuuhaku tidak bosan dengan gambar anak kucing, ia juga memintamu untuk mengunduh gambar kelinci dari "https://loremflickr.com/320/240/bunny". Kuuhaku memintamu mengunduh gambar kucing dan kelinci secara bergantian (yang pertama bebas. contoh : tanggal 30 kucing > tanggal 31 kelinci > tanggal 1 kucing > ... ). Untuk membedakan folder yang berisi gambar kucing dan gambar kelinci, nama folder diberi awalan "Kucing_" atau "Kelinci_" (contoh : "Kucing_13-03-2023").

Pertama, kita bisa tentukan sebuah direktori untuk menyimpan folder-folder tersebut. Misal, kita bisa buat sebuah direktori di /home/[username] bernama Koleksi.
```
$ mkdir Koleksi
$ cd Koleksi
```
Kemudian, kita buat direktori untuk foto yang akan diunduh dengan format "Kucing_tanggal-bulan-tahun"
```
$ mkdir $(date "+ Kucing_%d-%m-%Y")
```
Selanjutnya, kita masuk ke direktori tersebut dan mendownload foto kucing dari "https://loremflickr.com/320/240/kitten".
```
$ wget https://loremflickr.com/320/240/kitten
```
Kemudian untuk meng-otomatis-kan semua perintah itu, kita taruh di file soal3c.sh.
```
#! /bin/sh/

cd Koleksi
mkdir $(date "+ Kucing_%d-%m-%Y")
cd $(date "+ Kucing_%d-%m-%Y")
wget https://loremflickr.com/320/240/kitten
cd
```
Karena kita juga harus melakukan hal yang sama untuk kelinci, maka kita buat 2 fungsi didalam soal3c.sh.
```
#! /bin/sh/

function kitten() {
cd Koleksi
mkdir $(date "+ Kucing_%d-%m-%Y")
cd $(date "+ Kucing_%d-%m-%Y")
wget https://loremflickr.com/320/240/kitten
cd
}

function bunny() {
cd Koleksi
mkdir $(date "+ Kelinci_%d-%m-%Y")
cd $(date "+ Kelinci_%d-%m-%Y")
wget https://loremflickr.com/320/240/bunny
cd
}
```
Untuk mengunduh file kucing, kita bisa memanggil fungsinya menggunakan command ```source``` seperti berikut.
```
$ source soal3c.sh; kitten
```
Kemudian, karena kita harus meng-otomatis-kan pengunduhan file kucing dan kelinci dengan hari yang berselang-seling, maka kita tambahkan perintah berikut ini ke crontab.
```
0 0 1-31/2 * * source soal3c.sh; bunny
0 0 2-31/2 * * source soal3c.sh; kitten
```
Maka fungsi akan tereksekusi tiap pukul 00:00, untuk ```bunny``` pada tanggal ganjil, dan untuk ```kitten``` pada tanggal genap.

d. Untuk mengamankan koleksi Foto dari Steven, Kuuhaku memintamu untuk membuat script yang akan memindahkan seluruh folder ke zip yang diberi nama “Koleksi.zip” dan mengunci zip tersebut dengan password berupa tanggal saat ini dengan format "MMDDYYYY" (contoh : “03032003”).

Untuk meng-zip folder ````Koleksi```` menggunakan password berupa ```tanggalbulantahun``` maka kita bisa gunakan command berikut.
```
$ current=$(date "+%d%m%Y")
$ zip -P $current -r Koleksi.zip Koleksi/
```
```-P``` digunakan untuk menambahkan password pada zip, berupa ```current``` yang isinya adalah tanggal hari itu.
```-r``` digunakan agar proses zip dilakukan secara rekursif, sehingga semua subfolder dalam ```Koleksi/``` bisa masuk ke zip.
Hasil dari proses adalah "Koleksi.zip" yang berada di direktori ```/home/[username]/```

e. Karena kuuhaku hanya bertemu Steven pada saat kuliah saja, yaitu setiap hari kecuali sabtu dan minggu, dari jam 7 pagi sampai 6 sore, ia memintamu untuk membuat koleksinya ter-zip saat kuliah saja, selain dari waktu yang disebutkan, ia ingin koleksinya ter-unzip dan tidak ada file zip sama sekali.


