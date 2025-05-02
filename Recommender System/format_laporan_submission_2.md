# Laporan Proyek Machine Learning - Marchio Apriadi

## Project Overview

eiring dengan pesatnya perkembangan teknologi smartphone, pilihan produk yang tersedia di pasar menjadi semakin banyak dan beragam. Setiap pengguna memiliki preferensi unik berdasarkan kebutuhan personal, seperti performa perangkat, kapasitas kamera, ukuran baterai, hingga harga. Akibatnya, konsumen kerap mengalami kesulitan dalam memilih smartphone yang paling sesuai dengan kebutuhan mereka. Oleh karena itu, sistem rekomendasi berbasis data menjadi solusi penting untuk membantu pengguna menemukan produk yang paling relevan dengan preferensi mereka. 

Proyek ini bertujuan untuk membangun sistem rekomendasi smartphone dengan pendekatan content-based filtering dan collaborative filtering. Content-based filtering akan merekomendasikan smartphone berdasarkan kesamaan spesifikasi (fitur produk) yang pernah disukai pengguna dan Collaborative filtering akan memberikan rekomendasi berdasarkan preferensi pengguna lain yang memiliki pola perilaku serupa.

## Business Understanding

### Problem Statements
- **Tantangan Personalisasi Fitur Ponsel:** Bagaimana cara merekomendasikan ponsel pintar berdasarkan kemiripan fitur dengan preferensi pengguna sebelumnya?
- **Tantangan Personalisasi Penjualan** Bagaimana pola preferensi pengguna lain dapat membantu merekomendasikan ponsel pintar yang relevan?
  
### Goals
- Dengan menganalisis fitur-fitur ponsel pintar yang paling disukai oleh pengguna dan pola preferensi mereka, dapat membantu dalam pengembangan sistem rekomendasi berbasis fitur yang lebih baik dan sesuai dengan minat penggguna
- Analisis pola interaksi dan rating antar pengguna terhadap berbagai ponsel pintar dapat memberikan gambaran tentang preferensi kolektif dan kemiripan selera, sehingga dapat membantu dalam pengembangan sistem rekomendasi yang lebih efektif dan mengikuti preferensi pengguna lain yang serupa.
- Penyajian rekomendasi ponsel pintar yang dipersonalisasi berdasarkan kedua pendekatan dapat memberikan nilai tambah bagi pengguna dalam menemukan perangkat yang relevan dengan kebutuhan dan preferensi mereka.
  
### Solution statements
- Content-Based Filtering: Menganalisis fitur-fitur ponsel (merek, spesifikasi, harga, dll.) dan riwayat rating pengguna untuk merekomendasikan ponsel yang serupa dengan yang telah disukai pengguna.
- Collaborative Filtering (Neural Network): Membangun model jaringan saraf yang mempelajari pola interaksi pengguna-item (rating) untuk memprediksi preferensi dan merekomendasikan ponsel berdasarkan pengguna lain yang memiliki selera yang mirip.

## Data Understanding
### URL/tautan sumber data
Dataset yang digunakan dalam proyek ini adalah dataset https://www.kaggle.com/datasets/meirnizri/cellphones-recommendations yang terdiri dari tiga file utama:
- cellphones data.csv: Berisi informasi mengenai 34 ponsel pintar populer di AS pada tahun 2022. Setiap ponsel memiliki 13 fitur utama, termasuk performa (berdasarkan skor AnTuTu), ukuran memori, resolusi kamera, kapasitas baterai, ukuran layar, tanggal rilis, dan harga.
- cellphones users.csv: Mengandung informasi demografis pengguna yang berpartisipasi dalam survei, termasuk usia, jenis kelamin, dan pekerjaan.
- cellphones ratings.csv: Berisi data rating yang diberikan oleh pengguna melalui survei di Mechanical Turk. Setiap peserta melihat 10 ponsel acak dan memberikan rating seberapa besar kemungkinan mereka akan membeli setiap ponsel dengan harga yang diberikan, pada skala 1 (sangat tidak mungkin) hingga 10 (sangat mungkin).

Variabel-variabel pada dataset adalah sebagai berikut :

**cellphones data.csv**
- cellphone_id: Identifikasi unik untuk setiap ponsel pintar.
- brand: Merek ponsel pintar.
- model: Nama model ponsel pintar.
- operating system: Sistem operasi yang digunakan ponsel.
- internal memory: Kapasitas memori internal ponsel (GB).
- RAM: Kapasitas Random Access Memory (GB).
- performance: Skor performa ponsel .
- main camera: Resolusi kamera utama (MP).
- selfie camera: Resolusi kamera depan (MP).
- battery size: Kapasitas baterai (mAh).
- screen size: Ukuran layar (inci).
- weight: Berat ponsel (gram).
- price: Harga ponsel (Dollar).
- release date: Tanggal rilis ponsel.
  
