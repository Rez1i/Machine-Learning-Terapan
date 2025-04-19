# Laporan Proyek Machine Learning - Muhammad Abel Al-Fahrezi

## Project Overview

Sistem rekomendasi telah menjadi bagian integral dari platform digital, terutama di industri hiburan seperti layanan streaming film. Proyek ini bertujuan untuk membangun sistem rekomendasi film berbasis content-based filtering yang mampu memberikan rekomendasi personal kepada pengguna berdasarkan konten film yang pernah mereka sukai sebelumnya.

Sistem ini mengandalkan fitur-fitur seperti genre, sinopsis, sutradara, dan aktor untuk mengidentifikasi kesamaan antar film dan menghasilkan saran yang relevan.

Proyek ini penting karena Dengan meningkatnya jumlah film yang tersedia secara online, pengguna sering mengalami kebingungan dalam memilih tontonan. Sistem rekomendasi ini membantu menyederhanakan proses pengambilan keputusan tersebut.  
  
Referensi : Content-Based Recommendation Systems, Ricci, F., Rokach, L., & Shapira, B. (2015)

## Business Understanding

Sistem rekomendasi telah menjadi komponen penting dalam industri hiburan digital, khususnya layanan streaming film. Dalam situasi di mana pengguna memiliki ribuan pilihan film, mereka membutuhkan bantuan untuk menemukan film yang sesuai dengan selera mereka. Oleh karena itu, dibutuhkan sistem yang mampu memberikan rekomendasi secara personal, berdasarkan konten dari film yang disukai sebelumnya.

### Problem Statements

- Bagaimana cara merekomendasikan film kepada pengguna berdasarkan film yang pernah mereka sukai, tanpa data historis pengguna lainnya?
→ Permasalahan ini muncul karena tidak semua platform memiliki data interaksi pengguna secara eksplisit (seperti rating atau history).

- Bagaimana mengidentifikasi kemiripan antar film berdasarkan informasi konten seperti sinopsis, genre, dan aktor?
→ Dibutuhkan pendekatan untuk mengolah fitur-fitur tekstual dan kategorikal agar bisa dibandingkan secara matematis.

- Bagaimana membangun sistem rekomendasi yang efisien dan tetap relevan terhadap kebutuhan pengguna secara individual?
→ Sistem harus tetap ringan namun cukup akurat dalam menampilkan film yang relevan.

### Goals

- Membangun sistem rekomendasi film berbasis konten (content-based filtering) tanpa memerlukan data rating pengguna.
→ Sistem akan fokus pada konten film dan kesamaan antar item.

- Membuat model untuk mengukur kemiripan antar film berdasarkan representasi vektor dari fitur-fitur kontennya.
→ Sistem akan menggunakan teknik NLP dan representasi numerik (TF-IDF / CountVectorizer).

- Menyediakan rekomendasi film yang relevan dan mudah diakses bagi pengguna berdasarkan input satu film yang mereka sukai.
→ Output berupa daftar film serupa (top-N recommendations).

### Solution statements
Untuk mencapai tujuan proyek ini, digunakan dua pendekatan berbeda dalam sistem rekomendasi:  
1. TF-IDF Vectorizer + Cosine Similarity
- Menggunakan sinopsis (overview) film sebagai fitur utama.
- Mengolah teks dengan TF-IDF untuk membentuk representasi vektor.
- Menghitung kemiripan antar film menggunakan cosine similarity.
- Cocok untuk mengukur kedekatan semantik berdasarkan deskripsi cerita.

2. CountVectorizer pada "Soup" Fitur Gabungan  
- Membuat kolom gabungan (soup) dari beberapa fitur konten: genre, keywords, cast, director.
- Menggunakan CountVectorizer untuk menghasilkan vektor kata sederhana.
- Mengukur kesamaan menggunakan cosine similarity.
- Cocok untuk menangkap konteks umum dari film berdasarkan fitur yang tidak hanya berasal dari teks bebas.

## Data Understanding
Dataset yang digunakan dalam proyek ini adalah TMDB 5000 Movie Dataset, tersedia secara publik di platform Kaggle. Dataset ini disediakan oleh The Movie Database (TMDB) dan berisi informasi lengkap mengenai lebih dari 4.800 film. [TMDB 5000 Movie Dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata/data).  
Dataset terdiri dari dua file utama:
- tmdb_5000_movies.csv: berisi informasi konten film (judul, sinopsis, genre, popularitas, dll.)
- tmdb_5000_credits.csv: berisi informasi kredensial seperti aktor dan kru produksi

Secara keseluruhan, dataset ini memiliki kualitas yang baik, namun diperlukan beberapa preprocessing seperti parsing data dalam bentuk JSON string, penggabungan antar tabel, dan pembersihan teks.

Variabel-variabel pada TMDB Movie Dataset adalah sebagai berikut:  

tmdb_5000_movies.csv
- id: ID unik film
- title: Judul film
- genres: Daftar genre film dalam format JSON
- overview: Sinopsis film dalam bentuk teks
- keywords: Daftar kata kunci yang relevan dengan film
- popularity: Skor popularitas film berdasarkan TMDB
- vote_average: Rata-rata rating pengguna
- vote_count: Jumlah rating yang diberikan
- runtime: Durasi film
- release_date: Tanggal rilis film

tmdb_5000_credits.csv
- movie_id: ID film (untuk digabungkan dengan file movies.csv)
- title: Judul film
- cast: Daftar aktor utama (dalam format JSON)
- crew: Daftar kru, termasuk posisi seperti sutradara (dalam format JSON)

Tahapan Pemahaman Data (Exploratory Data Analysis):  
Beberapa tahapan yang dilakukan untuk memahami data:
1. Penggabungan data: Gabungkan tmdb_5000_movies.csv dan tmdb_5000_credits.csv menggunakan kolom title.
2. Pengecekan null values: Mengecek apakah ada data yang kosong terutama pada kolom overview, cast, genres, dan crew.
3. Parsing data JSON: Kolom seperti genres, keywords, cast, dan crew memiliki format string JSON dan perlu diekstrak menjadi list/teks.
4. Visualisasi:
   - Genre paling sering muncul
   - Aktor atau sutradara paling sering muncul
   - Distribusi panjang sinopsis (overview)
   - Korelasi antara popularitas dan rating



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
