# Laporan Proyek Machine Learning - Marchio Apriadi


## Project Overview


Seiring dengan pesatnya perkembangan teknologi smartphone, pilihan produk yang tersedia di pasar menjadi semakin banyak dan beragam. Setiap pengguna memiliki preferensi unik berdasarkan kebutuhan personal, seperti performa perangkat, kapasitas kamera, ukuran baterai, hingga harga. Akibatnya, konsumen kerap mengalami kesulitan dalam memilih smartphone yang paling sesuai dengan kebutuhan mereka. Oleh karena itu, sistem rekomendasi berbasis data menjadi solusi penting untuk membantu pengguna menemukan produk yang paling relevan dengan preferensi mereka. 


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


### Sumber data


Dataset yang digunakan dalam proyek ini bersumber pada : https://www.kaggle.com/datasets/meirnizri/cellphones-recommendations yang terdiri dari tiga file utama:
- cellphones data.csv: Berisi informasi mengenai 33 ponsel pintar populer di AS pada tahun 2022. Terdapat 14 fitur pada dataset ini, seperti performa (berdasarkan skor AnTuTu), ukuran memori, resolusi kamera, kapasitas baterai, ukuran layar, tanggal rilis, dan harga.
- cellphones users.csv: Mengandung informasi mengenai 99 pengguna seperti usia, jenis kelamin, dan pekerjaan.
- cellphones ratings.csv: Berisi 990 data rating yang diberikan oleh pengguna. Setiap peserta melihat 10 ponsel acak dan memberikan rating seberapa besar kemungkinan mereka akan membeli setiap ponsel dengan harga yang diberikan, pada skala 1 (sangat tidak mungkin) hingga 10 (sangat mungkin).

### Informasi variabel masing-masing data


Variabel-variabel pada dataset adalah sebagai berikut :


**cellphones data.csv**

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 33 entries, 0 to 32
Data columns (total 14 columns):
 #   Column            Non-Null Count  Dtype  
---  ------            --------------  -----  
 0   cellphone_id      33 non-null     int64  
 1   brand             33 non-null     object 
 2   model             33 non-null     object 
 3   operating system  33 non-null     object 
 4   internal memory   33 non-null     int64  
 5   RAM               33 non-null     int64  
 6   performance       33 non-null     float64
 7   main camera       33 non-null     int64  
 8   selfie camera     33 non-null     int64  
 9   battery size      33 non-null     int64  
 10  screen size       33 non-null     float64
 11  weight            33 non-null     int64  
 12  price             33 non-null     int64  
 13  release date      33 non-null     object 
dtypes: float64(2), int64(8), object(4)
memory usage: 3.7+ KB
```
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
- tidak ditemukan adannya missing value.
  
  
**cellphones rating.csv**

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 990 entries, 0 to 989
Data columns (total 3 columns):
 #   Column        Non-Null Count  Dtype
---  ------        --------------  -----
 0   user_id       990 non-null    int64
 1   cellphone_id  990 non-null    int64
 2   rating        990 non-null    int64
dtypes: int64(3)
memory usage: 23.3 KB
```

- user_id: Identifikasi unik untuk setiap pengguna.
- cellphone_id: Identifikasi unik untuk setiap ponsel pintar.
- rating: Tingkat kemungkinan pembelian yang diberikan pengguna(1-10).
- tidak ditemukan adanya missing value
  

**cellphones users.csv**

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 99 entries, 0 to 98
Data columns (total 4 columns):
 #   Column      Non-Null Count  Dtype 
---  ------      --------------  ----- 
 0   user_id     99 non-null     int64 
 1   age         99 non-null     int64 
 2   gender      99 non-null     object
 3   occupation  98 non-null     object