**cellphones rating.csv**
- user_id: Identifikasi unik untuk setiap pengguna.
- cellphone_id: Identifikasi unik untuk setiap ponsel pintar.
- rating: Tingkat kemungkinan pembelian yang diberikan pengguna(1-10).

**cellphones users.csv**
- user_id: Identifikasi unik untuk setiap pengguna.
- age: Usia pengguna.
- gender: Jenis kelamin pengguna.
- occupation: Pekerjaan pengguna.

Pada tahapan ini dilakukan Analisis statistik deskriptif (mean, median, standar deviasi, dll.) dan juga Pengecekan Unique Value untuk mendapatkan pemahaman tentang karakteristik data 
### Analisis statistik deskriptif
Dengan menggunakan fungsi describe(), didapatkan hasil pada masing-masing data seperti berikut :

**cellphones data.csv**

<img src="https://github.com/user-attachments/assets/633cb824-bcd0-410a-a95a-577869fe9f35" alt="Hasil describe() data hp" style="float: left; margin-right: 15px; width: auto; height: auto;">

Data Numerik:
- internal memory: Kapasitas penyimpanan internal ponsel. Rentangnya dari 8 hingga 512, dengan rata-rata sekitar 146.
- RAM: Kapasitas memori RAM   Rentangnya dari 3 hingga 12, dengan rata-rata sekitar 6.8.
- performance: Skor atau rating performa ponsel. Rentangnya dari 1.02 hingga 11, dengan rata-rata sekitar 6.2.
- main camera: Resolusi kamera utama. Rentangnya dari 12 hingga 108, dengan rata-rata sekitar 41.
- selfie camera: Resolusi kamera depan. Rentangnya dari 4 hingga 40, dengan rata-rata sekitar 15.
- battery size: Kapasitas baterai. Rentangnya dari 2018 hingga 5003, dengan rata-rata sekitar 4321.
- screen size: Ukuran layar. Rentangnya dari 4.7 hingga 7.6, dengan rata-rata sekitar 6.4.
- weight: Berat ponsel. Rentangnya dari 141 hingga 271, dengan rata-rata sekitar 197.
- price: Harga ponsel. Rentangnya dari 129 hingga 1998, dengan rata-rata sekitar 628.
  
Data Kategorikal:
- brand: Merek ponsel. Terdapat 10 merek unik, dengan "Samsung" menjadi merek yang paling sering muncul (8 kali).
- model: Nama model ponsel. Terdapat 33 model unik, yang berarti setiap baris kemungkinan besar mewakili model yang berbeda. "iPhone SE (2022)" adalah model yang paling sering muncul.
- operating system: Sistem operasi ponsel. Terdapat 2 sistem operasi unik, dengan "Android" menjadi yang paling sering muncul (27 kali).
release date: Tanggal rilis ponsel. Terdapat 26 tanggal rilis yang berbeda, dengan "24/09/2021" menjadi tanggal yang paling sering muncul (4 kali).

**cellphones rating.csv**

<img src="https://github.com/user-attachments/assets/11b28d7f-dd1f-46c4-be6f-819d6d241b26" alt="Hasil descrribe() data rating" style="float: left; margin-right: 15px; width: auto; height: auto;">

- Rating terendah adalah 1 dan rating tertinggi adalah 18
- Rata-rata rating adalah 6.7. 
  
**cellphones users.csv**

<img src="https://github.com/user-attachments/assets/eddd05c6-ca20-40da-9f75-c260cbabfd8f" alt="Hasil descrribe() data users" style="float: left; margin-right: 15px; width: auto; height: auto;">

Data Numerik:
- age: Terdapat 99 data usia penggun dengan rata-rata usia pengguna adalah sekitar 36 tahun. Usia pengguna termuda adalah 21 tahun dan usia pengguna tertua adalah 61 tahun.

Data Kategorikal
- gender: Terdapat 3 kategori jenis kelamin yang berbeda. Kategori jenis kelamin yang paling sering muncul adalah "Male" (Laki-laki) sebanyak 50 kali.
- occupation: Terdapat 56 jenis pekerjaan yang berbeda. Pekerjaan yang paling sering muncul adalah "Information Technology" (Teknologi Informasi) sebanyak 10 kali.

