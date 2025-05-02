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

## Data Understanding

Dataset yang digunakan berisi informasi terkait harga emas (open, high, low, close, volume), nilai tukar mata uang (USD/CHF, EUR/USD), serta indeks saham (SP500, NASDAQ) yang mempengaruhi harga emas. Data yang digunakan dalam proyek ini mencakup periode dari tahun 2010 hingga 2024 dengan 3905 record. Beberapa kolom yang dipilih dalam analisis adalah sebagai berikut:

- **Date**: Tanggal data
- **Gold Open, High, Low, Close**: Harga pembukaan, tertinggi, terendah, dan penutupan emas pada hari tersebut.
- **Gold Volume**: Volume perdagangan emas pada hari tersebut.
- **SP500 Close, NASDAQ Close**: Harga penutupan indeks saham S&P 500 dan NASDAQ.
- **USD/CHF, EUR/USD**: Nilai tukar mata uang antara USD dan CHF, serta EUR dan USD.

## Data Preparation

Pada tahap ini, dilakukan pembersihan data untuk menghilangkan missing values atau data yang tidak valid, serta melakukan konversi tipe data yang sesuai. Kolom yang tidak relevan dengan analisis harga emas dihapus. Selanjutnya, data yang tersedia dibagi menjadi dua set: data training dan data testing, yang digunakan untuk melatih model dan mengevaluasi akurasi model tersebut.

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

Setelah model dilatih dengan data training, dilakukan evaluasi dengan menggunakan data testing. Metrik evaluasi yang digunakan adalah:

- **MAE (Mean Absolute Error)**: 2.376
- **MSE (Mean Squared Error)**: 13.481
- **RMSE (Root Mean Squared Error)**: 3.672
- **R² Score**: 0.983

Nilai **R² Score** yang mendekati 1 menunjukkan bahwa model dapat menjelaskan hampir 98% variasi harga emas, yang berarti model ini sangat akurat dalam memprediksi harga emas.

## Visualisasi

Visualisasi hasil prediksi harga emas dibandingkan dengan harga emas aktual pada data testing menunjukkan bahwa model dapat mengikuti pola harga emas dengan cukup baik. Berikut adalah plot perbandingan antara harga emas aktual dan harga emas yang diprediksi oleh model

![download (2)](https://github.com/user-attachments/assets/8b5fa199-3eab-473d-966c-a491bf3f26df)

## Kesimpulan
Dengan menggunakan Random Forest Regressor dan setelah melakukan hyperparameter tuning, model ini dapat memprediksi harga emas dengan sangat akurat, mencapai R2 Score sebesar 0.98. Prediksi harga emas ini dapat digunakan oleh para investor untuk membuat keputusan yang lebih baik dalam berinvestasi pada komoditas emas.