dtypes: int64(2), object(2)
memory usage: 3.2+ KB
```

- user_id: Identifikasi unik untuk setiap pengguna.
- age: Usia pengguna.
- gender: Jenis kelamin pengguna.
- occupation: Pekerjaan pengguna.
- tidak ditemukan adanya missing value


### Analisis statistik deskriptif


Pada tahapan ini dilakukan Analisis statistik deskriptif (mean, median, standar deviasi, dll.) dan juga Pengecekan Unique Value untuk mendapatkan pemahaman tentang karakteristik data 
Dengan menggunakan fungsi describe(), didapatkan hasil pada masing-masing data seperti berikut :


### cellphones data.csv


<img src="https://github.com/user-attachments/assets/633cb824-bcd0-410a-a95a-577869fe9f35" alt="hp_desc()" style="float: left; margin-right: 15px; width: auto; height: auto;">


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


### cellphones rating.csv


<img src="https://github.com/user-attachments/assets/11b28d7f-dd1f-46c4-be6f-819d6d241b26" alt="rating_desc()" style="float: left; margin-right: 15px; width: auto; height: auto;">


- Rating terendah adalah 1 dan rating tertinggi adalah 18
- Rata-rata rating adalah 6.7.
  
  
### cellphones users.csv


<img src="https://github.com/user-attachments/assets/eddd05c6-ca20-40da-9f75-c260cbabfd8f" alt="user_desc()" style="float: left; margin-right: 15px; width: auto; height: auto;">


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


**DATA PREPARATION CONTENT BASED**


Mempersiapkan data agar sesuai untuk digunakan dalam model Content-Based Filtering. Fokusnya adalah pada pembuatan representasi fitur untuk setiap item (ponsel) berdasarkan atribut-atributnya. Beberapa proses yang dilakukan adalah :


- Penghapusan duplikasi berdasarkan spesifikasi, karena satu ponsel bisa muncul beberapa kali dari user berbeda.


```
phone_cols = ['cellphone_id', 'brand', 'model', 'operating system', 'internal memory',
              'RAM', 'performance', 'main camera', 'selfie camera', 'battery size',
              'screen size', 'weight', 'price']

df_unique_phones = df[phone_cols].drop_duplicates().reset_index(drop=True)
```

  
- Penggabungan kolom brand, model, dan operating system menjadi satu teks untuk mewakili fitur kategorikal.


```
df_unique_phones['combined_text'] = df_unique_phones[['brand', 'model', 'operating system']].agg(' '.join, axis=1)
```


- fitur kategorikal diubah menjadi vektor angka menggunakan TfidfVectorizer.


```
tfidf = TfidfVectorizer()
X_text = tfidf.fit_transform(df_unique_phones['combined_text'])
```


- Fitur Numerik yang Di-scaling sehingga memiliki nilai dalam rentang antara 0 dan 1 dengan menggunakan StandardScaler.


```
scaler = StandardScaler()
X_num = scaler.fit_transform(df_unique_phones[numeric_features])
```


- menggabungkan hasil TF-IDF (teks) dan fitur numerik menjadi satu vektor menggunakan hstack()


```
X_all = hstack([X_text, X_num])
```


- Mengambil indeks dari ponsel yang paling mirip berdasarkan urutan skor similarity.


<img src="https://github.com/user-attachments/assets/24cabd53-80f8-46e2-a299-448a117cc769" alt="cb_process" style="float: left; margin-right: 15px; width: auto; height: auto;">


**DATA PREPARATION COLLABORATIVE FILLTERING**


Mempersiapkan data untuk tugas collaborative filtering menggunakan model neural network. Langkah-langkah utamanya adalah:


- Mengubah ID pengguna dan item menjadi indeks numerik berurutan menggunakan LabelEncoder()
  
  ```
  user_encoder = LabelEncoder()
  df_preparation['user_index'] = user_encoder.fit_transform(df_preparation['user_id'])
  item_encoder = LabelEncoder()
  df_preparation['item_index'] = item_encoder.fit_transform(df_preparation['cellphone_id'])
  ```

  
- Membagi data menjadi set pelatihan dan pengujian menggunakan train_test_split.
  
  ```
  train_df, test_df = train_test_split(df_preparation, test_size=0.2, random_state=42)
  ```

  
- Membuat TensorFlow Dataset yang efisien untuk memproses data selama pelatihan dan evaluasi model.
  
  ```
  train_dataset = create_tf_dataset(train_df).batch(64).prefetch(tf.data.AUTOTUNE)
  test_dataset = create_tf_dataset(test_df).batch(64).prefetch(tf.data.AUTOTUNE)
  ```

  
- Menskalakan nilai rating ke rentang 0-1.
  
  ```
  ratings = df['rating'].values.astype(np.float32) / 5.0
  ```


## Model Development


### Content-Based Filtering


**Model-Development**


Membangun fungsi rekomendasi menggunakan Fungsi recommend()  untuk memberikan rekomendasi ponsel yang paling mirip dengan ponsel tertentu berdasarkan cellphone_id. Sistem ini menggunakan pendekatan Content-Based Filtering dengan mengukur kemiripan fitur antar ponsel menggunakan Cosine Similarity. Fungsi ini mencari ponsel yang paling relevan dari segi spesifikasi dan mengembalikan daftar ponsel yang paling mirip.


```
idx = df_unique_phones[df_unique_phones['cellphone_id'] == cellphone_id].index[0]
sim_scores = list(enumerate(similarity_matrix[idx]))
sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)[1:top_n+1]
recommended_indices = [i[0] for i in sim_scores]
```


**Rekomendasi Content Based**


Dilakukan pengimplementasian sistem rekomendasi content-based filtering dengan memanggil kembali fungsi recommend() untuk mendapatkan top-N cellphone yang memiliki kemiripan fitur yang serupa. Berikut adalah hasilnya (unutk cellphone_id = 11)


<img src="https://github.com/user-attachments/assets/af939a9b-a2f1-4a60-83a0-4a214f118564" alt="cb_rec" style="float: left; margin-right: 15px; width: auto; height: auto;">


### Collaborative filtering


Membangun model jaringan saraf (RecommenderNetV2) dengan lapisan embedding untuk pengguna dan item, diikuti oleh lapisan dense dengan aktivasi ReLU dan lapisan dropout. Model dilatih untuk memprediksi rating yang dinormalisasi (skala 0-1 setelah rating asli dibagi 10 dan diskalakan). Rekomendasi dihasilkan dengan memprediksi rating untuk item yang belum di-rating oleh pengguna dan memilih top-N dengan prediksi tertinggi.


**modelling**


RecommenderNetV2: Model Neural Collaborative Filtering (RecommenderNetV2) dirancang dengan pendekatan embedding untuk user dan item, lalu diproses melalui dua layer dense bertingkat yang masing-masing diikuti oleh dropout untuk mencegah overfitting. Model ini menggunakan aktivasi ReLU dan output akhir menggunakan fungsi sigmoid untuk prediksi rating. Regularisasi L2 juga diterapkan pada embedding untuk menjaga kestabilan pelatihan.


```
self.dense_1 = layers.Dense(hidden_units, activation='relu')
self.dropout_1 = layers.Dropout(dropout_rate)
self.dense_output = layers.Dense(1, activation='sigmoid')
```


**compile dan train**


Menginstansiasi model RecommenderNetV2 dengan konfigurasi tertentu (ukuran embedding, jumlah hidden unit, dropout rate), mengompilasinya dengan optimizer, fungsi loss, dan metrik yang sesuai, serta melatihnya dengan data yang telah disiapkan menggunakan early stopping untuk mencegah overfitting dan mendapatkan model dengan kinerja terbaik.


```
model.compile(
    optimizer=tf.keras.optimizers.Adam(learning_rate=0.0005),
    loss='mse',
    metrics=[tf.keras.metrics.RootMeanSquaredError()]
)

