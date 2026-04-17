# Laporan Proyek Predictive Analytics - Dimas Sukmana

## Domain Proyek

Permasalahan perumahan merupakan isu global yang berdampak besar pada kesejahteraan masyarakat, terutama di wilayah dengan kepadatan penduduk yang tinggi dan tingkat urbanisasi yang pesat, seperti California. Keterbatasan lahan, kebijakan perencanaan yang kompleks, dan tingginya permintaan pasar membuat harga properti di wilayah ini melonjak signifikan dalam beberapa dekade terakhir. Menurut _California Legislative Analyst’s Office_ (2024), harga rumah di California berada di antara yang tertinggi di Amerika Serikat, terutama disebabkan oleh keterbatasan pasokan perumahan yang memicu tingginya harga pasar [1].

Selain itu, biaya bulanan untuk rumah kelas menengah di California mencapai hampir $5.900 pada Maret 2024, meningkat sebesar 82% sejak Januari 2020. Untuk rumah kelas bawah, biaya bulanan melebihi $3.500, naik 87% dalam periode yang sama. Peningkatan ini disebabkan oleh kenaikan harga rumah dan suku bunga hipotek yang lebih tinggi. Sementara itu, pertumbuhan upah rata-rata hanya sebesar 24% sejak Januari 2020, menunjukkan bahwa biaya perumahan meningkat lebih cepat daripada pendapatan [1].

Di wilayah Bay Area, harga rumah pemula telah mencapai $1 juta di 59 kota, menjadikannya semakin tidak terjangkau bagi pembeli rumah pertama. Bahkan, rumah pemula di San Francisco memiliki harga sekitar $706.000, dengan perkiraan penurunan harga sebesar 5% pada tahun 2025. Kenaikan harga ini sebagian besar disebabkan oleh faktor-faktor seperti suku bunga hipotek yang rendah selama pandemi, peningkatan tabungan, dan keinginan akan ruang yang lebih luas [2].

Dalam konteks California, tantangan kekurangan perumahan dan tingginya modal ekonomi yang diperlukan ini memiliki implikasi sosial, ekonomi, dan kebijakan yang kompleks. Oleh karena itu, langkah-langkah solutif yang holistik dan berkelanjutan diperlukan untuk mengatasi masalah ini dan memastikan bahwa setiap pembeli rumah pertama di California memiliki akses terhadap perumahan yang terjangkau.

## Business Understanding

Proyek _predictive analytics_ ini bertujuan untuk menganalisis faktor-faktor yang secara signifikan mempengaruhi harga median rumah di berbagai distrik di California. Dengan pemahaman ini, berbagai pihak yang berkepentingan di pasar real estate seperti calon pembeli, penjual, investor, dan pengembang properti dapat membuat keputusan yang lebih informatif dan strategis terkait penilaian dan investasi properti.

### a. Problem Statements

Berdasarkan latar belakang kompleksitas pasar perumahan California yang telah diuraikan sebelumnya, rumusan masalah untuk proyek ini adalah sebagai berikut :

- Algoritma regresi apa yang mampu memberikan performa prediksi terbaik untuk harga rumah di California ?
- Faktor-faktor atau fitur apa saja yang memiliki pengaruh paling signifikan terhadap harga median sebuah distrik perumahan di California ?

### b. Goals

Berdasarkan dengan rumusan masalah yang dijelaskan sebelumnya, tujuan yang ingin dicapai dalam proyek ini adalah :

- Mengidentifikasi algoritma terbaik dengan kemampuan prediksi harga paling dekat dengan nilai aslinya.
- Mengidentifikasi faktor atau fitur yang paling mempengaruhi secara signifikan terhadap harga rumah.

### c. Solution statements

Untuk memenuhi tujuan dari proyek ini, solusi yang diajukan dalam proyek ini sebagai berikut :

- Mengembangkan dan membandingkan empat algoritma regresi: K-Nearest Neighbors (KNN), Random Forest, AdaBoost, dan Support Vector Regression (SVR), untuk menemukan model prediksi harga rumah terbaik di California.
- Memanfaatkan model dengan performa terbaik untuk mengidentifikasi faktor atau fitur paling signifikan yang mempengaruhi harga rumah, diantaranya melalui analisis skor kepentingan fitur.

## Data Understanding

