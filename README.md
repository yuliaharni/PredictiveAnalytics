# Laporan Proyek Prediksi Harga Emas

## Domain Proyek

Pada bagian ini, peneliti melakukan analisis untuk memprediksi harga emas berdasarkan data historis dan faktor-faktor ekonomi yang mempengaruhi pasar emas, seperti nilai tukar mata uang dan indeks saham. Emas merupakan komoditas yang banyak diperdagangkan dan dipengaruhi oleh berbagai faktor, baik secara langsung maupun tidak langsung. Oleh karena itu, penting untuk memiliki model prediksi yang tepat guna membantu investor atau trader dalam mengambil keputusan.

Dengan meningkatnya ketidakpastian pasar dan pergerakan harga emas yang fluktuatif, memprediksi harga emas di masa depan dapat membantu para investor untuk merencanakan strategi investasi yang lebih baik. Model yang dikembangkan dalam proyek ini akan digunakan untuk memprediksi harga emas berdasarkan data historis yang ada dan faktor-faktor terkait yang dapat mempengaruhi harga emas.

## Business Understanding

### Problem Statements

1. Bagaimana memprediksi harga emas yang akan datang berdasarkan data historis harga emas, nilai tukar mata uang, dan indeks saham?
2. Faktor apa saja yang memengaruhi fluktuasi harga emas dan dapat digunakan untuk meningkatkan akurasi model prediksi harga emas?

### Goals

1. Mengembangkan model prediksi yang akurat untuk harga emas dengan menggunakan faktor-faktor yang mempengaruhi harga emas.
2. Meningkatkan akurasi model dengan menggunakan beberapa algoritma regresi dan melakukan hyperparameter tuning untuk menemukan kombinasi yang optimal.
Menggunakan teknik regresi, model akan mempelajari hubungan antara harga emas dengan faktor eksternal (seperti indeks saham, nilai tukar, volume perdagangan) dan memprediksi harga emas di masa depan.

Model ini dibangun untuk memprediksi harga emas di masa mendatang berdasarkan faktor-faktor eksternal seperti harga saham (S&P 500, Nasdaq), nilai tukar mata uang (USD/CHF, EUR/USD), dan volume perdagangan emas.

Tujuan dari prediksi ini adalah memberikan gambaran atau insight kepada investor, analis keuangan, maupun pelaku pasar dalam mengambil keputusan investasi. Walaupun output dari model ini hanya berupa angka prediksi (bukan instruksi langsung seperti "beli" atau "jual"), informasi ini tetap sangat berguna untuk:

Melihat tren pergerakan harga emas di masa depan

Menganalisis kapan waktu yang tepat untuk membeli atau menjual emas

Menghubungkan harga emas dengan faktor-faktor global yang mempengaruhinya

Dengan begitu, hasil prediksi bisa menjadi dasar untuk pengambilan keputusan yang lebih informatif dan strategis dalam dunia investasi logam mulia, terutama emas.

### Solution Statements

- Menggunakan algoritma Random Forest Regressor untuk memprediksi harga emas berdasarkan data historis dan faktor terkait.
- Mengoptimalkan model menggunakan teknik hyperparameter tuning untuk meningkatkan hasil prediksi.