early_stopping = tf.keras.callbacks.EarlyStopping(
    monitor='val_loss', patience=5, restore_best_weights=True
)
```


**Rekomendasi Collaborative Filltering**


Menghasilkan rekomendasi HP yang dipersonalisasi untuk pengguna berdasarkan preferensi pengguna lain yang serupa, menggunakan model Neural Collaborative Filtering yang telah dilatih. Fungsi recommend_top_n_neural_cf_final_unique_simplified bertugas untuk menghasilkan Top-N rekomendasi HP untuk seorang pengguna berdasarkan model Neural Collaborative Filtering.


```
# Memprediksi item yang belum dirating oleh user
user_input = np.expand_dims(np.array([user_index] * len(items_to_predict)), axis=1)
item_input = np.expand_dims(items_to_predict, axis=1)
predictions = model.predict(np.concatenate([user_input, item_input], axis=1))

# Menyusun hasil rekomendasi
top_n_indices = np.argsort(predictions, axis=0)[::-1][:top_n].flatten()

```


## Evaluation


### Evaluasi Content Base filltering


Evaluasi sistem rekomendasi Content Base filltering dilakukan menggunakan metrik Precision@5, yang mengukur seberapa banyak dari lima rekomendasi teratas yang benar-benar relevan untuk pengguna. Dalam konteks ini, relevansi ditentukan berdasarkan apakah pengguna sebelumnya pernah memberikan rating tinggi (≥7) untuk ponsel yang juga muncul dalam hasil rekomendasi. 


```
Precision@5 Rata-rata: 0.20404040404040408
```


### Kesimpulan 


Dari hasil evaluasi, diperoleh Precision@5 rata-rata sebesar 0.204, yang berarti sekitar 20% dari rekomendasi yang diberikan tergolong relevan secara personalisasi. Ini memberikan gambaran awal terhadap efektivitas sistem rekomendasi berbasis konten, dimana hal ini menunjukkan bahwa sistem merekomendasikan sekitar 1 dari 5 ponsel dengan tepat, berdasarkan preferensi pengguna sebelumnya.


### Evaluasi Collaborative filltering


Hasil top-10 recommendation berbasis sistem rekomendasi Collaborative Filtering berbasis Neural Network, berikut adalah evaluasi yang dapat dipaparkan :


<img src="https://github.com/user-attachments/assets/76ea16ff-b594-41dd-9b87-0828fa44db84" alt="top-10" style="float: left; margin-right: 15px; width: auto; height: auto;">


berdasarkan prediksi kecocokan pengguna terhadap ponsel, dalam skala 0 hingga 1, dengan nilai lebih tinggi menunjukkan kecocokan yang lebih besar dengan preferensi pengguna. Sebagai contoh, ponsel pertama yang direkomendasikan adalah OnePlus 10 Pro, dengan prediksi rating 0.975440, yang menunjukkan bahwa ponsel ini memiliki tingkat kecocokan yang sangat tinggi dengan preferensi pengguna 245.


Kinerja model Neural CF dievaluasi menggunakan Loss dan Root Mean Squared Error (RMSE) pada set pengujian, yang mengukur perbedaan antara rating prediksi dan rating sebenarnya (setelah diskalakan).



```
Loss on test set (Neural CF): 0.7939
RMSE on test set (Neural CF): 0.8909
```


berikut adalah hasil visualisasi dari proses pelatihan model


<img src="https://github.com/user-attachments/assets/8c47b631-3c00-46f9-a37e-92711c7de88c" alt="eval cf" style="float: left; margin-right: 15px; width: auto; height: auto;">


### Kesimpulan 


Penjelasan Metrik Evaluasi:


Loss (0.7939):
- Loss adalah ukuran seberapa jauh prediksi yang dihasilkan oleh model dari nilai yang sebenarnya. Dalam hal ini, loss mengukur kesalahan antara prediksi rating yang dihasilkan model untuk ponsel dan rating aktual yang diinginkan (dari data uji).
- Semakin kecil nilai loss, semakin baik model dalam membuat prediksi yang sesuai dengan preferensi pengguna.
- Dalam konteks ini, loss sebesar 0.7939 menunjukkan bahwa model memiliki tingkat kesalahan tertentu dalam memprediksi rating ponsel yang relevan untuk pengguna. Model ini bekerja dengan cukup baik, tetapi masih ada ruang untuk perbaikan agar lebih akurat.
  

Root Mean Squared Error (RMSE) (0.8909):
- RMSE adalah akar dari rata-rata kuadrat selisih antara prediksi dan nilai sebenarnya, yang memberikan gambaran yang lebih jelas tentang besarnya kesalahan prediksi.
- Nilai RMSE yang lebih rendah menunjukkan bahwa model lebih baik dalam memprediksi rating atau preferensi pengguna. Dengan RMSE sebesar 0.8909, model ini menunjukkan kesalahan prediksi yang relatif kecil, tetapi masih ada perbedaan antara prediksi yang diberikan model dan preferensi sesungguhnya.
- Dalam konteks rekomendasi ponsel, RMSE yang lebih rendah menunjukkan bahwa model bisa lebih akurat dalam merekomendasikan ponsel yang relevan berdasarkan pola preferensi pengguna lain.


Model Collaborative Filtering berusaha memahami pola preferensi pengguna lain, yaitu dengan melihat bagaimana pengguna yang memiliki selera atau preferensi yang mirip memberikan rating pada ponsel. Semakin baik model dalam memprediksi rating ini (ditunjukkan dengan nilai loss dan RMSE yang rendah), semakin relevan rekomendasi ponsel yang diberikan kepada pengguna tertentu.


Metrik seperti loss dan RMSE mencerminkan seberapa baik model memahami preferensi pengguna berdasarkan data yang ada. Jika loss dan RMSE semakin kecil, ini berarti model lebih berhasil dalam meniru pola preferensi pengguna lain dan memberikan rekomendasi ponsel yang sesuai dengan keinginan pengguna. Sebaliknya, nilai yang lebih tinggi menunjukkan bahwa rekomendasi yang dihasilkan masih bisa ditingkatkan untuk lebih mencocokkan selera pengguna.