Dataset yang digunakan dalam proyek ini berjudul [California Housing Prices](https://www.kaggle.com/datasets/camnugent/california-housing-prices), yang dapat diakses melalui platform Kaggle. Dataset ini memiliki format CSV (comma separated value) dan terdiri dari 20.640 jumlah baris data/sampel dengan 10 kolom fitur, dimana 9 fitur bertipe numeric sedangkan 1 fitur sisanya bertipe object.

### Variabel-variabel pada dataset California Housing Prices adalah sebagai berikut:

1. `longitude` : Ukuran seberapa jauh sebuah rumah berada di barat; nilai yang lebih tinggi berarti lebih ke barat.
2. `latitude` : Ukuran seberapa jauh sebuah rumah berada di utara; nilai yang lebih tinggi berarti lebih ke utara.
3. `housing_median_age` : Usia median dari rumah-rumah dalam satu blok; nilai yang lebih rendah berarti bangunan lebih baru.
4. `total_rooms` : Jumlah total kamar dalam satu blok.
5. `total_bedrooms` : Jumlah total kamar tidur dalam satu blok. Fitur ini memiliki 207 nilai yang hilang.
6. `population` : Jumlah total orang yang tinggal dalam satu blok.
7. `households` : Jumlah total rumah tangga (keluarga) dalam satu blok.
8. `median_income` : Pendapatan median untuk rumah tangga dalam satu blok (diukur dalam puluhan ribu dolar AS).
9. `ocean_proximity` : Menunjukkan kedekatan lokasi blok dengan laut/samudra (kategorikal).
10. `median_house_value` : Variabel target. Harga median rumah untuk rumah tangga dalam satu blok (dalam dolar AS).

### Exploratory Data Analysis

#### 1. Data Information

| No  | Column             | Non-Null Count | Data Type |
| --- | ------------------ | -------------- | --------- |
| 1   | longitude          | 20640          | float64   |
| 2   | latitude           | 20640          | float64   |
| 3   | housing_median_age | 20640          | float64   |
| 4   | total_rooms        | 20640          | float64   |
| 5   | total_bedrooms     | 20433          | float64   |
| 6   | population         | 20640          | float64   |
| 7   | households         | 20640          | float64   |
| 8   | median_income      | 20640          | float64   |
| 9   | median_house_value | 20640          | float64   |
| 10  | ocean_proximity    | 20640          | object    |

    Tabel 1. Tabel informasi dataset

Dataset `California Housing Prices` memiliki 20640 baris dan 10 kolom. Sebagian besar kolom memiliki tipe data `float64`, yang menunjukkan data numerik. Kolom `ocean_proximity` memiliki tipe data `object`, yang merupakan data kategorikal. Terlihat ada nilai yang hilang (Non-Null Count kurang dari 20640) pada kolom `total_bedrooms`.
Berdasarkan hasil pengecekan, kolom `total_bedrooms` teridentifikasi memiliki 207 nilai yang hilang. Jumlah ini relatif kecil dibandingkan dengan total ukuran dataset, penanganan missing values ini akan dilakukan pada tahap data preprocessing melalui penghapusan baris yang teridentifikasi.

#### 2. Variable Description

![image](https://raw.githubusercontent.com/Dimskmn/Predictive-Analytics/refs/heads/main/images/var-desc.png)

         Gambar 1. Analisis statistik deskriptif

Analisis statistik deskriptif fitur numerik menunjukkan beberapa variabel seperti `total_rooms`, `total_bedrooms`, `population`, dan `households` memiliki nilai maksimum yang jauh lebih besar dari kuartil ketiganya, mengindikasikan kemungkinan _outlier_ dan distribusi yang sangat miring ke kanan. Usia median rumah (`housing_median_age`) adalah sekitar 29 tahun, dengan beberapa mencapai 52 tahun. Pendapatan median (`median_income`) berkisar 0.5 hingga 15, dengan rata-rata 3.87.
Harga median rumah (`median_house_value`) memiliki rentang sangat luas (\$14.999 - \$500.001) dengan variasi signifikan (standar deviasi 115395.6), menandakan perbedaan harga yang besar antar lokasi. `total_bedrooms` juga menunjukkan standar deviasi tinggi, kemungkinan terkait nilai hilang atau _outlier_.

#### 3. Univariate Analysis

##### a. Fitur Kategorikal

![image](https://raw.githubusercontent.com/Dimskmn/Predictive-Analytics/refs/heads/main/images/cat-univariate.png)

         Gambar 2. Analisis univariat fitur kategorikal

Grafik tersebut menyajikan distribusi jumlah sampel untuk setiap kategori dalam fitur `ocean_proximity`. Dari visualisasi diagram batang ini, dapat diambil beberapa informasi penting:

- `<1H OCEAN` (kurang dari 1 jam perjalanan ke laut) menunjukkan bahwa sebagian besar properti, jumlahnya hampir mencapai 9000 sampel.
- `INLAND` (pedalaman) menempati urutan kedua dalam jumlah sampel, dengan lebih dari 6000 properti.
- `NEAR OCEAN` (dekat laut) dan `NEAR BAY` (dekat teluk) memiliki jumlah sampel yang lebih sedikit dibandingkan dua kategori sebelumnya, masing-masing di atas 2000 sampel.
- `ISLAND` memiliki frekuensi yang sangat rendah, hampir tidak terlihat pada grafik, yang mengindikasikan bahwa properti di pulau sangat jarang dalam dataset ini.

##### b. Fitur Numerikal

![image](https://raw.githubusercontent.com/Dimskmn/Predictive-Analytics/refs/heads/main/images/num-univariate.png)

         Gambar 3. Analisis univariat fitur numerikal

Grafik diatas menampilkan serangkaian histogram yang menggambarkan distribusi dari masing-masing fitur numerik dalam dataset harga rumah di California. Dari grafik tersebut, informasi yang dapat diambil adalah sebagai berikut :

- `longitude` & `latitude` : Menunjukkan konsentrasi properti di beberapa area geografis utama California.
- `housing_median_age` : Banyak blok perumahan berusia maksimum (sekitar 52 tahun), dengan distribusi yang cukup merata di rentang usia lainnya.
- `total_rooms`, `total_bedrooms`, `population`, `households` : Semuanya menunjukkan distribusi miring ke kanan, mengindikasikan mayoritas blok memiliki nilai rendah untuk fitur ini dengan beberapa outlier bernilai tinggi.
- `median_income` : Distribusi relatif normal dengan sedikit kemiringan ke kanan; mayoritas pendapatan median terkonsentrasi di nilai tengah.
- `median_house_value` (_Target_) : Miring ke kanan dengan pengelompokan nilai yang signifikan pada batas atas (sekitar $500.000).

#### 4. Multivariate Analysis

##### a. Fitur Kategorikal

![image](https://raw.githubusercontent.com/Dimskmn/Predictive-Analytics/refs/heads/main/images/cat-multivariate.png)

         Gambar 4. Analisis multivariat fitur kategorikal

Grafik diagram batang ini menampilkan rata-rata `median_house_value` (harga median rumah) untuk setiap kategori dalam fitur `ocean_proximity`. Garis hitam di atas setiap batang menunjukkan interval kepercayaan atau variasi data. Dari grafik ini, dapat diambil beberapa informasi penting sebagai berikut:

- `ISLAND` : Kategori ini menunjukkan rata-rata `median_house_value` yang paling tinggi yang mengindikasikan bahwa properti yang berlokasi di pulau cenderung memiliki harga median yang sangat mahal, yaitu sekitar $380.000.
- `NEAR BAY` : Properti yang berlokasi di dekat teluk memiliki rata-rata `median_house_value` tertinggi kedua, sekitar $260.000.
- `NEAR OCEAN` : Kategori ini memiliki rata-rata `median_house_value` yang juga tinggi, sedikit di bawah kategori NEAR BAY, yaitu sekitar $250.000.
- `<1H OCEAN` : Properti yang berlokasi kurang dari satu jam perjalanan dari laut memiliki rata-rata `median_house_value` yang lebih rendah dibandingkan `NEAR BAY` dan `NEAR OCEAN`, yaitu sekitar $240.000.
- `INLAND` : Kategori ini menunjukkan rata-rata `median_house_value` yang paling rendah, yaitu sekitar $125.000. Ini menunjukkan bahwa properti yang berlokasi di pedalaman cenderung memiliki harga yang jauh lebih terjangkau dibandingkan dengan yang dekat dengan perairan (laut atau teluk).

##### b. Fitur Numerikal

![image](https://raw.githubusercontent.com/Dimskmn/Predictive-Analytics/refs/heads/main/images/correlation.png)

         Gambar 5. Analisis multivariat correlation matrix

Warna pada _Correlation Matrix_ menunjukkan arah dan kekuatan korelasi, dengan warna merah tua mengindikasikan korelasi positif kuat, biru tua mengindikasikan korelasi negatif kuat, dan warna mendekati putih menunjukkan korelasi yang lemah atau tidak ada. Angka di dalam setiap sel adalah nilai koefisien korelasi. Informasi yang dapat diambil dari matriks ini adalah:

- Hubungan dengan median_house_value (Target):
  - median_income berkorelasi positif paling kuat (0.69).
  - total_rooms (0.13) dan housing_median_age (0.11) berkorelasi positif sangat lemah.
  - households (0.07) dan total_bedrooms (0.05) memiliki korelasi positif yang sangat rendah.
  - longitude (-0.05), latitude (-0.14), dan population (-0.02) menunjukkan korelasi negatif yang sangat lemah.
- Multikolinearitas Antar Fitur Prediktor:
  - longitude dan latitude memiliki korelasi negatif sangat kuat (-0.92).
- Korelasi Lainnya:
  - housing_median_age berkorelasi negatif sedang (-0.3 hingga -0.36) dengan total_rooms, total_bedrooms, population, dan households.

## Data Preparation

Pada bagian ini tahapan-tahapan yang dilakukan dalam mempersiapkan data sebelum dilakukan pemodelan adalah sebagai berikut :

1.  **Mengatasi _Missing Values_**
    Berdasarkan analisis data eksploratif sebelumnya, teridentifikasi bahwa kolom `total_bedrooms` memiliki nilai yang hilang (_missing values_). Secara spesifik, terdapat 207 baris yang tidak memiliki data pada kolom ini. Mengingat jumlah total baris dalam dataset adalah 20.640, proporsi data yang hilang ini relatif kecil, yaitu sekitar 1% dari keseluruhan dataset.
    Untuk menangani nilai yang hilang ini, pendekatan penghapusan baris (_row deletion_ atau _listwise deletion_) diaplikasikan. Ini berarti seluruh baris yang mengandung nilai kosong pada kolom `total_bedrooms` akan dihilangkan dari dataset. Dengan menghapus baris-baris tersebut, dataset yang digunakan untuk tahap selanjutnya menjadi lebih bersih dan setiap entri memiliki informasi yang lengkap untuk semua fitur yang relevan.

2.  **Mengatasi _Outliers_**
    ![image](https://raw.githubusercontent.com/Dimskmn/Predictive-Analytics/refs/heads/main/images/box-visualization.png)

            Gambar 6. Visualisasi fitur numerik pada boxplot

        Setelah penanganan nilai yang hilang, langkah selanjutnya dalam persiapan data adalah mengatasi adanya nilai ekstrim (*outlier*). Visualisasi data pada boxplot, telah mengungkapkan keberadaan outlier pada beberapa fitur numerik. *Outilers* ini terutama terdeteksi pada variabel-variabel yang berkaitan dengan ukuran properti, seperti `total_rooms`, `total_bedrooms`, `population`, dan `households`, serta pada fitur `median_income` dan variabel target `median_house_value`. Boxplot secara visual menyoroti adanya nilai-nilai data yang berada jauh di luar rentang interkuartil (IQR), yang mengindikasikan potensi keberadaan anomali atau nilai ekstrem. Nilai-nilai ekstrem ini perlu ditangani karena dapat memberikan dampak negatif pada keandalan dan performa model prediktif yang akan dibangun.
        Untuk mengidentifikasi dan menangani outlier ini, metode Interquartile Range (IQR) digunakan. Metode IQR bekerja dengan menetapkan ambang batas berdasarkan kuartil pertama (Q1) dan kuartil ketiga (Q3) dari distribusi data pada masing-masing fitur. Secara spesifik, sebuah nilai dianggap sebagai outlier jika berada di bawah Q1 - 1.5 * IQR atau di atas Q3 + 1.5 * IQR. Observasi (baris) yang mengandung nilai outlier pada fitur-fitur numerik yang telah teridentifikasi akan dihapus dari dataset.
        Prosedur penghapusan baris yang mengandung outlier ini bertujuan untuk membersihkan data dari nilai-nilai ekstrem yang berpotensi mengganggu kinerja dan akurasi model machine learning. Setelah proses ini, jumlah baris dalam dataset akan berkurang, namun diharapkan dataset yang dihasilkan menjadi lebih robust dan representatif terhadap pola data yang umum.

3.  **_One-Hot Ecoding_**
    Fitur kategorikal dalam dataset, yaitu `ocean_proximity`, perlu diubah menjadi format numerik agar dapat diproses oleh sebagian besar algoritma _machine learning_ yang berbasis operasi matematika. Untuk tujuan ini, metode _One-Hot Encoding_ diterapkan.
    Proses _One-Hot Encoding_ bekerja dengan menciptakan kolom-kolom biner baru untuk setiap kategori unik yang ada dalam fitur `ocean_proximity`. Setiap kolom baru ini akan mewakili satu kategori, dan nilainya akan menjadi 1 jika kategori tersebut ada pada baris data yang bersangkutan, dan 0 jika tidak. Sebagai contoh, jika kategori dalam `ocean_proximity` adalah 'NEAR BAY', 'INLAND', '<1H OCEAN', 'ISLAND', 'NEAR OCEAN' maka akan dibuat lima kolom baru. Jika suatu properti memiliki nilai `ocean_proximity` 'NEAR BAY', maka kolom 'NEAR BAY' akan bernilai 1, sementara kolom 'INLAND', '<1H OCEAN' dan yang lainnya akan bernilai 0 untuk properti tersebut.
    Langkah ini krusial untuk memastikan bahwa informasi kategorikal dapat diinterpretasikan dengan benar oleh model tanpa menimbulkan asumsi urutan atau bobot tertentu antar kategori. Dengan demikian, _One-Hot Encoding_ membantu menyiapkan data non-numerik agar kompatibel dan efektif untuk digunakan dalam pelatihan model _machine learning_.

4.  **Reduksi Dimensi dengan PCA**
    ![image](https://raw.githubusercontent.com/Dimskmn/Predictive-Analytics/refs/heads/main/images/PCA.png)

            Gambar 7. Visualisasi relasi antara fitur 'longitude' dan 'latitude'

        Untuk menyederhanakan representasi spasial, fitur `longitude` dan `latitude` direduksi dimensinya menjadi satu fitur gabungan tunggal bernama `coordinate` menggunakan Principal Component Analysis (PCA). Langkah ini bertujuan menangkap variasi utama dari kedua fitur geografis tersebut dalam satu variabel, menyederhanakan input model sambil tetap mempertahankan informasi lokasi yang penting.

5.  **_Data Splitting_**
    Tahap pembagian data memisahkan dataset menjadi dua subset: data training (90%) dan data testing (10%). Proses ini dilakukan menggunakan `train_test_split` dengan `random_state` tertentu untuk memastikan hasil yang dapat direproduksi. Pembagian ini krusial agar model dilatih hanya pada data training dan kemudian dievaluasi performanya secara objektif pada data testing yang belum pernah dilihat sebelumnya, memberikan estimasi kinerja model di dunia nyata.

6.  **_Standardization_ (Normalisasi)**
    Tahap Standardization menyeragamkan skala fitur-fitur numerik menggunakan `StandardScaler`. Proses ini mentransformasi data sedemikian rupa sehingga setiap fitur memiliki rata-rata nol dan standar deviasi satu. Penerapan scaler ini hanya dilatih pada data training dan kemudian diterapkan pada data testing untuk mencegah data leakage, memastikan bahwa model tidak mendapatkan informasi tentang distribusi data testing sebelum evaluasi. Standardization penting agar fitur dengan skala berbeda tidak mendominasi dalam proses pelatihan model, khususnya pada algoritma yang sensitif terhadap skala.

## Modeling

Seperti yang telah dijelaskan di awal, proyek ini akan membuat pemodelan dengan menggunakan 4 algoritma yang berbeda, yaitu K-Nearest Neighbour (KNN), RandomForest Regressor, AdaBoostRegressor, dan Suport Vector Regressor (SVR).

- _K-Nearest Neighbour (KNN)_
  Algoritma K-Nearest Neighbors (KNN) bekerja dengan cara menghitung jarak antara satu data uji terhadap seluruh data pelatihan, kemudian memilih sejumlah tetangga terdekat sebanyak k (dengan k merupakan bilangan positif) [3]. Algoritma ini umum digunakan untuk menyelesaikan masalah klasifikasi maupun regresi. Dalam konteks klasifikasi, label yang diberikan pada data baru ditentukan berdasarkan mayoritas label dari k tetangga terdekatnya. Sementara itu, jika digunakan untuk regresi, nilai prediksi dari data baru dihitung sebagai rata-rata dari nilai target tetangga-tetangga terdekat tersebut.
  Kelebihan utama dari KNN terletak pada kesederhanaan konsep dan kemudahan implementasinya [4]. Selain itu, algoritma ini cukup efektif dalam menangani data dengan pola yang tidak linier. Meski demikian, KNN memiliki beberapa keterbatasan, antara lain performanya yang menurun pada dataset berukuran besar serta sensitivitasnya terhadap perbedaan skala antar fitur dan terhadap keberadaan outlier [4].
  Pada proyek ini, library `sklearn.neighbors` digunakan untuk mengimport fungsi algoritma `KNeighborsRegressor`. Tahap pertama yang dilakukan adalah menentukan parameter `n_neighbors`, dimana untuk proyek ini `n_neighbors = 10`. Parameter `n_neighbors` sendiri merupakan jumlah k tetangga tedekat yang merupakan parameter terpenting dalam algoritma KNN. Selanjutnya, untuk menjalankan training model menggunakan perintah
  `   knn.fit(X_train, y_train)
`
- _RandomForest Regressor_
  Algoritma Random Forest merupakan metode supervised learning yang termasuk dalam kelompok ensemble models, di mana model dibangun dari kumpulan pohon keputusan (decision trees) yang masing-masing dilatih dengan subset data dan fitur yang dipilih secara acak [3]. Pada proses prediksi, setiap pohon menghasilkan prediksi sendiri, kemudian hasil akhir ditentukan berdasarkan mayoritas suara (untuk klasifikasi) atau rata-rata nilai prediksi dari seluruh pohon (untuk regresi).
  Keunggulan utama dari Random Forest adalah kemampuannya dalam menangani data yang mengandung noise maupun nilai yang hilang (missing values), serta performanya yang baik pada dataset berskala besar [5]. Selain itu, algoritma ini cenderung tidak mudah mengalami overfitting dan dapat memberikan wawasan mengenai tingkat kepentingan (importance) dari setiap fitur dalam proses prediksi. Meski demikian, kelemahan dari algoritma ini terletak pada tingkat kompleksitasnya yang tinggi, sehingga interpretasi hasil menjadi lebih sulit [5]. Selain itu, performa optimal Random Forest bergantung pada proses penyetelan parameter (hyperparameter tuning) yang tepat.
  Pada proyek ini, library `sklearn.ensemble` digunakan untuk mengimport fungsi algoritma `RandomForestRegressor`. Kemudian dilakukan hyperparameter tuning seperti `n_estimators`, `max_depth`, `min_samples_split`, `min_samples_leaf`, `max_features`,`random_state` dan `n_jobs`. - Parameter `n_estimators` merupakan jumlah trees (pohon) di forest dan proyek ini menggunakan `n_estimator = 150`. - Parameter `max_depth` adalah kedalaman maksimum setiap pohon dimana untuk proyek ini menggunakan `max_depth = 10`. - Parameter `min_samples_split` adalah jumlah sampel minimum yang diperlukan untuk memecah node internal, proyek ini menggunakan `min_samples_split = 2`. - Parameter `min_samples_leaf` adalah jumlah sampel minimum yang diperlukan di node daun, proyek ini menggunakan `min_samples_leaf = 2`. - Parameter `max_features` adalah proporsi fitur yang dipertimbangkan saat mencari pemecahan terbaik (50%), proyek ini menggunakan `max_features = 0.5`. - Parameter `random_state` digunakan untuk mengontrol random number generator yang digunakan dan proyek ini menggunakan `random_state = 55`. - Parameter `n_jobs` adalah jumlah job (pekerjaan) yang digunakan secara paralel. Proyek ini menggunakan `n_jobs = -1` yang artinya semua proses berjalan secara bersamaan/paralel.

      Selanjutnya, setelah seluruh parameter selesai diatur, untuk membangun model Random Forest akan dijalankan perintah
      ```
      RF.fit(X_train, y_train)
      ```

- _AdaBoostRegressor_
  Algoritma boosting merupakan metode pembelajaran ansambel yang bekerja dengan cara membangun sejumlah model secara berurutan. Model awal dilatih menggunakan data latih, dan model-model berikutnya dirancang untuk memperbaiki kesalahan prediksi yang dibuat oleh model sebelumnya. Proses ini terus berlanjut hingga model mampu memprediksi data latih dengan baik atau hingga tercapai jumlah maksimum iterasi yang telah ditentukan [3].
  Pada algoritma AdaBoost, semua data latih pada awalnya diberikan bobot yang sama. Setelah model lemah pertama dilatih, bobot dari data yang salah diklasifikasikan akan ditingkatkan, sehingga model selanjutnya akan lebih fokus pada data yang sulit diprediksi. Proses pembobotan dan pelatihan ini diulang dalam beberapa iterasi. Ketika melakukan prediksi, masing-masing model lemah akan memberikan kontribusi sesuai dengan tingkat akurasinya, dan hasil akhir diperoleh melalui agregasi prediksi yang dibobot berdasarkan performa setiap model.
  AdaBoost memiliki sejumlah kelebihan, antara lain kemampuannya dalam meningkatkan akurasi prediksi, mengurangi risiko overfitting, serta fleksibilitas dalam menggunakan berbagai jenis model lemah [6]. Selain itu, algoritma ini cukup efektif untuk menangani dataset yang tidak seimbang. Meski demikian, AdaBoost cenderung sensitif terhadap noise dan outlier, yang dapat memengaruhi stabilitas prediksinya [6].
  Pada proyek ini, library `sklearn.ensemble` digunakan untuk mengimport fungsi algoritma `AdaBoostRegressor`. Kemudian dilakukan parameter tuning `learning_rate`, dan `random_state`. - Parameter `learning_rate` merupakan bobot yang diterapkan pada setiap _regressor_ di masing-masing proses iterasi _boosting_ dimana untuk proyek ini menerapkan `learning_rate = 0.1`. - Parameter `random_state` digunakan untuk mengontrol _random number generator_ yang digunakan untuk menjaga kekonsistenan dan proyek ini menerapkan `random_state = 55`.

  Selanjutnya, setelah seluruh parameter berhasil diatur, untuk membangun model AdaBoost akan dijalankan perintah

  ```
  adaboosting.fit(X_train, y_train)
  ```

- _Suport Vector Regressor (SVR)_
  Support Vector Regression (SVR) adalah salah satu metode _supervised learning_ yang merupakan pengembangan dari algoritma Support Vector Machine (SVM), dan digunakan untuk menyelesaikan permasalahan regresi. Tujuan utama dari SVR adalah membangun sebuah fungsi prediksi yang memiliki deviasi maksimal sebesar ε (epsilon) dari nilai aktual target, sambil tetap menjaga kompleksitas model seminimal mungkin [7].
  Pada prinsip kerjanya, SVR mencoba mencari sebuah hyperplane yang meminimalkan kesalahan prediksi di luar margin toleransi ε. Prediksi yang berada di dalam batas margin dianggap cukup baik dan tidak dikenakan penalti, sedangkan prediksi di luar margin akan dikenakan penalti proporsional tergantung jaraknya terhadap margin tersebut. Untuk menangani hubungan non-linier, SVR dapat menggunakan fungsi kernel (seperti RBF) untuk memetakan data ke ruang berdimensi lebih tinggi agar hubungan linier dapat ditemukan di ruang tersebut [7][8].
  SVR memiliki keunggulan dalam memodelkan hubungan non-linier dan cukup tahan terhadap outlier kecil, serta menunjukkan performa generalisasi yang baik. Namun, algoritma ini kurang efisien untuk data berukuran besar, sensitif terhadap pemilihan parameter, dan sulit untuk diinterpretasikan karena kompleksitas modelnya [7].
  Pada proyek ini, library `sklearn.svm` digunakan untuk mengimport fungsi algoritma `SVR`. Kemudian dilakukan parameter tuning `degree`, dan `epsilon`. - Parameter `degree` merupakan derajat fungsi polinomial yang akan digunakan untuk mentransformasi data, untuk proyek ini menerapkan `degree = 5`. - Parameter `epsilon` digunakan untuk menentukan lebar "epsilon-tube" di sekitar garis regresi yang diprediksi (kesalahan dalam jarak ini tidak dikenakan penalti) dan proyek ini menerapkan `epsilon = 0.5`.

  Selanjutnya, setelah seluruh parameter berhasil diatur, untuk membangun model AdaBoost akan dijalankan perintah

  ```
  SVR.fit(X_train, y_train)
  ```

Alasan Pemilihan Algoritma tersebut ialah:

- `K-Nearest Neighbors` dipilih karena kesederhanaan prinsip kerjanya, serta kemampuannya dalam menangani data dengan pola non-linier tanpa perlu proses pelatihan yang kompleks. KNN juga mudah diimplementasikan dan memberikan hasil yang cukup baik pada dataset berskala kecil hingga menengah.
- `Random Forest` dipilih karena kemampuannya dalam memproses data berdimensi tinggi dan kompleks secara efektif. Algoritma ini juga mampu mengurangi varians model melalui pendekatan ensemble, serta menyediakan informasi penting mengenai kontribusi masing-masing fitur terhadap hasil prediksi.
- `AdaBoost` digunakan karena keefektifannya dalam meningkatkan akurasi model prediksi dengan menggabungkan beberapa model lemah secara iteratif. Selain itu, algoritma ini dapat mengurangi risiko overfitting dan bekerja dengan baik pada dataset yang memiliki distribusi kelas yang tidak seimbang.
- `Support Vector Regression` dipilih karena kemampuannya dalam memodelkan hubungan non-linier secara fleksibel melalui penggunaan fungsi kernel. SVR juga dikenal memiliki performa generalisasi yang baik dan relatif tahan terhadap outlier kecil, menjadikannya cocok untuk regresi dengan data yang tidak sepenuhnya terdistribusi secara linier.

## Evaluation

Pada proyek ini, metrik yang digunakan untuk menghitung serta menampilkan hasil proses evaluasi adalah Mean Squared Error (MSE) dari masing-masing model pada algoritma yang dijalankan. Mean Squared Error (MSE) merupakan alat untuk mengukur tingkat error yang terjadi dalam model statistik dengan cara menghitung jumlah selisih kuadrat rata-rata nilai sebenarnya dengan nilai prediksi [3]. MSE didefinisikan dalam persamaan berikut :

$$
\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} \left( y_i - ypred_i \right)^2
$$

Keterangan:

- \( n \) : jumlah data
- \( y_i \) : nilai aktual pada data ke-\( i \)
- \( ypred_i \) : nilai prediksi pada data ke-\( i \)

Semakin kecil nilai MSE, maka semakin baik performa model dalam melakukan prediksi. Hasil perhitungan MSE pada data latih dan data uji dari masing-masing algoritma ditampilkan pada Tabel 1 dibawah ini.

| Model       | MSE Data Latih | MSE Data Uji   |
| ----------- | -------------- | -------------- |
| KNN         | 2313994.530776 | 2721791.745701 |
| RF          | 1747114.417286 | 2363565.449537 |
| AdaBoosting | 4167215.125633 | 3982864.983359 |
| SVR         | 9035975.230688 | 8697667.120081 |

    Tabel 2. Tabel evaluasi MSE data latih dan data uji dari masing-masing algoritma

![image](https://raw.githubusercontent.com/Dimskmn/Predictive-Analytics/refs/heads/main/images/model-plot.png)

    Gambar 8. Grafik evaluasi MSE data latih dan data uji dari tiap algoritma

Dari Tabel 1 dan Gambar 7, dapat dilihat algoritma _Random Forest_ memiliki tingkat _error_ yang lebih rendah dibandingkan dengan algoritma lainnya, dengan tingkat _error_ pada data latih sebesar 1747114.417286 dan tingkat _error_ pada data uji sebesar 2363565.449537.
Model `RandomForest` adalah model yang paling unggul dalam memprediksi harga rumah pada dataset ini, diikuti oleh model `KNN`. Model `AdaBoosting` dan `SVR` menunjukkan performa yang kurang memuaskan dibandingkan kedua model tersebut. Pemilihan model terbaik untuk tugas prediksi harga rumah ini jatuh pada `RandomForest` berkat nilai `MSE` testing-nya yang paling rendah.

## Feature Importance

Setelah model terbaik diidentifikasi, analisis terhadap feature importances dilakukan untuk memahami faktor-faktor mana yang memiliki pengaruh paling besar dalam memprediksi harga rumah di California. Hasil analisis dapat dilihat pada tabel 2 dibawah ini.
| No | Feature | Importance |
|----|----------------------------------|--------------|
| 1 | median*income | 0.380533 |
| 2 | ocean_proximity_INLAND | 0.204061 |
| 3 | coordinate | 0.176961 |
| 4 | housing_median_age | 0.061176 |
| 5 | population | 0.051788 |
| 6 | total_rooms | 0.039777 |
| 7 | total_bedrooms | 0.035693 |
| 8 | households | 0.032941 |
| 9 | ocean_proximity_NEAR OCEAN | 0.009450 |
| 10 | ocean_proximity*<1H OCEAN | 0.004906 |
| 11 | ocean_proximity_NEAR BAY | 0.001744 |
| 12 | ocean_proximity_ISLAND | 0.000970 |
Tabel 3. Tabel feature importance yang di ekstrak dari model RandomForest
Fitur yang paling berpengaruh dalam memprediksi harga rumah `median_house_value` adalah `median_income`. Ini menunjukkan bahwa pendapatan median rumah tangga di suatu area merupakan faktor kunci dalam menentukan nilai properti di California. Fitur lainnya seperti koordinat geografis `coordinate` dan usia rumah `housing_median_age` juga memiliki kontribusi yang signifikan, tetapi tidak sebesar pendapatan.

## Demonstrasi Prediksi pada Data Tunggal

Untuk memberikan gambaran praktis mengenai bagaimana model-model yang telah dilatih bekerja dalam melakukan prediksi pada data individual, sebuah demonstrasi inferensi dilakukan. Dalam demonstrasi ini, satu sampel data diambil dari data uji (`X_test`) yang tidak digunakan selama proses pelatihan model. Fitur-fitur dari sampel data tunggal ini kemudian dijadikan input untuk setiap model regresi yang telah dikembangkan (`KNeighborsRegressor`, `RandomForestRegressor`, `AdaBoostRegressor`, dan `Support Vector Regression`).
Setiap model kemudian menghasilkan nilai prediksi harga rumah (`median_house_value`) untuk sampel data tersebut. Hasil prediksi dari masing-masing model dibandingkan dengan nilai harga rumah aktual (`y_true`) dari sampel data uji yang bersangkutan.
| y_true | Prediksi KNN | Prediksi RF| Prediksi AdaBoosting| Prediksi SVR|
|-----------|----------------|-------------|------------------------|---------------|
| 75500.0 | 84200.0 | 73726.3 | 95191.9 | 169577.4 |
Tabel 4. Tabel Prediksi model pada data tunggal
Pada satu sampel uji (nilai aktual 75500), model `RandomForest` memberikan prediksi terdekat (73726.3), diikuti `KNN` dan `AdaBoosting`. `SVR` menunjukkan prediksi yang paling jauh. Ini mendukung performa `RandomForest` sebagai model yang terbaik.

## Kesimpulan

Proyek ini berhasil mengembangkan dan mengevaluasi empat model regresi untuk memprediksi harga rumah di California menggunakan dataset _California Housing Prices_. Dari hasil eksplorasi data, diketahui bahwa variabel `median_income` merupakan fitur paling berpengaruh dalam menentukan harga rumah, diikuti oleh `ocean_proximity`, `coordinate`, dan `housing_median_age`.

Empat algoritma yang digunakan meliputi K-Nearest Neighbors (KNN), Random Forest, AdaBoost, dan Support Vector Regression (SVR). Berdasarkan evaluasi menggunakan metrik Mean Squared Error (MSE), algoritma Random Forest terbukti menjadi model paling unggul dengan MSE paling rendah pada data uji. Hasil ini juga diperkuat dengan uji prediksi pada satu data individual, di mana prediksi dari Random Forest paling mendekati nilai aktual dibandingkan model lainnya.

## Referensi

[1] California Legislative Analyst’s Office, “California Housing Affordability Tracker (1st Quarter 2025)”, 2025. [Online]. Available: https://lao.ca.gov/LAOEconTax/Article/Detail/793.

[2] J. Dineen, “Want a Bay Area starter home? In these 59 cities, it'll cost you at least $1 million,” _San Francisco Chronicle_, 2025. [Online]. Available: https://www.sfchronicle.com/personal-finance/article/starter-home-down-payment-california-20311305.php.

[3] dicoding. "Rangkuman Studi Kasus Pertama: Predictive Analytics". Available: https://www.dicoding.com/academies/319/tutorials/18600.

[4] Medium. "Klasifikasi menggunakan Metode KNN (K-Nearest Neighbor) dalam Python". Available: https://medium.com/@16611130/klasifikasi-menggunakan-metode-knn-k-nearest-neighbor-dalam-python-a40e79a74101.

[5] Medium. "What is Random Forest Regression?". Available: https://medium.com/@maniksonituts/what-is-random-forest-regression-d5cdabd04c0c.

[6] Medium. "AdaBoostRegressor and Classifier with python and r programming". Available: https://medium.com/@reddyyashu20/adaboostregressor-and-classifier-with-python-and-r-programming-8c4d49f3a50d.

[7] B. M. Patil and R. S. Meshram, “A comparative study on prediction of house prices using machine learning algorithms,” _Materials Today: Proceedings_, vol. 78, pp. 628–634, 2024. [Online]. Available: https://doi.org/10.1016/j.matpr.2023.10.490

[8] R. Kavitha, S. Sasikala, and S. Sudha, “House price prediction using Support Vector Regression with optimized features,” _Materials Today: Proceedings_, vol. 66, pp. 4876–4880, 2023. [Online]. Available: https://doi.org/10.1016/j.matpr.2022.09.217
