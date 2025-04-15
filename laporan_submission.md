# Laporan Proyek Machine Learning - Muhammad Abel Al-fahrezi

## Domain Proyek

Diabetes mellitus, khususnya tipe-2, merupakan salah satu penyakit kronis yang paling umum di dunia dan menjadi salah satu penyebab utama kematian serta komplikasi kesehatan serius. Menurut data dari World Health Organization (WHO), pada tahun 2021 lebih dari 422 juta orang di dunia menderita diabetes, dan angka ini diperkirakan akan terus meningkat dalam beberapa dekade ke depan (WHO, 2021).

Secara khusus, komunitas Pima Indians di Amerika Serikat memiliki tingkat prevalensi diabetes tipe-2 yang sangat tinggi dibandingkan dengan populasi lain. Berdasarkan penelitian yang dilakukan oleh National Institute of Diabetes and Digestive and Kidney Diseases (NIDDK), sekitar 50% orang dewasa dari suku Pima menderita diabetes, menjadikan mereka kelompok studi penting untuk memahami faktor risiko dan prediksi diabetes.

Dataset Pima Indians Diabetes Dataset berisi data kesehatan perempuan berusia di atas 21 tahun dari komunitas tersebut, mencakup informasi seperti jumlah kehamilan, kadar glukosa, tekanan darah, BMI, dan faktor genetik. Dengan memanfaatkan machine learning, kita dapat membangun model prediksi untuk mengklasifikasikan apakah seseorang berisiko terkena diabetes atau tidak berdasarkan fitur-fitur tersebut.

### Pentingnya Masalah Ini Diselesaikan
- Deteksi Dini & Pencegahan: Mengembangkan model klasifikasi yang akurat akan membantu deteksi dini individu yang berisiko tinggi, sehingga intervensi medis atau perubahan gaya hidup dapat dilakukan lebih awal untuk mencegah komplikasi.

- Efisiensi Layanan Kesehatan: Sistem prediksi otomatis dapat membantu tenaga medis dalam proses skrining, mengurangi waktu diagnosis manual, dan mempercepat pengambilan keputusan.

- Biaya Kesehatan: Diagnosis dan penanganan diabetes memerlukan biaya tinggi. Dengan prediksi dini, biaya pengobatan jangka panjang dapat ditekan secara signifikan (American Diabetes Association, 2018).

- Meningkatkan Kesadaran: Memberikan pemahaman kepada masyarakat mengenai pentingnya faktor kesehatan seperti pola makan, berat badan, dan genetika dalam pengembangan diabetes.



### Referensi
- World Health Organization (WHO). (2021). Diabetes.
https://www.who.int/news-room/fact-sheets/detail/diabetes

- National Institute of Diabetes and Digestive and Kidney Diseases (NIDDK). (2016). Diabetes in American Indians and Alaska Natives: Facts At-a-Glance.
https://www.niddk.nih.gov/health-information/diabetes/statistics

## Business Understanding

Dalam proyek ini, fokus utama adalah membangun model klasifikasi untuk memprediksi risiko diabetes berdasarkan data kesehatan individu dari komunitas Pima Indians. Proses klarifikasi dilakukan untuk memastikan bahwa masalah yang akan diselesaikan benar-benar spesifik, terukur, dan relevan dengan data yang tersedia.


### Problem Statements

Berdasarkan latar belakang yang telah dijelaskan, rumusan masalah dalam proyek ini adalah sebagai berikut:

- Bagaimana membangun model klasifikasi machine learning untuk memprediksi risiko diabetes pada perempuan dewasa komunitas Pima Indian berdasarkan data kesehatan mereka?

- Fitur-fitur kesehatan apa saja yang paling berpengaruh dalam menentukan apakah seseorang berisiko menderita diabetes atau tidak?

- Bagaimana performa model klasifikasi yang dibangun dalam hal akurasi, presisi, recall, dan F1-score pada dataset Pima Indians Diabetes?

