# Laporan Proyek Machine Learning - Marchio Apriadi

## Domain Proyek

Dalam beberapa tahun terakhir, sektor properti mengalami dinamika yang signifikan, terutama di wilayah urban yang berkembang pesat. Penilaian harga rumah menjadi tantangan tersendiri karena dipengaruhi oleh berbagai faktor seperti lokasi, luas bangunan, tahun pembangunan, dan efisiensi energi. Metode penilaian tradisional seringkali tidak mampu menangkap kompleksitas hubungan non-linear antar variabel tersebut.​

Perkembangan teknologi kecerdasan buatan (AI), khususnya machine learning (ML), menawarkan pendekatan baru dalam memprediksi harga properti. Studi oleh Rampini dan Re Cecconi (2022) menunjukkan bahwa algoritma seperti ElasticNet, XGBoost, dan Artificial Neural Network (ANN) dapat digunakan untuk memprediksi harga rumah dengan tingkat akurasi yang tinggi. Dalam penelitian mereka yang dilakukan di kota Brescia dan Varese, ANN menunjukkan performa terbaik dengan Mean Absolute Error (MAE) yang lebih rendah dibandingkan model lainnya. Dalam penelitian mereka yang dilakukan di kota Brescia dan Varese, ANN menunjukkan performa terbaik dengan Mean Absolute Error (MAE) yang lebih rendah dibandingkan model lainnya.​

Namun, penelitian tersebut juga mencatat bahwa semua model mengalami penurunan akurasi dalam memprediksi properti dengan harga tertinggi, kemungkinan disebabkan oleh kurangnya data pada segmen tersebut. Hal ini menekankan pentingnya ketersediaan data yang representatif untuk semua segmen pasar dalam membangun model prediksi yang andal.​

Dengan mempertimbangkan temuan tersebut, proyek ini bertujuan untuk membangun model prediksi harga rumah  menggunakan algoritma ML seperti Linear Regression dan  Random Forest. Selain membandingkan hasil evaluasi model, proyek ini juga akan menganalisis variabel-variabel penting yang memengaruhi harga rumah berdasarkan dataset yang tersedia.



## Business Understanding
### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- Pernyataan Masalah 1: Bagaimana kita dapat membangun model machine learning yang akurat untuk memprediksi harga penjualan rumah berdasarkan berbagai fitur yang tersedia dalam dataset?
- Pernyataan Masalah 2: Faktor-faktor apa saja yang paling signifikan mempengaruhi harga penjualan rumah berdasarkan analisis model yang dibangun

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Jawaban pernyataan masalah 1: Tujuan utama proyek ini adalah untuk mengembangkan model machine learning dengan kinerja prediksi harga rumah yang tinggi, diukur dengan metrik evaluasi yang sesuai seperti Root Mean Squared Error (RMSE) dan R-squared.
- Jawaban pernyataan masalah 2 : Melalui analisis koefisien model kita akan mengidentifikasi fitur-fitur yang memiliki pengaruh paling besar terhadap prediksi harga rumah.

### Solution statements
  - Solution Statement 1: Pemodelan dengan Regresi Linear: Mengembangkan model regresi linear untuk memprediksi harga penjualan rumah berdasarkan fitur-fitur numerik dan kategorikal yang telah di-preprocess. Kinerja model akan diukur menggunakan metrik RMSE dan R-squared.
  - Solution Statement 2: Pemodelan dengan Random Forest (Sebagai Pembanding): Mengembangkan model Random Forest Regressor sebagai algoritma non-linear untuk membandingkan kinerja prediksi dengan model Regresi Linear. Kinerja model ini juga akan diukur menggunakan metrik RMSE dan R-squared