### uniqe_values

**cellphones data.csv**
```
Nilai unik dari DataFrame 'cellphones':

Kolom 'cellphone_id':
[ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23
 24 25 26 27 28 29 30 31 32]

Kolom 'brand':
['Apple' 'Asus' 'Samsung' 'Google' 'OnePlus' 'Oppo' 'Vivo' 'Xiaomi' 'Sony'
 'Motorola']

Kolom 'model':
['iPhone SE (2022)' 'iPhone 13 Mini' 'iPhone 13' 'iPhone 13 Pro'
 'iPhone 13 Pro Max' 'iPhone XR' 'Zenfone 8' 'Galaxy A13' 'Galaxy A32'
 'Galaxy A53' 'Galaxy S22' 'Galaxy S22 Plus' 'Galaxy S22 Ultra'
 'Galaxy Z Flip 3' 'Galaxy Z Fold 3' 'Pixel 6 \xa0' 'Pixel 6a'
 'Pixel 6 Pro\xa0' 'Nord N20' 'Nord 2T' '10 Pro' '10T' 'Find X5 Pro'
 'X80 Pro' 'Redmi Note 11' '11T Pro' '12 Pro' 'Poco F4' 'Xperia Pro'
 'Moto G Stylus (2022)' 'Moto G Play (2021)' 'Moto G Pure'
 'Moto G Power (2022)']

Kolom 'operating system':
['iOS' 'Android']

Kolom 'internal memory':
[128 256  64  32 512]

Kolom 'RAM':
[ 4  6  3  8 12]

Kolom 'performance':
[ 7.23  7.72  7.75  7.94  8.01  4.22  6.76  1.36  2.2   3.79  8.81  7.22
  9.68  5.96  6.35  6.88  7.19  3.8   6.04  8.86 11.   10.12  9.81  2.44
  7.59  9.85  6.98  6.82  2.3   1.42  1.02  1.35]

Kolom 'main camera':
[ 12  64  50  48 108  13]

Kolom 'selfie camera':
[ 7 12  8 13 32 10 40  4 11 16 20  5]

Kolom 'battery size':
[2018 2438 3240 3065 4352 2942 4000 5000 3700 4500 3300 4400 4614 4410
 5003 4800 4700 4600]

Kolom 'screen size':
[4.7 5.4 6.1 6.7 5.9 6.6 6.5 6.8 7.6 6.4]

Kolom 'weight':
[144 141 174 204 240 194 169 196 205 189 167 195 228 183 271 207 178 210
 173 190 201 218 215 179 225 188 203]

Kolom 'price':
[ 429  699  999 1199  236  599  154  199  312  528  899  840 1799  499
  449  299  379  780  649  987  872  174  435  618  428 1998  500  159
  129  189]

Kolom 'release date':
['18/03/2022' '24/09/2021' '26/10/2018' '12/05/2021' '23/03/2022'
 '22/01/2021' '24/03/2022' '25/02/2022' '11/08/2021' '28/10/2021'
 '21/07/2021' '28/04/2022' '21/05/2022' '11/01/2022' '06/08/2022'
 '14/03/2022' '29/04/2022' '09/02/2022' '05/10/2021' '31/12/2021'
 '27/07/2022' '27/01/2021' '27/04/2022' '14/01/2021' '14/10/2021'
 '22/02/2022']
```

**cellphones rating.csv**
```
Nilai unik dari DataFrame 'rating':

Kolom 'user_id':
[  0   1   6   8  10  12  16  24  25  26  27  28  29  30  32  33  35  36
  37  38  52  53  56  60  74  79  80  84  85  91  95  98  99 100 104 105
 106 110 111 112 113 114 115 116 119 120 123 124 126 128 129 137 140 142
 143 144 145 148 152 154 156 160 162 164 169 178 183 194 200 203 204 208
 211 215 226 227 230 231 232 233 234 235 236 237 238 240 242 243 244 245
 246 251 252 253 254 255 256 257 258]

Kolom 'cellphone_id':
[30  5 10  9 23  8 22 16 19  3  7 31 18 32 28 15  4 13  1 27 29 25 20  0
 11 17 21  6 14 12 24 26  2]

Kolom 'rating':
[ 1  3  9  2 10  8  7  5  6  4 18]
```