### Goals

Adapun tujuan dari proyek ini meliputi:

- Mengembangkan model klasifikasi berbasis machine learning yang mampu memprediksi dengan baik apakah seseorang terdiagnosis diabetes atau tidak, menggunakan data kesehatan dari Pima Indians Diabetes Dataset.

- Melakukan analisis terhadap faktor-faktor kesehatan seperti kadar glukosa, tekanan darah, BMI, dan jumlah kehamilan, serta menentukan pengaruhnya terhadap risiko diabetes.

- Mengevaluasi performa model menggunakan metrik evaluasi standar (akurasi, precision, recall, F1-score), dan mengidentifikasi apakah model tersebut layak digunakan untuk mendukung proses skrining awal pada individu dengan risiko diabetes.

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.  
- Menambahkan bagian “Solution Statement” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

### Solution statements
- Solution 1: Baseline Model menggunakan Logistic Regression
Sebagai baseline model, digunakan algoritma Logistic Regression. Algoritma ini dipilih karena sifatnya yang sederhana, interpretatif, dan cocok untuk masalah klasifikasi biner.
Langkah-langkah:

1. Melakukan data preprocessing seperti menangani missing values (jika ada), normalisasi data, dan split dataset menjadi training & testing set.

2. Menggunakan Logistic Regression tanpa hyperparameter tuning untuk menghasilkan baseline.

3. Mengevaluasi performa model menggunakan metrik: Accuracy, Precision, Recall, F1-Score dan Confusion Matrix untuk melihat distribusi prediksi.

- Solution 2: Improvement dengan Random Forest
Setelah baseline, solusi kedua adalah menggunakan model Random Forest Classifier, yang dikenal memiliki performa yang baik dalam menangani dataset dengan fitur numerik serta memiliki kemampuan mengatasi overfitting lebih baik dibanding decision tree tunggal.
Langkah-langkah:

1. Melakukan preprocessing yang sama seperti pada baseline.

2. Mengimplementasikan Random Forest Classifier dengan hyperparameter tuning, seperti:Number of estimators (n_estimators), Maximum depth (max_depth), Minimum samples split, Criterion (Gini/Entropy)

3. Mengevaluasi model menggunakan metrik yang sama dengan baseline:Accuracy, Precision, Recall, F1-Score,Confusion Matrix



