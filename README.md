# **Predictive-Analytics**

## California Housing Price Prediction

Proyek ini bertujuan untuk membangun model machine learning yang dapat memprediksi nilai median harga rumah di California. Proyek ini mencakup seluruh pipeline data science, mulai dari pembersihan data, analisis eksploratif (EDA), hingga evaluasi berbagai algoritma regresi untuk menemukan model terbaik.

## 📌 Domain Proyek
Kenaikan harga rumah di California yang mencapai 82% sejak 2020 tidak sebanding dengan kenaikan upah rata-rata yang hanya 24%. Hal ini menciptakan urgensi bagi calon pembeli dan investor untuk memiliki alat estimasi harga yang akurat. Proyek ini menggunakan teknik **Predictive Analytics** untuk memberikan estimasi harga properti berdasarkan parameter ekonomi dan geografis.

## 📊 Dataset
Dataset yang digunakan adalah **California Housing Dataset**.
- **Jumlah Data:** 20.640 sampel.
- **Fitur Utama:**
  - `longitude` & `latitude`: Lokasi geografis.
  - `housing_median_age`: Usia rata-rata rumah.
  - `total_rooms` & `total_bedrooms`: Kapasitas ruangan.
  - `median_income`: Pendapatan penduduk di area tersebut.
  - `ocean_proximity`: Lokasi terhadap laut (kategorikal).
- **Target:** `median_house_value` (Harga rumah).

## 🛠️ Langkah Preprocessing
1. **Pembersihan Data:** Menangani *missing values* pada kolom `total_bedrooms`.
2. **Outlier Removal:** Menghapus data pencilan menggunakan metode IQR untuk meningkatkan akurasi model.
3. **Encoding:** Mengubah fitur kategori `ocean_proximity` menjadi numerik menggunakan *One-Hot Encoding*.
4. **Data Splitting:** Membagi data menjadi 80% data latih dan 20% data uji.
5. **Standarisasi:** Menggunakan `StandardScaler` untuk menyamakan skala fitur numerik agar algoritma seperti KNN dan SVR dapat bekerja optimal.

## 🧠 Pemodelan
Dalam proyek ini, saya membandingkan empat algoritma Machine Learning:
1.  **K-Nearest Neighbor (KNN):** Algoritma berbasis jarak.
2.  **Random Forest:** Algoritma berbasis ensemble (bagging) yang tangguh terhadap data non-linear.
3.  **AdaBoost:** Algoritma boosting yang fokus pada perbaikan error di tiap iterasi.
4.  **Support Vector Regression (SVR):** Algoritma yang mencari hyperplane terbaik dalam ruang dimensi tinggi.

## 📈 Evaluasi Model
Performa model diukur menggunakan metrik **Mean Squared Error (MSE)**. Berikut adalah hasil perbandingannya:

| Model | Train MSE | Test MSE |
|---|---|---|
| **KNN** | 2.502e+09 | 4.093e+09 |
| **Random Forest** | 4.881e+08 | 2.871e+09 |
| **AdaBoost** | 3.398e+09 | 3.425e+09 |
| **SVR** | 9.074e+09 | 8.851e+09 |

**Kesimpulan:** Model **Random Forest** memberikan performa terbaik dengan error terendah pada data uji, menjadikannya model yang paling direkomendasikan untuk prediksi harga perumahan ini.

## 🚀 Cara Menjalankan
1. Clone repository ini:
   ```bash
   git clone [https://github.com/Dimskmn/Predictive-Analytics.git](https://github.com/Dimskmn/Predictive-Analytics.git)