**cellphones users.csv**
```
Nilai unik dari DataFrame 'users':

Kolom 'user_id':
[  0   1   6   8  10  12  16  24  25  26  27  28  29  30  32  33  35  36
  37  38  52  53  56  60  74  79  80  84  85  91  95  98  99 100 104 105
 106 110 111 112 113 114 115 116 119 120 123 124 126 128 129 137 140 142
 143 144 145 148 152 154 156 160 162 164 169 178 183 194 200 203 204 208
 211 215 226 227 230 231 232 233 234 235 236 237 238 240 242 243 244 245
 246 251 252 253 254 255 256 257 258]

Kolom 'age':
[38 40 55 25 23 28 31 57 27 29 33 61 34 39 30 41 42 50 48 43 32 36 37 56
 46 49 21 35 58 45]

Kolom 'gender':
['Female' 'Male' '-Select Gender-']

Kolom 'occupation':
['Data analyst' 'team worker in it' 'IT' 'Manager' 'worker' 'Accountant'
 'sales' 'it' 'Team leader' 'FINANCE' 'Finance' 'Sales' 'Ops Manager'
 'ICT Officer' 'QA Software Manager' 'Healthcare' 'self employed'
 'banking' 'nurse' 'executive' 'software developer' nan 'manager'
 'Warehousing' 'WEB DESIGN' 'Information Technology' 'Technical Engineer'
 'information' 'Administrator' 'System Administrator' 'Marketing'
 'EDUCATION' 'Security' 'retail' 'technician' 'homemaker' 'teacher'
 'president transportation company' 'ADMINISTRATIVE OFFICER'
 'Information technology' 'master degree' 'construction' 'accountant'
 'team leader' 'Administrative officer' 'SALES MANAGER' 'Purchase Manager'
 'writer' 'registered' 'business' 'Transportation' 'Education' 'HEALTHARE'
 'MANAGER' 'HEALTHCARE' 'Computer technician' 'Executive Manager']
```

berdasarkan proses diatas, terdapat beberapa point penting yang dapat dilakukan untuk proses selanjutnya:
- fitur rating, terdapat nilai 18 (seharusnya max 10)
- fitur model, terdapat inkonsistensi pada data karena adanya penggunaan tahun walaupun fitur releas date sudah ada
- fitur date, merubah tipe data tanggal
- fitur gender, 'select gender' akan diubah menjadi unknown
- fitur occupation, banyak nya nilai uniqe yang bermakna sama dan juga banyak data yang tidak konsisten.



## Data Preparation
### merge data
Penggabungan data ini dilakukan agar tiap fitur akan memiliki informasi yang lebih berkesinambungan yang akan meningkatkan keakurasian dari hasil sistem rekomendasi sehingga memungkinkan agar hasil rekomendasi ini lebih berfokus pada personal recommendation

<img src="https://github.com/user-attachments/assets/78e5259d-71db-4c8a-a420-f13f940905b6" alt="merge data" style="float: left; margin-right: 15px; width: auto; height: auto;">

### Perbaikan beberapa fitur

**fitur rating**

Membatasi nilai dalam kolom 'rating' antara 1 dan 10 dengan fungsi clip()
```
Statistik kolom 'rating' setelah perbaikan di df_preparation:
count    990.000000
mean       6.691919
std        2.616552
min        1.000000
25%        5.000000
50%        7.000000
75%        9.000000
max       10.000000
Name: rating, dtype: float6
```

**Fitur Gender**

Nilai '-Select Gender-' kemungkinan merupakan nilai placeholder atau nilai default yang muncul ketika pengguna tidak memilih jenis kelamin secara spesifik. Menggantinya dengan 'Unknown' menciptakan representasi yang lebih standar dan konsisten untuk data yang tidak teridentifikasi\.
```
df_preparation['gender'] = df_preparation['gender'].replace('-Select Gender-', 'Unknown')

['Female' 'Male' 'Unknown']
```

**Fitur Occupation**

Mengelompokkan dan menstandarkan berbagai jenis pekerjaan (occupation) ke dalam kategori yang lebih umum dan terstruktur. Ini dilakukan dengan menggunakan sebuah mapping dictionary (occupation_mapping). Berikut adalah hasil akhirnya
```
['Data analyst' 'IT' 'Manager' 'Other' 'Finance' 'Sales' 'ICT Officer'
 'Healthcare' 'Executive' 'Unknown' 'Technical Engineer' 'Admin'
 'Marketing' 'Education' 'Technical' 'Transportation']
```

**fitur release date**