## Data Understanding
Dalam proyek ini, digunakan Pima Indians Diabetes Dataset, yang berasal dari National Institute of Diabetes and Digestive and Kidney Diseases (NIDDK) dan tersedia di Kaggle link :(https://www.kaggle.com/datasets/nancyalaswad90/review) . Dataset ini berisi data kesehatan dari perempuan dewasa keturunan suku Pima Indian, dengan tujuan utama untuk memprediksi apakah seorang individu menderita diabetes berdasarkan berbagai indikator kesehatan.

Deskripsi Dataset :
- Dataset ini terdiri dari 768 sampel (baris) dan 8 fitur numerik, serta 1 variabel target (Outcome).

- Semua fitur dalam dataset adalah numerik dan berkaitan dengan kesehatan individu.

- Tidak ada data kategori, sehingga tidak diperlukan encoding tambahan.

### Variabel-variabel pada Pima Indians Diabetes dataset adalah sebagai berikut:
- Pregnancies	: Jumlah kehamilan yang pernah dialami individu.
- Glucose	: Kadar glukosa dalam darah (mg/dL).
- BloodPressure	: Tekanan darah diastolik (mm Hg).
- SkinThickness	: Ketebalan lipatan kulit trisep (mm), sebagai indikator lemak tubuh.
- Insulin	: Kadar insulin dalam darah (mu U/ml).
- BMI	        : Indeks Massa Tubuh (Body Mass Index).
- DiabetesPedigreeFunction	:Faktor risiko diabetes berdasarkan riwayat keluarga.
- Age	        :Usia individu dalam tahun.
- Outcome	:Label target (0 = Tidak Diabetes, 1 = Diabetes).

- Eksplorasi Data (Exploratory Data Analysis - EDA)
1. Statistik Deskriptif
  > Distribusi Nilai Fitur: Dilakukan analisis distribusi data untuk melihat apakah terdapat skewness atau outlier.
  > Rata-rata dan Median: Misalnya, rata-rata kadar glukosa pada individu yang didiagnosis diabetes lebih tinggi dibandingkan yang tidak.

2. Visualisasi Data
Beberapa metode visualisasi yang digunakan untuk memahami pola data:
  > Histogram & Boxplot: Digunakan untuk melihat distribusi nilai setiap fitur.
  > Heatmap Korelasi: Untuk menganalisis hubungan antar variabel.
  > Pairplot (Seaborn): Untuk melihat distribusi dan pola hubungan antar fitur.

3. Identifikasi Missing Values
  > Beberapa nilai dalam fitur seperti Glucose, BloodPressure, SkinThickness, Insulin, dan BMI memiliki nilai 0, yang secara medis tidak mungkin terjadi.
  > Solusi yang dilakukan adalah mengganti nilai nol dengan median atau menggunakan metode imputasi.

## Data Preparation
Sebelum melatih model klasifikasi, dilakukan data preparation untuk memastikan kualitas data optimal. Proses ini mencakup penanganan missing values, normalisasi, penanganan outlier, dan penyeimbangan data.

- Menangani Missing Values
Meskipun tidak ada nilai NaN secara eksplisit dalam dataset Pima Indians Diabetes, beberapa fitur seperti Glucose, BloodPressure, SkinThickness, Insulin, dan BMI memiliki nilai 0, yang secara medis tidak masuk akal. Oleh karena itu, nilai 0 dalam fitur kesehatan digantikan dengan median.

- Menangani Outlier
Beberapa fitur seperti Insulin dan SkinThickness memiliki outlier yang signifikan. Outlier diidentifikasi menggunakan Interquartile Range (IQR) dan ditangani dengan Winsorization.

- Normalisasi Data (Feature Scaling)
Fitur numerik memiliki skala yang berbeda, sehingga dilakukan normalisasi dengan Min-Max Scaling agar model bekerja lebih baik.

- Menangani Ketidakseimbangan Kelas
Dataset ini memiliki ketidakseimbangan dalam jumlah pasien dengan diabetes (1) lebih sedikit dibandingkan tanpa diabetes (0). Untuk mengatasi hal ini, digunakan SMOTE (Synthetic Minority Oversampling Technique).

- Split Data (Train-Test Split)
Dataset dibagi menjadi 80% training data dan 20% testing data menggunakan stratified sampling agar proporsi kelas tetap seimbang.

- Mengganti nilai 0 dengan median karena Median lebih tahan terhadap outlier dibandingkan mean dan Menghindari bias akibat distribusi yang skewed
- Menangani outlier karena outlier dapat menyebabkan model overfitting atau hasil yang tidak akurat dan menggunakan Winsorization agar distribusi tetap stabil tanpa menghapus data.
- Menggunakan Min-Max Scaling untuk memastikan semua fitur dalam rentang 0-1, memudahkan model berbasis Gradient Descent dan mencegah fitur dengan nilai besar mendominasi model.
- Menggunakan SMOTE karena model cenderung bias ke kelas mayoritas jika dataset tidak seimbang dan SMOTE membuat sampel sintetis untuk kelas minoritas tanpa kehilangan data asli.
- Menggunakan stratify untuk memastikan proporsi kelas tetap seimbang antara training dan testing set.


## Modeling
Disini saya menggunakan 2 algoritma yaitu :

1. Logistic Regression
Algoritma yang digunakan untuk klasifikasi biner berdasarkan regresi logistik.
Parameter yang Digunakan:
- random_state=42: Agar hasil dapat direproduksi.

2. Random Forest Classifier
Algoritma berbasis ensemble yang menggunakan banyak decision tree untuk meningkatkan akurasi.
Parameter yang Digunakan:
- n_estimators=100: Jumlah decision tree yang digunakan.
- random_state=42: Agar hasil dapat direproduksi.

1. Logistic Regression :
Kelebihan  
- Sederhana dan cepat untuk diimplementasikan.
- Mudah untuk diinterpretasikan karena berbasis probabilitas.
- Cocok untuk dataset kecil dan tidak terlalu kompleks.

Kekurangan:
- Kurang fleksibel untuk menangkap hubungan non-linear.
- Rentan terhadap outlier jika tidak ditangani dengan baik.

2. Random Forest Classifier  
Kelebihan:
- Lebih akurat dibanding model sederhana seperti Logistic Regression.
- Mampu menangani fitur dengan hubungan non-linear.
- Tidak mudah overfitting karena menggunakan banyak pohon keputusan.

Kekurangan:
- Lebih lambat dibanding Logistic Regression terutama untuk dataset besar.
- Kurang dapat diinterpretasikan dibanding Logistic Regression.


Dari dua algoritma yang diuji (Logistic Regression vs. Random Forest), model terbaik adalah Random Forest, karena:
- Akurasi lebih tinggi (80%) dibanding Logistic Regression (73%).
- Recall & F1-score lebih tinggi, artinya lebih baik dalam mendeteksi pasien diabetes.
- Dapat menangani fitur non-linear & lebih fleksibel dibanding Logistic Regression.

## Evaluation
Metrik Evaluasi yang Digunakan
Karena masalah yang kita hadapi adalah klasifikasi biner (Diabetes atau Tidak), maka kita menggunakan empat metrik utama untuk menilai performa model:

1. Accuracy
- Kelebihan: Memberikan gambaran umum tentang seberapa sering model benar.
- Kekurangan: Tidak cukup representatif jika data tidak seimbang.
- Relevansi: Dataset Pima Indians memang sedikit tidak seimbang (jumlah penderita diabetes < non-diabetes), jadi akurasi perlu dilengkapi dengan metrik lain seperti recall dan F1.

2. Precision
- Kelebihan: Cocok untuk mengevaluasi seberapa "pasti" model saat menyatakan seseorang menderita diabetes.
- Relevansi: Dalam konteks medis, false positive (mendiagnosis seseorang sebagai penderita padahal tidak) bisa membuat pasien khawatir atau menjalani pemeriksaan tak perlu. Maka, precision penting tapi bukan yang utama.

3. Recall
- Kelebihan: Memastikan bahwa kasus diabetes tidak luput dari deteksi.

- Relevansi: Sangat penting. Dalam konteks kesehatan, false negative sangat berbahaya—pasien yang tidak didiagnosis bisa luput dari penanganan dini. Recall tinggi artinya model lebih sensitif terhadap kasus positif.

4. F1-score
- Kelebihan: Metrik gabungan yang menyeimbangkan precision dan recall.

- Relevansi: Sangat berguna karena mempertimbangkan trade-off antara prediksi positif yang benar dan kegagalan mendeteksi kasus penting. Cocok untuk dataset tidak seimbang.


**Berikut Formula metrik dan bagaimana metrik tersebut bekerja:**
1. Accuracy :
Formula :
 ```math
  Accuracy = \frac{TP + TN}{TP + TN + FP + FN}
  ```
Cara Kerjanya :
  - Mengukur seberapa banyak prediksi yang benar dibandingkan total prediksi.
  - Cocok digunakan ketika dataset memiliki distribusi kelas yang seimbang.
  - Jika dataset tidak seimbang, akurasi bisa menyesatkan.
2. Precision
Formula :
 ```math
  Precision = \frac{TP}{TP + FP}
  ```
Cara Kerjanya : 
- Precision tinggi berarti model jarang memberikan prediksi positif yang salah.
- Cocok digunakan jika false positive memiliki konsekuensi serius, misalnya kesalahan diagnosis yang dapat menyebabkan pasien menjalani perawatan yang tidak perlu.

3. Recall
Formula : 
```math
  Recall = \frac{TP}{TP + FN}
  ```
Cara Kerjanya : 
  - Recall tinggi berarti model mampu menangkap hampir semua kasus positif.
  - Berguna jika false negative lebih berbahaya, misalnya jika pasien diabetes tidak terdeteksi sehingga tidak mendapatkan perawatan yang diperlukan.

4. F1-Score
Formula : 
```math
  F1 = 2 \times \frac{Precision \times Recall}{Precision + Recall}
  ```
Cara Kerjanya : 
  - F1-score berguna ketika terdapat trade-off antara precision dan recall.
  - Jika dataset tidak seimbang, F1-score lebih akurat daripada akurasi dalam menilai performa model.

**Hasil Evaluasi dan Komparasi Model**
Hasil evaluasi kuantitatif :
1. Logistic Regression
- Accuracy  : 0.73
- Precision : 0.73
- Recall    : 0.74
- F1-score  : 0.73
  
2. Random Forest
- Accuracy  : 0.80
- Precision : 0.80
- Recall    : 0.80
- F1-score  : 0.80


Model Terbaik Berdasarkan metrik evaluasi:  

- Random Forest Classifier lebih unggul daripada Logistic Regression.

- Meskipun belum dituning, model ini sudah memberikan recall dan F1-score lebih tinggi, yang sangat penting untuk kasus klasifikasi kesehatan.

**Hubungan dengan Business Understanding**  
1. Bagaimana membangun model klasifikasi machine learning untuk memprediksi risiko diabetes pada perempuan dewasa komunitas Pima Indian berdasarkan data kesehatan mereka?

Tercapai :

- Model klasifikasi berbasis Random Forest dan Logistic Regression telah berhasil dibangun dan diuji.

- Model mampu melakukan prediksi secara cukup akurat dengan metrik yang kuat: F1-score 0.80, Recall 0.80, dan Precision 0.80 menggunakan Random Forest.

- Hal ini membuktikan bahwa model dapat digunakan sebagai alat bantu prediksi awal risiko diabetes pada kelompok sasaran.

2. Fitur-fitur kesehatan apa saja yang paling berpengaruh dalam menentukan apakah seseorang berisiko menderita diabetes atau tidak?  

Tercapai :  

- Dari model Random Forest, kita bisa memperoleh informasi tentang feature importance.

- Fitur yang paling berpengaruh (berdasarkan evaluasi model) meliputi Glucose, BMI (Body Mass Index), Age, dan Insulin

- Pengetahuan ini sangat penting bagi pihak medis dan komunitas kesehatan untuk fokus pada variabel-variabel yang paling relevan dalam pencegahan dan deteksi dini.

3. Bagaimana performa model klasifikasi yang dibangun dalam hal akurasi, presisi, recall, dan F1-score pada dataset Pima Indians Diabetes?

Tercapai

- Evaluasi menunjukkan bahwa model Random Forest tanpa tuning memberikan hasil performa terbaik dibandingkan Logistic Regression. Accuracy: 80%, Precision: 80%, Recall: 80%, F1-score: 80%

- Dengan nilai yang seimbang di semua metrik, model tidak hanya akurat tetapi juga cukup andal dalam menangani risiko false negative, yang krusial dalam konteks kesehatan.

**Dampak Solusi terhadap Bisnis**  
  
Solusi yang dibangun dalam bentuk model klasifikasi:

- Berguna secara praktis untuk membantu tenaga kesehatan atau pengambil kebijakan dalam melakukan skrining awal berbasis data.

- Memberikan insight prediktif terhadap siapa yang memiliki risiko tinggi menderita diabetes.

- Dapat diintegrasikan ke dalam sistem kesehatan komunitas untuk membantu proses intervensi dini, pengelolaan program edukasi, dan distribusi sumber daya.
