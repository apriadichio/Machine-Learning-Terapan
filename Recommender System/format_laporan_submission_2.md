# Laporan Proyek Machine Learning - Marchio Apriadi

## Project Overview

Pada bagian ini, Kamu perlu menuliskan latar belakang yang relevan dengan proyek yang diangkat.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Jelaskan mengapa proyek ini penting untuk diselesaikan.
- Menyertakan hasil riset terkait atau referensi. Referensi yang diberikan harus berasal dari sumber yang kredibel dan author yang jelas.
  
  Format Referensi: [Judul Referensi](https://scholar.google.com/) 

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
Dataset yang digunakan dalam proyek ini adalah dataset https://www.kaggle.com/datasets/meirnizri/cellphones-recommendations yang terdiri dari tiga file utama:
- cellphones data.csv: Berisi informasi mengenai 34 ponsel pintar populer di AS pada tahun 2022. Setiap ponsel memiliki 13 fitur utama, termasuk performa (berdasarkan skor AnTuTu), ukuran memori, resolusi kamera, kapasitas baterai, ukuran layar, tanggal rilis, dan harga.
- cellphones users.csv: Mengandung informasi demografis pengguna yang berpartisipasi dalam survei, termasuk usia, jenis kelamin, dan pekerjaan.
- cellphones ratings.csv: Berisi data rating yang diberikan oleh pengguna melalui survei di Mechanical Turk. Setiap peserta melihat 10 ponsel acak dan memberikan rating seberapa besar kemungkinan mereka akan membeli setiap ponsel dengan harga yang diberikan, pada skala 1 (sangat tidak mungkin) hingga 10 (sangat mungkin).

Variabel-variabel pada dataset adalah sebagai berikut (setelah penggabungan):
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
- user_id: Identifikasi unik untuk setiap pengguna.
- rating: Tingkat kemungkinan pembelian yang diberikan pengguna (1-10).
- age: Usia pengguna.
- gender: Jenis kelamin pengguna.
- occupation: Pekerjaan pengguna.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