Selanjutnya adalah melakukan perubahan format data pada kolom 'release date' menjadi tipe data datetime yang dikenali oleh Pandas dengan menggunakan fungsi to_datetime(). Berikut adalah hasilnya
```
Nilai unik dan tipe data kolom 'release date' setelah konversi:
<DatetimeArray>
['2021-01-14 00:00:00', '2018-10-26 00:00:00', '2022-02-25 00:00:00',
 '2022-03-24 00:00:00', '2022-04-29 00:00:00', '2021-01-22 00:00:00',
 '2022-03-14 00:00:00', '2021-07-21 00:00:00', '2022-05-21 00:00:00',
 '2021-09-24 00:00:00', '2022-03-23 00:00:00', '2021-10-14 00:00:00',
 '2022-04-28 00:00:00', '2022-02-22 00:00:00', '2021-01-27 00:00:00',
 '2021-10-28 00:00:00', '2021-08-11 00:00:00', '2022-07-27 00:00:00',
 '2022-04-27 00:00:00', '2021-10-05 00:00:00', '2022-01-11 00:00:00',
 '2022-03-18 00:00:00', '2022-08-06 00:00:00', '2021-05-12 00:00:00',
 '2022-02-09 00:00:00', '2021-12-31 00:00:00']
Length: 26, dtype: datetime64[ns]
datetime64[ns]
```

**fitur model**

membersihkan dan menstandarkan data pada kolom 'model' dengan melakukan dua jenis penggantian string
- Mengganti non-breaking space : Menggantinya dengan spasi biasa memastikan konsistensi dan mencegah kesalahan saat membandingkan atau menganalisis nama model.
- Menghapus informasi tahun yang berada di dalam tanda kurung: membersihkan nama model dari informasi tahun rilis, yang sebenarnya sudah ada di fitur release date
```
Nilai unik kolom 'model' setelah menghapus tahun:
['Moto G Play' 'iPhone XR' 'Galaxy S22' 'Galaxy A53' 'X80 Pro'
 'Galaxy A32' 'Find X5 Pro' 'Pixel 6a' 'Nord 2T' 'iPhone 13 Pro'
 'Galaxy A13' 'Moto G Pure' 'Nord N20' 'Moto G Power' 'Xperia Pro'
 'Pixel 6' 'iPhone 13 Pro Max' 'Galaxy Z Flip 3' 'iPhone 13 Mini'
 'Poco F4' 'Moto G Stylus' '11T Pro' '10 Pro' 'iPhone SE'
 'Galaxy S22 Plus' 'Pixel 6 Pro' '10T' 'Zenfone 8' 'Galaxy Z Fold 3'
 'Galaxy S22 Ultra' 'Redmi Note 11' '12 Pro' 'iPhone 13']
```

## Modeling

**Content-Based Filtering**

Membuat profil item (ponsel) berdasarkan rata-rata fitur-fitur numerik yang telah di-scaling dan fitur kategorikal yang telah di-encode. Profil pengguna dibuat berdasarkan rata-rata profil item yang telah diberi rating tinggi oleh pengguna. Rekomendasi dihasilkan berdasarkan cosine similarity antara profil pengguna dan profil semua item yang belum di-rating. Berikut adalah hasilnya
```
Rekomendasi Content-Based untuk User ID 1:
            model  similarity
3          12 Pro    0.298273
13    Moto G Play    0.252409
16  Moto G Stylus    0.251552
22        Poco F4    0.242491
24        X80 Pro    0.23719
```

**collaborative filtering**

Membangun model jaringan saraf (RecommenderNetV2) dengan lapisan embedding untuk pengguna dan item, diikuti oleh lapisan dense dengan aktivasi ReLU dan lapisan dropout. Model dilatih untuk memprediksi rating yang dinormalisasi (skala 0-1 setelah rating asli dibagi 10 dan diskalakan). Rekomendasi dihasilkan dengan memprediksi rating untuk item yang belum di-rating oleh pengguna dan memilih top-N dengan prediksi tertinggi.

<img src="https://github.com/user-attachments/assets/2abb2bbf-9bff-4fb8-a2ee-b598c2046169" alt="model cf" style="float: left; margin-right: 15px; width: auto; height: auto;">


## Evaluation
Kinerja model Neural CF dievaluasi menggunakan Loss dan Root Mean Squared Error (RMSE) pada set pengujian, yang mengukur perbedaan antara rating prediksi dan rating sebenarnya (setelah diskalakan).

```
Loss on test set (Neural CF): 0.7939
RMSE on test set (Neural CF): 0.8909
```

berikut adalah hasil visualisasi dari proses pelatihan model
<img src="https://github.com/user-attachments/assets/8c47b631-3c00-46f9-a37e-92711c7de88c" alt="eval cf" style="float: left; margin-right: 15px; width: auto; height: auto;">



