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

### Exploratory Data Analysis(EDA)
Beberapa tahapan yang dilakukan untuk memahami data:
1. Penggabungan Dataset
Dua file CSV, yaitu tmdb_5000_movies.csv dan tmdb_5000_credits.csv, digabungkan berdasarkan kolom title menggunakan fungsi merge() dari pandas. Penggabungan ini diperlukan untuk menggabungkan informasi film (seperti overview, genre, dan keywords) dengan informasi pemain dan kru film (seperti cast dan crew), sehingga fitur yang dibutuhkan tersedia dalam satu dataframe.
2. Pengecekan null values
Dilakukan pengecekan terhadap kolom penting seperti overview, genres, cast, dan crew untuk mengetahui apakah terdapat nilai kosong (null). Ini penting karena keberadaan data kosong bisa menyebabkan error saat proses parsing atau training model.
3. Parsing Data JSON
Kolom genres, keywords, cast, dan crew berisi data dalam format string JSON. Oleh karena itu, dilakukan parsing data menggunakan ast.literal_eval() untuk mengubah string menjadi list of dictionary. Kemudian, fitur penting seperti nama genre, keyword, tiga aktor utama, dan sutradara diekstrak dan disimpan dalam bentuk list of string. Parsing ini penting agar data dapat digunakan untuk proses tokenisasi dan vectorization dalam model content-based filtering, yang berbasis teks.
4. Visualisasi:
   - Genre paling sering muncul
   - Aktor paling sering muncul
   - Distribusi panjang sinopsis (overview)
   - Korelasi antara popularitas dan rating



## Data Preparation
Pada tahap ini, data yang telah melalui proses eksplorasi dan parsing JSON difokuskan untuk disiapkan sebagai input model content-based filtering. Langkah-langkah data preparation dilakukan sebagai berikut
1. Penanganan Nilai Kosong (Null Values)  
Setelah dilakukan pengecekan di tahap sebelumnya, ditemukan bahwa beberapa kolom penting seperti overview, genres, cast, dan crew memiliki nilai kosong. Langkah ini penting agar proses parsing dan pembuatan fitur tidak mengalami error atau menghasilkan hasil yang bias. Penanganan dilakukan sebagai berikut:
   - Kolom overview yang kosong digantikan dengan string kosong (""), karena kolom ini berbentuk teks dan masih bisa diproses.
   - Untuk kolom genres, cast, dan crew, jika terdapat nilai kosong maka baris tersebut dihapus, karena kolom-kolom ini penting dalam proses ekstraksi fitur. Kehilangan satu atau lebih dari informasi ini dapat menurunkan kualitas rekomendasi.

2. Pembuatan Fitur Gabungan (tags)
Dibuat kolom tags sebagai gabungan dari:
   - overview
   - genres
   - keywords
   - cast (3 aktor utama)
   - crew (sutradara)

Penggabungan dilakukan agar model content-based dapat menggunakan satu representasi teks gabungan untuk menghitung kemiripan antar film berdasarkan isi kontennya.

3. Normalisasi Teks  
Semua teks pada kolom tags dikonversi menjadi huruf kecil (lowercase). Hal ini untuk mencegah token yang identik tapi berbeda kapitalisasi dianggap berbeda oleh model, seperti "Action" vs "action".

4. Stemming dan Tokenisasi  
Proses stemming dapat dilakukan untuk mengubah kata ke bentuk dasarnya, sementara tokenisasi memecah teks menjadi unit kata. Ini opsional, namun bermanfaat untuk menyamakan makna kata-kata yang memiliki bentuk turunan.
Proses ini dilakukan menggunakan library NLTK dengan algoritma PorterStemmer, yang merupakan salah satu stemming algorithm paling umum digunakan di Natural Language Processing (NLP).
Langkah ini sangat penting karena membantu mengurangi redundansi kata dan memperkuat akurasi dalam mengukur kemiripan antar film berbasis teks yang telah diproses.


## Modeling
Pada tahap ini, sistem rekomendasi dibangun dengan pendekatan Content-Based Filtering, yaitu merekomendasikan film berdasarkan kemiripan konten antar film. Kemiripan diukur dari informasi seperti genre, kata kunci, pemeran, sutradara, dan deskripsi film (overview) yang telah digabungkan ke dalam kolom tags.
1. TF-IDF Vectorization  

Model pertama menggunakan teknik TF-IDF Vectorization untuk mengubah data teks dari kolom tags menjadi representasi numerik. TF-IDF memberi bobot pada setiap kata berdasarkan frekuensinya dalam satu dokumen relatif terhadap seluruh koleksi dokumen. Tujuannya adalah untuk menekankan kata-kata yang spesifik dan mengurangi pengaruh kata-kata umum.

Kemudian, dilakukan perhitungan cosine similarity antar vektor film untuk mengetahui tingkat kemiripan antara satu film dengan yang lainnya. Film dengan nilai kemiripan tertinggi akan dijadikan rekomendasi.

2. Count Vectorizer

Pendekatan kedua menggunakan Count Vectorizer, yaitu metode representasi teks berdasarkan jumlah kemunculan kata (frekuensi). Meskipun metode ini lebih sederhana dan cepat, ia tidak memperhitungkan seberapa penting suatu kata di seluruh korpus. Akibatnya, kata-kata yang umum masih dianggap penting.

**Fungsi Rekomendasi**  
Fungsi rekomendasi dikembangkan untuk menerima input berupa judul film, lalu mengeluarkan daftar film yang paling mirip berdasarkan kemiripan konten. Rekomendasi yang dihasilkan bersifat dinamis dan berbasis pada kedekatan nilai cosine similarity dari vektor teks.

**Perbandingan Pendekatan**
1. TF-IDF  
   Kelebihan : Lebih selektif terhadap kata umum; meningkatkan relevansi rekomendasi  
   Kekurangan: Lebih kompleks, bisa menghilangkan kata-kata penting yang sering muncul
2. CountVectorizer  
   Kelebihan : Sederhana, cepat, mudah dipahami  
   Kekurangan: Kurang selektif, bisa menyebabkan over-representasi kata umum

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**