## Data Understanding
Dataset yang digunakan dalam proyek ini berisi informasi mengenai berbagai fitur rumah dan harga penjualannya. Fitur-fitur ini mencakup karakteristik fisik rumah, ukuran lahan, tahun pembangunan, dan kualitas lingkungan. Variabel target yang ingin diprediksi adalah harga penjualan rumah (House_Price).
[Kaggle Datasets](https://www.kaggle.com/datasets/prokshitha/home-value-insights).

### Variabel-variabel pada dataset ini adalah sebagai berikut:
- Square_Footage: Ukuran rumah dalam satuan kaki persegi. 
- Num_Bedrooms: Jumlah kamar tidur dalam rumah.
- Num_Bathrooms: Jumlah kamar mandi dalam rumah. 
- Year_Built: Tahun rumah dibangun. 
- Lot_Size: Ukuran lahan tempat rumah dibangun, diukur dalam satuan acre. 
- Garage_Size: Jumlah mobil yang dapat ditampung di garasi. 
- Neighborhood_Quality: Penilaian kualitas lingkungan pada skala 1-10, di mana 10 menunjukkan lingkungan berkualitas tinggi. 
- House_Price (Target Variable): Harga rumah, yang merupakan variabel dependen yang ingin diprediksi

Terdapat beberapa tahapan yang diperlukan untuk memahami data, seperti:
- Analisis statistik deskriptif (mean, median, standar deviasi, dll.) dilakukan untuk mendapatkan pemahaman awal tentang karakteristik data.
- Melakukan pengecekan terhadap data seperti mencari missing value, duplicate dan Outlier
- Melakukan Univariate dan Multivariate analysis

### Analisis statistik deskriptif
Untuk melakukan analisis statisitik dekriptif digunakan fungsi describe() dan diperoleh:

<img src="https://github.com/user-attachments/assets/efe8a418-317c-466e-bbdb-51cf6458576f" alt="Hasil descrribe()" style="float: left; margin-right: 15px; width: auto; height: auto;">

- Square_Footage: Luas bangunan rumah (dalam satuan hektar). Rata-rata luas sebesar 2.815 hektar, dengan minimum 503 hektar  dan maksimum 4.999 hektar

- Num_Bedrooms: Jumlah kamar tidur. Rata-rata 3 kamar, berkisar antara 1 hingga 5 kamar.

- Num_Bathrooms: Jumlah kamar mandi. Rata-rata 2 kamar mandi, dengan maksimum 3.

- Year_Built: Tahun rumah dibangun. Rentang antara tahun 1950 hingga 2022

- Lot_Size: Ukuran lahan rumah (dalam satuan hektar). Rata-rata sebesar 2.78 dengan nilai maksimum sekitar 4.99.

- Garage_Size: Ukuran garasi (jumlah mobil yang dapat ditampung). Mayoritas rumah memiliki 1-2 ukuran garasi.

- Neighborhood_Quality: Skor kualitas lingkungan (skala 1–10). Rata-rata sebesar 5.6 dengan skor terendah 1 dan tertinggi 8

- House_Price: Harga rumah( dolar). Rata-rata sekitar 618.861, harga tertinggi 1.108.237 dan harga terendah 111.627.


### Missing Value
Untuk mendeteksi missing value digunakan fungsi isnull().sum() dan diperoleh:

<img src="https://github.com/user-attachments/assets/2af4bfde-ed9c-4b9b-bc1b-d89528b3cdae" alt="Hasil isnull().sum()" style="float: left; margin-right: 15px; width: auto; height: auto;">

### Duplicate
Untuk mendeteksi duplicate digunakan fungsi duplicated().sum() dan diperoleh:

<img src="https://github.com/user-attachments/assets/f89e9c35-a7be-40a4-aacd-99195186a671" alt="duplicated().sum()" style="float: left; margin-right: 15px; width: auto; height: auto;">

### Outlier
Untuk mendeteksi Outlier digunakan metode IQR serta boxplot untuk visualisasi nya berikut adalah hasilnya:

<img src="https://github.com/user-attachments/assets/2fbf4526-dd78-4f3a-9b2a-628453014e51" alt="Outlier" style="float: left; margin-right: 15px; width: auto; height: auto;">

### Univariate Analysis
Analisis yang melibatkan satu variabel, fokus pada distribusi, nilai ekstrim, atau statistik deskriptif.

<img src="https://github.com/user-attachments/assets/a161a28e-864d-44a8-a447-2ba5f54b8c12" alt="Distribusi" style="float: left; margin-right: 15px; width: auto; height: auto;">

Diagram di atas menunjukkan distribusi frekuensi dari masing-masing fitur dalam dataset ini. Untuk fitur target dalam case ini (House_Price), memiliki distribusi harga rumah yang terlihat mendekati normal tetapi sedikit skew ke kiri (lebih banyak rumah dengan harga menengah ke tinggi).

### Multivariate Analysis
Analisis yang melibatkan dua atau lebih variabel untuk melihat hubungan antar fitur, pola, atau korelasi. Untuk analisis ini akan memanfaatkan matriks korelasi dan juga pair plot.

<img src="https://github.com/user-attachments/assets/b5ec6b14-27f9-455a-a4da-6db30ce09d6a" alt="Korelasi" style="float: left; margin-right: 15px; width: auto; height: auto;">

Visualisasi di atas menunjukkan matriks korelasi antar fitur numerik dalam dataset perumahan. Korelasi berkisar antara -1 (berbanding terbalik sempurna) hingga +1 (berbanding lurus sempurna). Warna lebih merah berarti korelasi lebih tinggi, sedangkan warna biru menunjukkan korelasi lemah atau negatif.

- Square_Footage dan House_Price: 0.99 :
  Hubungan sangat kuat dan positif. Artinya, semakin besar ukuran rumah, semakin tinggi harga rumah.

Fitur lain seperti:
- Lot_Size, Garage_Size, dan Year_Built memiliki korelasi lemah dengan harga rumah (masing-masing di bawah 0.2).
- Num_Bedrooms, Num_Bathrooms, dan Neighborhood_Quality hampir tidak memiliki korelasi signifikan dengan harga rumah.
- Korelasi antar fitur lainnya juga sangat rendah, menunjukkan tidak ada multikolinearitas yang kuat di antara sebagian besar fitur.

<img src="https://github.com/user-attachments/assets/5b3d6a0a-9f89-4483-8a45-9381efa00cc8" alt="Pairplot" style="float: left; margin-right: 15px; width: auto; height: auto;">

Visualisasi di atas adalah pairplot, yang menunjukkan hubungan pasangan antar fitur numerik dalam dataset. Untuk Square_Footage dengan House_Price, Terlihat hubungan linear yang sangat kuat, garisnya tampak lurus dan naik yang menguatkan bahwa ada korelasi tinggi seperti yang dilihat pada visualisasi sebelumnya (0.99).


## Data Preparation
Selanjutnya akan dilakukan Pembagian dataset (splitting data) ke dalam data uji dan latih. Proses ini akan dilakukan terlebih dahulu sebelum proses transformasi seperti standarisasi untuk mencegah kebocoran data (data leakage) yakni data uji bisa "tercemar" oleh informasi dari data latih (seperti mean dan standar deviasi), sehingga hasil evaluasi model menjadi tidak valid.

### Pembagian Dataset
Dataset dibagi menjadi set pelatihan (X_train, y_train) dan set pengujian (X_test, y_test) menggunakan fungsi train_test_split dengan proporsi 80% untuk pelatihan dan 20% untuk pengujian dan random_state = 42  untuk memastikan reproduktibilitas.

<img src="https://github.com/user-attachments/assets/c1978a4d-ac78-4fcc-80ce-11a4f96e18db" alt=" Splitting" style="float: left; margin-right: 15px; width: auto; height: auto;">

berikut adalah hasil dari pembagian dataset

<img src="https://github.com/user-attachments/assets/df39d392-11e3-41cd-ae97-176c75939ab5" alt=" hasil Splitting" style="float: left; margin-right: 15px; width: auto; height: auto;">



### Standarisasi Fitur Numerik 

Fitur-fitur numerik (Square_Footage, Num_Bedrooms, Num_Bathrooms, Year_Built, Lot_Size, Garage_Size, Neighborhood_Quality) distandarisasi menggunakan metode Z-Score melalu fungsi StandardScaler() dari scikit-learn untuk memastikan semua fitur berada pada skala yang serupa yakni memiliki mean 0 dan standar deviasi 1.

Proses standarisasi dilakukan secara terpisah untuk set pelatihan dan set pengujian. Objek StandardScaler di-fit (dilatih untuk mendapatkan mean dan standar deviasi) hanya pada data pelatihan. Kemudian, mean dan standar deviasi yang diperoleh dari data pelatihan digunakan untuk mentransformasi baik data pelatihan maupun data pengujian. Hal ini bertujuan untuk mencegah data leakage dan memastikan bahwa data pengujian diproses dengan cara yang sama seperti data yang dipelajari oleh model selama pelatihan.


Berikut adalah hasilnya untuk data X_train dan y_train
<img src="https://github.com/user-attachments/assets/3960fa6f-9f44-4d9c-907b-05f8749664cd" alt="X_train" style="float: left; margin-right: 15px; width: auto; height: auto;">

<img src="https://github.com/user-attachments/assets/45fa1d7d-f889-456c-ba34-a9c1d7aa537e" alt="y_train" style="float: left; margin-right: 15px; width: auto; height: auto;">

Berikut adalah hasilnya untuk data X_test dan y_test
<img src="https://github.com/user-attachments/assets/36a95f60-4a36-4dfb-b812-96000c4a576f" alt="X_test" style="float: left; margin-right: 15px; width: auto; height: auto;">

<img src="https://github.com/user-attachments/assets/8d21fb81-ae30-4f4d-b7bd-e255ef0437e3" alt="y_test" style="float: left; margin-right: 15px; width: auto; height: auto;">



## Modeling
Pada tahapan ini, kita membangun model machine learning untuk memprediksi harga penjualan rumah. Kita mengeksplorasi dua algoritma regresi: Regresi Linear dan Random Forest Regressor.

### Model Linear Regression
Model ini mencoba menemukan hubungan linear antara fitur-fitur (variabel independen) dan variabel target (House_Price). Secara sederhana, model ini mencari garis lurus (atau hyperplane dalam dimensi yang lebih tinggi) yang paling sesuai dengan data. Berikut adalah tahapan-tahapan yang dilakukan :
- Inisialisasi model LinearRegression dari scikit-learn
- Melatih model menggunakan data pelatihan (X_train, y_train) dengan metode fit()
- membuat prediksi harga rumah pada data pengujian (X_test) menggunakan metode predict().

<img src="https://github.com/user-attachments/assets/eb539412-8233-4f06-8421-085e7a09d898" alt="Linreg" style="float: left; margin-right: 15px; width: auto; height: auto;">

Terderpat beberapa kelebihan dan juga kekurangan dari model ini, antara lain :
- Kelebihan: Interpretasi model relatif mudah melalui analisis koefisien. Komputasi cepat dan efisien. Bekerja baik jika hubungan antara fitur dan target cenderung linear.
- Kekurangan: Mengasumsikan hubungan linear, yang mungkin tidak selalu akurat. Sensitif terhadap outliers dan multikolinearitas (meskipun analisis korelasi awal tidak menunjukkan multikolinearitas yang kuat).


## Model Random Forest Regressor:
Model ini merupakan ensemble learning method yang membangun banyak pohon keputusan (decision trees) secara acak pada subset data dan fitur yang berbeda. Hasil prediksi adalah rata-rata dari prediksi semua pohon. Berikut adalah tahapan-tahapan yang dilakukan :
- Inisialisasi model RandomForestRegressor dari scikit-learn dengan parameter awal n_estimators=100 dan random_state=42 
- Melatih model menggunakan data pelatihan (X_train, y_train) dengan metode fit()
- Membuat prediksi harga rumah pada data pengujian (X_test) menggunakan metode predict(

<img src="https://github.com/user-attachments/assets/f1b8523a-a313-41fb-ae34-7b1eaa897b9e" alt="RFG" style="float: left; margin-right: 15px; width: auto; height: auto;">

Terderpat beberapa kelebihan dan juga kekurangan dari model ini, antara lain :
- Kelebihan: Mampu menangkap hubungan non-linear dan interaksi antar fitur secara efektif. Lebih robust terhadap outliers dibandingkan Regresi Linear. Dapat memberikan informasi mengenai feature importance.
- Kekurangan: Model yang lebih kompleks dan sulit diinterpretasikan dibandingkan Regresi Linear. Cenderung overfit jika tidak di-tune dengan baik.

Pemilihan sebagai Model Terbaik: Pemilihan model terbaik untuk kasus ini akan berdasarkan hasil evaluasi yang menekankan pada metrik MSE, RMSE, MAE, dan R-Squared. 


## Evaluation
Pada bagian ini, kita akan mengevaluasi kinerja model Regresi Linear dan Random Forest menggunakan metrik yang sesuai untuk tugas regresi: Mean Squared Error (MSE), Root Mean Squared Error (RMSE), Mean Absolute Error (MAE), dan R-squared (R2).

Penjelasan mengenai metrik yang digunakan:

- Mean Squared Error (MSE): Rata-rata dari kuadrat selisih antara nilai prediksi dan nilai sebenarnya. Semakin rendah nilai MSE, semakin baik kinerja model.
- Root Mean Squared Error (RMSE): Akar kuadrat dari MSE. Memberikan ukuran kesalahan prediksi dalam unit yang sama dengan variabel target (harga rumah), sehingga lebih mudah diinterpretasikan. Semakin rendah nilai RMSE, semakin baik kinerja model.
- Mean Absolute Error (MAE): Rata-rata dari selisih absolut antara nilai prediksi dan nilai sebenarnya. Lebih robust terhadap outliers dibandingkan MSE. Semakin rendah nilai MAE, semakin baik kinerja model.
- R-squared (R2): Koefisien determinasi yang mengukur proporsi varians dalam variabel dependen (harga) yang dapat diprediksi dari variabel independen (fitur). Nilai R-squared berkisar antara 0 hingga 1. Nilai yang lebih tinggi menunjukkan bahwa model lebih baik dalam menjelaskan variabilitas data.

Menjelaskan hasil proyek berdasarkan metrik evaluasi:

    Evaluasi Model Regresi Linear:
      Mean Squared Error (MSE): 101434798.5056
      Root Mean Squared Error (RMSE): 10071.4844
      Mean Absolute Error (MAE): 8174.5836
      R-squared (R2): 0.9984

    Evaluasi Model Random Forest:
      Mean Squared Error (MSE): 394154497.0413
      Root Mean Squared Error (RMSE): 19853.3246
      Mean Absolute Error (MAE): 16106.2722
      R-squared (R2): 0.993

Berdasarkan hasil evaluasi, Model Regresi Linear menunjukkan kinerja yang lebih baik dengan nilai MSE (101,434,798.51), RMSE (10,071.48), dan MAE (8,174.58) yang lebih rendah, serta nilai R-squared yang lebih tinggi (0.9984) dibandingkan Model Random Forest (MSE: 394,154,497.04, RMSE: 19,853.32, MAE: 16,106.27, R-squared: 0.9939). Nilai R-squared yang sangat tinggi untuk kedua model menunjukkan bahwa keduanya mampu menjelaskan sebagian besar varians dalam harga rumah. Namun, metrik kesalahan yang lebih rendah dan R-squared yang lebih tinggi menjadikan **Regresi Linear sebagai model yang sedikit lebih akurat dan lebih baik dalam menjelaskan variabilitas data pada dataset ini**.

### Analisis Koefisien
Setelah pelatihan, dilakukan analisisis koefisien model Regresi Linear dengan menggunakan fungsi coef_ untuk memahami pengaruh linear setiap fitur terhadap prediksi harga rumah. Berikut adalah hasilnya

```
Koefisien Model Regresi Linear:
                Feature    Coefficient
0        Square_Footage  249787.914843
1          Num_Bedrooms   14524.734398
2         Num_Bathrooms    6695.906775
3            Year_Built   20662.121612
4              Lot_Size   19088.111033
5           Garage_Size    4219.449419
6  Neighborhood_Quality     335.247488

Intercept Model: 618576.0544
```

Berdasarkan hasil koefisie diatas dapat disimpulkan bahwa :
- Interpretasi koefisien Regresi Linear menunjukkan bahwa luas area rumah memiliki pengaruh positif terbesar terhadap harga.
- Fitur lain yang juga signifikan secara positif adalah Year_Built dan dan Lot_Size. Sementara itu, jumlah kamar tidur dan kamar mandi memiliki pengaruh positif yang lebih kecil, dan ukuran garasi serta kualitas lingkungan memiliki pengaruh positif yang relatif paling kecil.
- Hasil perkiraan harga awal dari sebuah rumah (apabila semua fitur dinggap 0) berdasarkan model Regresi Linear adalah 618576.0544