# Data Understanding
### Sumber Data
Dataset ini diperoleh dari Kaggle Financial Dataset (https://www.kaggle.com/datasets/franciscogcc/financial-data). Dataset ini berisi informasi harga emas dan faktor ekonomi makro lain seperti indeks saham, mata uang, dan logam mulia lainnya dari tahun 2010 hingga 2024.

### Jumlah Data
Dataset memiliki:
Jumlah baris: 3905 baris
Jumlah kolom awal: 45 kolom
Jumlah kolom yang digunakan: 10 kolom

### Kondisi Data:
#### Missing Values:
Terdapat missing values di beberapa kolom seperti:
gold open, gold high, gold low, gold close, gold volume: 185 missing values
usd_chf, eur_usd: 210 missing values
Missing values ini telah diatasi dengan menghapus baris-baris yang mengandung data kosong tersebut.
#### Outlier:
Deteksi outlier dilakukan menggunakan metode IQR (Interquartile Range). Outlier tidak dihapus karena dapat memuat informasi penting dalam data harga emas yang fluktuatif.
#### Duplicate:
Tidak ditemukan data duplikat.


# Data Preparation
- Seleksi Fitur
    Dari total 45 fitur, hanya 10 fitur yang dipilih berdasarkan relevansi terhadap harga emas. Fitur-fitur ini mencakup informasi harga emas itu sendiri serta faktor eksternal seperti 
    indeks saham dan nilai tukar mata uang yang dinilai dapat memengaruhi harga emas.
    #### Uraian Seluruh Fitur pada Dataset
    Dataset awal terdiri dari 45 fitur, berikut adalah deskripsi singkat fitur-fitur utamanya:
    
    💰 Harga Emas
    gold open: Harga pembukaan emas pada hari tersebut
    
    gold high: Harga tertinggi emas pada hari tersebut
    
    gold low: Harga terendah emas pada hari tersebut
    
    gold close: Harga penutupan emas pada hari tersebut (target yang diprediksi)
    
    gold volume: Volume perdagangan emas
    
    📈 Indeks Pasar Saham
    sp500 close: Harga penutupan indeks S&P 500
    
    nasdaq close: Harga penutupan indeks NASDAQ
    
    💱 Nilai Tukar Mata Uang
    usd_chf: Kurs USD terhadap Franc Swiss
    
    eur_usd: Kurs Euro terhadap USD

- Handling Missing Values
    Dataset memiliki missing values terutama pada kolom harga dan volume emas serta kurs mata uang:
    
    Kolom gold open, gold high, gold low, gold close, gold volume: 185 missing values
    
    Kolom usd_chf, eur_usd: 210 missing values
    
    Solusi:
    Baris-baris yang mengandung missing values dihapus agar model tidak terganggu oleh data yang tidak lengkap.

- Handling Outliers
    Outlier dicek menggunakan metode Interquartile Range (IQR). Namun, karena data harga emas sangat fluktuatif secara alami, outlier tidak dihapus, agar tetap merepresentasikan kondisi     pasar yang sesungguhnya.
- Konversi Tipe Data
Kolom date dikonversi menjadi tipe datetime untuk memudahkan analisis waktu bila diperlukan.
- Split Data
  Data dibagi menjadi data latih dan data uji:
  
  80% data digunakan untuk training
  
  20% data digunakan untuk testing

- Feature Scaling
  Tidak dilakukan feature scaling karena model yang digunakan (Random Forest Regressor) tidak sensitif terhadap skala fitur.

## Modeling

Model yang digunakan dalam proyek ini adalah **Random Forest Regressor**, sebuah algoritma yang sering digunakan untuk masalah regresi. Algoritma ini bekerja dengan cara membangun banyak pohon keputusan dan mengambil rata-rata dari hasil prediksi pohon-pohon tersebut. Hal ini dapat mengurangi risiko overfitting dan memberikan hasil prediksi yang lebih stabil.

### Hyperparameter Tuning

Untuk meningkatkan performa model, dilakukan **hyperparameter tuning** menggunakan **GridSearchCV**. Beberapa parameter yang dioptimalkan adalah:

- `n_estimators`: Jumlah pohon dalam hutan.
- `max_depth`: Kedalaman maksimum pohon.
- `min_samples_split`: Jumlah minimum sampel untuk membagi node.
- `min_samples_leaf`: Jumlah minimum sampel di ujung daun.

Setelah melakukan tuning, model terbaik ditemukan dengan kombinasi parameter:
- `n_estimators = 200`
- `max_depth = None`
- `min_samples_split = 2`
- `min_samples_leaf = 1`

## Evaluation

Evaluation
📏 Evaluation Metrics
Untuk mengevaluasi performa model dalam memprediksi harga penutupan emas (gold close), digunakan beberapa metrik regresi berikut:

- MAE (Mean Absolute Error): Rata-rata dari selisih absolut antara nilai aktual dan nilai prediksi.
    Hasil: 2.3899
    
- MSE (Mean Squared Error): Rata-rata dari kuadrat selisih antara nilai aktual dan prediksi.
    Hasil: 13.5483
    
- RMSE (Root Mean Squared Error): Akar dari MSE. Metrik ini memberikan penalti lebih besar untuk error yang besar.
    Hasil: 3.6808

- R² Score (Coefficient of Determination): Menunjukkan seberapa baik model menjelaskan variabilitas dari data target. Nilai mendekati 1 berarti model sangat baik.
    Hasil: 0.9829

🔍 Interpretasi Hasil
- Hasil evaluasi menunjukkan bahwa model Random Forest Regressor yang telah dituning bekerja sangat baik dalam memprediksi harga emas berdasarkan fitur-fitur yang dipilih.

- Nilai MAE dan RMSE yang rendah menunjukkan bahwa prediksi model cukup akurat dan tidak jauh meleset dari nilai aktual.

- Nilai R² Score sebesar 0.98 menunjukkan bahwa model mampu menjelaskan lebih dari 98% variabilitas dari harga emas.

## Visualisasi

Visualisasi hasil prediksi harga emas dibandingkan dengan harga emas aktual pada data testing menunjukkan bahwa model dapat mengikuti pola harga emas dengan cukup baik. Berikut adalah plot perbandingan antara harga emas aktual dan harga emas yang diprediksi oleh model

![download (2)](https://github.com/user-attachments/assets/8b5fa199-3eab-473d-966c-a491bf3f26df)

#### 💼 Relevansi dengan Business Understanding
Model ini dirancang untuk memprediksi harga penutupan emas berdasarkan beberapa indikator ekonomi penting (seperti nilai tukar USD/CHF, EUR/USD, dan indeks pasar saham). Dengan model yang akurat:

- Investor atau trader bisa menggunakan hasil prediksi untuk membantu pengambilan keputusan beli/jual emas.

- Perusahaan atau lembaga keuangan bisa mengelola risiko investasi dan strategi lindung nilai (hedging) dengan lebih baik.

- Model ini juga bisa menjadi dasar sistem rekomendasi investasi logam mulia.

#### ✅ Apakah menjawab Problem Statement?
Ya. Tujuan utama dari proyek ini adalah memprediksi harga penutupan emas dengan akurat menggunakan data finansial historis, dan model yang dibangun berhasil mencapai akurasi tinggi.

#### 🎯 Apakah berhasil mencapai goals?
Ya, model berhasil membangun sistem prediksi harga emas yang cukup akurat dan layak untuk diaplikasikan sebagai alat bantu pengambilan keputusan.

#### 🧩 Dampak solusi
Solusi yang diberikan dapat memberikan nilai tambah pada sektor investasi, membantu pelaku pasar mengambil keputusan berbasis data, dan mempermudah prediksi tren harga di masa depan.
## Kesimpulan
Dengan menggunakan Random Forest Regressor dan setelah melakukan hyperparameter tuning, model ini dapat memprediksi harga emas dengan sangat akurat, mencapai R2 Score sebesar 0.98. Prediksi harga emas ini dapat digunakan oleh para investor untuk membuat keputusan yang lebih baik dalam berinvestasi pada komoditas emas.
