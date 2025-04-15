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
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

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
