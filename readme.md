
# Laporan Proyek Machine Learning Terapan - Indradi Rahmatullah
## Predictive Analysis

## Domain Proyek
Menurut Organisasi Kesehatan Dunia (WHO), stroke merupakan penyebab kematian terbanyak ke-2 di dunia, yang menyebabkan sekitar 11% dari total kematian.

Proyek ini berfokus pada analisis data kesehatan untuk memprediksi risiko stroke pada individu berdasarkan faktor-faktor risiko yang relevan, seperti usia, riwayat medis, gaya hidup, dan kondisi kesehatan lainnya. Dengan menggunakan teknik pembelajaran mesin, proyek ini bertujuan untuk membantu penyedia layanan kesehatan mengidentifikasi individu dengan risiko tinggi sehingga tindakan pencegahan dapat dilakukan lebih dini. 

Oleh karena itu, diperlukan model prediksi risiko stroke yang lebih akurat. Pembelajaran mesin (ML) dapat memberikan solusi untuk hal ini dengan memanfaatkan basis data yang ada untuk membangun model prediksi risiko stroke yang akurat dan mengidentifikasi faktor risiko baru untuk stroke [1](https://www.sciencedirect.com/science/article/pii/S1386505625000280).

## Business Understanding

### Problem Statements
Bagaimana mengetahui pasien memiliki penyakit _Stroke_ berdasarkan riwayat dari variabel-variabel kesehatan yang ada?

### Goals
Untuk menyelesaikan permasalahan yang telah dijabarkan, adapun tujuan yang ingin dicapai sebagai berikut:
1. Mengembangkan model prediksi stroke berdasarkan riwayat kesehatannya.
2. Menganalisis variabel yang paling berpengaruh terhadap kemungkinan terjadinya stroke.

### Solution statements
1. Menggunakan dataset Stroke Prediction Dataset untuk eksplorasi dan analisis faktor-faktor risiko stroke.
2. Melakukan pra-pemrosesan data seperti penanganan nilai hilang, normalisasi, dan encoding variabel kategori.
3. Menggunakan algoritma pembelajaran mesin (**_Decision Tree_**, **_Logistic Regression_**, dan **_Support Vector Machine_**) untuk membangun model prediksi stroke.
4. Mengevaluasi performa model dengan metrik seperti akurasi untuk memastikan efektivitas prediksi.
5. Menyajikan hasil analisis dalam bentuk visualisasi dan interpretasi model untuk memberikan wawasan yang dapat digunakan oleh praktisi kesehatan.

## Data Understanding
Dataset yang digunakan pada proyek _machine learning_ merupakan **5110 data observasi** yang didapat dari situs [kaggle](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset). Terdapat 12 fitur yang dapat digunakan untuk memprediksi kemungkinan penyakit jantung. 

**Variabel-variabel pada Stroke Prediction Dataset adalah sebagai berikut:**
1) id: unique identifier
2) gender: "Male", "Female" or "Other"
3) age: age of the patient
4) hypertension: 0 if the patient doesn't have hypertension, 1 if the patient has hypertension
5) heart_disease: 0 if the patient doesn't have any heart diseases, 1 if the patient has a heart disease
6) ever_married: "No" or "Yes"
7) work_type: "children", "Govt_jov", "Never_worked", "Private" or "Self-employed"
8) Residence_type: "Rural" or "Urban"
9) avg_glucose_level: average glucose level in blood
10) bmi: body mass index
11) smoking_status: "formerly smoked", "never smoked", "smokes" or "Unknown"*
12) stroke: 1 if the patient had a stroke or 0 if not

### Explanatory Data Analysis
Untuk memahami data _heart disease_ dilakukan visualisasi menggunakan _bar chart_ dan _pie chart_. Dalam memvisualisasikannya, dilakukan dengan _Univariate Analysis_ dan _Multivariate Analysis_. Untuk keseluruhannya, dataset dibagi menjadi dua fitur, yakni fitur _categorical_ dan fitur _numerical_.

#### *Univariate Analysis - Categorical Feature*

1. _Univariate Analysis_ terhadap Heart Disease
![ua_heart_disease](https://user-images.githubusercontent.com/57740421/191168520-1c8543ce-27e3-4065-9584-c6faabf68804.png)	

Perlu diketahui bahwa variabel `target` dari _predictive analysis_ yang dilakukan adalah `HeartDisease`. Dari _plot_ yang dibuat, dapat diketahui bahwa data lebih banyak menunjukkan kondisi _heart disease_ [1] dibanding kondisi normal [0]. Dari _plot_ yang dibuat, dapat diketahui bahwa distribusi jenis kelamin yang lebih banyak menunjukkan kondisi _heart disease_ adalah Pria, dibandingkan Wanita. Hal ini disebabkan karena data Pria lebih banyak dibanding Wanita.

2. _Univariate Analysis_ terhadap Jenis Kelamin
![ua_sex](https://user-images.githubusercontent.com/57740421/191168460-1bf2f4e5-a00c-41e1-8563-578eb09caaf4.png)	

Dari _pie plot_ yang dibuat, ditunjukkan bahwa Wanita memiliki penyakit jantung 3x lebih rendah dibandingkan Pria.

3. _Univariate Analysis_ terhadap Sakit Dada
![ua_chestpaintype](https://user-images.githubusercontent.com/57740421/191168583-a773a3f4-b9a7-4eb2-9781-55bd46dab30a.png)	

Dapat dilihat dari _bar plot_ dan _pie plot_ bahwa tipe sakit dada atau `ChestPainType` yang banyak ditemukan atau memiliki keluhan diderita paling tinggi adalah `ASY` atau _Asymptomatic_ sebesar 54%.

4. _Univariate Analysis_ terhadap ECG
![ua_ecg](https://user-images.githubusercontent.com/57740421/191168621-66258908-c108-41ff-b15c-341587b144af.png)	

Pada variabel `RestingECG` terdapat 3 level tekanan darah, yakni Normal, LVH, dan ST. Dari dua _plot_ yang menyajikan ketiga level tersebut, dapat diketahui bahwa kategori Normal memiliki mayoritas distribusi, yakni sebesar 63.8%.

5. _Univariate Analysis_ terhadap Angina
![ua_angina](https://user-images.githubusercontent.com/57740421/191168654-cbe05350-bcd5-4ca2-86c3-24f692121fb6.png)	

Pada variabel `ExerciseAngina` yang disajikan oleh dua _plot_, dapat diketahui bahwa lebih banyak yang melakukan latihan angina, yakni sebesar 65.0%

6. _Univariate Analysis_ terhadap ST Slope
![ua_slope](https://user-images.githubusercontent.com/57740421/191168732-b10f81cf-2664-4d90-b09e-f39309a0305a.png)

Pada variabel `ST_Slope` yang disajikan oleh dua _plot_, dapat diketahui bahwa `Flat` lebih banyak yang memiliki kemiringan pada puncak segmen ST, yakni sebesar 51.6%

#### *Multivariate Analysis - Categorical Feature*
Dengan mengamati rata-rata harga relatif terhadap fitur _categorical_ di atas, didapatkan _insight_ sebagai berikut:

Heart Disease [0] menunjukkan bahwa pasien Normal. Heart Disease [1] menunjukkan bahwa pasien memiliki penyakit jantung.

- Pada fitur `sex`, rerata penyakit jantung atau _heart disease_ menyerang seseorang berjenis kelamin pria, dibanding wanita. Hal ini dapat dilihat pada bar chart [1] yang melambangkan pasien memiliki penyakit jantung. Pada pasien normal (tidak memiliki penyakit jantung, dilambangkan dengan [0]), rerata didominasi dengan pria. Hal yang sama juga terjadi pada pasien dengan penyakit jantung (dilambangkan dengan [1]), yang rerata didominasi dengan pria.

![mu_sex](https://user-images.githubusercontent.com/57740421/191168808-fa8afffc-e0d4-46d9-8b78-8d145a178276.png)

- Pada fitur `ChestPainType`, rerata pasien yang memiliki penyakit jantung (dilambangkan dengan [1]) memiliki sakit dada dengan tipe _Asymptomatic_ [ASY] sebannyak 392 kasus.

![mu_chestpaintype](https://user-images.githubusercontent.com/57740421/191168845-ac521103-35cd-4a4e-8764-3f6cc8ae53e5.png)

- Pada fitur `FastingBS`, rerata pasien yang memiliki penyakit jantung (dilambangkan dengan [1]) memiliki gula darah di bawah 120 mg/dl. Sedangkan pasien yang memiliki gula darah > 120 mg/dl cenderung tidak memiliki penyakit jantung.

![mu_fastingbs](https://user-images.githubusercontent.com/57740421/191168928-9800b32b-2a4f-4495-b906-7927acfd2f57.png)

- Pada fitur `RestingECG`, rerata pasien yang memiliki penyakit jantung (dilambangkan dengan [1]) memiliki tekanan darah yang normal.

![mu_ecg](https://user-images.githubusercontent.com/57740421/191168956-d08fea48-3308-44a6-b1c7-d621b00fff3b.png)

- Pada fitur `ExerciseAngina`, rerata pasien yang memiliki penyakit jantung (dilambangkan dengan [1]) memiliki angin.

![mu_angina](https://user-images.githubusercontent.com/57740421/191168979-8682656b-0464-4db0-9163-c8963687e48d.png)

- Pada fitur `ST_Slope`, rerata pasien yang memiliki penyakit jantung (dilambangkan dengan [1]) memiliki segmen ST yang bertipe flat.

![mu_slope](https://user-images.githubusercontent.com/57740421/191169012-fdfacc3e-d14e-4146-b3a5-e57a65b61c21.png)


#### *Univariate Analysis - Numerical Feature*
Melihat histogram masing-masing fitur _numerical_ yaitu `Age`, `RestingBP`, `Cholesterol`, `MaxHR`, dan `Oldpeak`

![ua_num](https://user-images.githubusercontent.com/57740421/191168159-71ab5b4c-7a70-4409-ace8-c34d49f3c35c.png)

#### *Multivariate Analysis - Numerical Feature*
Melakukan observasi korelasi antara fitur numerical dengan fitur target
![mu_num](https://user-images.githubusercontent.com/57740421/191170266-eeff64b2-4d29-4827-8ff0-ac0276d09f77.png)


## Data Preparation

_Data preparation_ yang digunakan di antaranya:

1. Seleksi Data: Menyeleksi data apakah data tersebut ada yang kosong atau tidak, jika ada data kosong maka akan dihapus. Pada data`heart_disease` tidak didapati data yang kosong. Hal ini dibuktikan dari pengecekan menggunakan `isnull().sum()`.
2. Menangani Outlier: Melakukan pengecekan apakah data `heart_disease` memiliki data outlier. Apabila terdapat data outlier, maka akan dihapus. Dalam menangani _outlier_, digunakan metode IQR. Ditemukan _outlier_ pada data `heart_disease`, hal ini ditemukan dengan melakukan visualisasi dengan `boxplot`. Dapat dilihat pada gambar, bahwa _outlier_ ditermukan pada `RestingBP`, `Cholesterol`, `MaxHR`, dan `Oldpeak`. Untuk mengatasi _outlier_ yang ada, maka digunakan metode IQR.

![outlier](https://user-images.githubusercontent.com/57740421/191170856-e838489d-4335-4b60-a739-0f2e6d0f95fb.png)

4. Melakukan Label Encoder: Melakukan proses encoding terhadap `categorical_feature`. Hal ini dilakukan karena fitur-fitur kategorikal perlu dirubah agar dapat digunakan pada tahap _modeling_.
5. Melakukan Splitting: membagi data menjadi _training_ dan _testing_ untuk _modeling_. Dalam melakukan _splitting_, digunakan rasio 80:20, yang berarti 80% data training, dan 20% data testing.
6. Standarisasi: membantu membuat fitur data menjadi bentuk yang lebih mudah diolah oleh algoritma. Dalam standarisasi, digunakan _module_ `StandarScaler` yang dapat ditemukan pada _library_ `sklearn`.


## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Proses ini dilakukan dengan menggunakan tiga algoritma, yakni KNN, RandomForest, dan AdaBoost. Hasil akhirnya adalah untuk mencari algoritma yang memiliki performa paling baik dari ketiga algoritma yang digunakan. Dapat dilihat dari _bar chart_ yang menunjukkan tiga model algoritma yang digunakan. Diketahui bahwa algoritma KNN merupakan algoritma yang memiliki error yang paling kecil dibanding model lainnya.

![eval](https://user-images.githubusercontent.com/57740421/191168197-ffee2389-6f90-4677-b7f1-84039afeedf2.png)

- Dalam membangun model KNN, digunakan module `RandomForestClassifier` dari _library_ `sklearn`. Digunakan parameter `n_neighbors = 10` untuk membangun model. Untuk melakukan _training_, maka digunakan `.fit(Xtrain, ytrain)` untuk _fitting_. Kemudian, untuk melakukan melakukan prediksi, digunakan `.predict(Xtrain)`.

- Dalam membangun model RandomForest, digunakan module `KNeighborsClassifier` dari _library_ `sklearn`. Digunakan parameter `max_features = 7` dan `max_depth = 3` untuk membangun model. Untuk melakukan _training_, maka digunakan `.fit(Xtrain, ytrain)` untuk _fitting_. Kemudian, untuk melakukan melakukan prediksi, digunakan `.predict(Xtrain)`.

- Dalam membangun model AdaBoost, digunakan module `AdaBoostClassifier` dari _library_ `sklearn`. Digunakan parameter `n_estimators = 3` dan `learning_rate = 0.2` untuk membangun model. Untuk melakukan _training_, maka digunakan `.fit(Xtrain, ytrain)` untuk _fitting_. Kemudian, untuk melakukan melakukan prediksi, digunakan `.predict(Xtrain)`.

## Evaluation
Evaluasi metrik yang digunakan untuk mengukur kinerja model adalah metrik mse (Mean Squared Error). Pemilihan matrik ini disebabkan karena kasus atau domain proyek yang dipilih adalah klasifikasi. Matrik MSE, pada dasarnya akan mengukur kuadrat rerata error dari prediksi yang dilakukan. MSE juga akan menghitung selisih kuadrat antara prediksi dan target, yang kemudian melakukan perhitungan rata-rata terhadap nilai-nilai tersebut.

Semakin tinggi nilai yang diperoleh MSE, semakin buruk juga modelnya. Nilai MSE tidak pernah negatif, tetapi akan menjadi NOL untuk model yang sempurna.

Rumus perhitungan matrik MSE: 
![alt](https://www.gstatic.com/education/formulas2/472522532/en/mean_squared_error.svg)

ket:

$\mathrm{MSE}$	=	mean squared error

${n}$	=	_number of data points_

$Y_{i}$	=	_observed values_ atau _ground truth_ dari nilai sebenarnya, dalam kasus ini nilai yang digunakan adalah nilai dari variabel `HeartDisease`

$\hat{Y}_{i}$	=	_predicted values_ atau _estimated target values_, dalam kasus ini nilai yang digunakan adalah nilai prediksi model terhadap variabel `HeartDisease`

Untuk melakukan evaluasi matrik, dapat menerapkan _code_ yang berada pada Evaluation Model yang tercantum pada _notebook_. Dalam melakukan evaluasi, nilai $\hat{Y}_{i}$ merupakan nilai prediksi yang keluar dari variabel-variabel yang ada dalam `Xtrain`, seperti `Age`, `Sex`, `ChestPainType`, `RestingBP`, `Cholesterol`, `FastingBS`, `RestingECG`, `MaxHR`, `ExerciseAngina`, `Oldpeak`, dan `ST_Slope`. Variabel-variabel pada tabel di bawah kemudian digunakan untuk melakukan prediksi, yang mana akan mengeluarkan nilai 0 atau 1, dan akan tersimpan pada variabel _predicted value_ .

|   |       Age |       Sex | ChestPainType | RestingBP | Cholesterol | FastingBS | RestingECG |     MaxHR | ExerciseAngina |   Oldpeak |  ST_Slope |
|--:|----------:|----------:|--------------:|----------:|------------:|----------:|-----------:|----------:|---------------:|----------:|----------:|
| 0 |  0.052026 |  0.516309 |      1.276887 |  0.970493 |   -0.036784 | -0.551733 |   0.017264 | -0.581047 |      -0.824310 | -0.831502 |  1.051095 |
| 1 |  0.052026 | -1.936826 |      0.230501 |  0.414627 |    1.007298 | -0.551733 |   1.600366 |  0.126132 |      -0.824310 | -0.831502 |  1.051095 |
| 2 |  0.158042 |  0.516309 |     -0.815884 | -0.030066 |    1.410278 | -0.551733 |   0.017264 | -0.188170 |       1.213136 |  0.293802 | -0.596519 |
| 3 | -1.114157 | -1.936826 |      1.276887 |  0.970493 |    0.503574 | -0.551733 |   0.017264 |  1.501203 |      -0.824310 | -0.831502 |  1.051095 |
| 4 | -0.372041 |  0.516309 |     -0.815884 |  0.414627 |    0.292926 | -0.551733 |   1.600366 |  0.126132 |       1.213136 |  3.857266 | -0.596519 |

Sedangkan, nilai $Y_{i}$ merupakan nilai sebenarnya dari variabel `HeartDisease`, yakni 0 dan 1. Kemudian, MSE akan melakukan perhitungan yang melibatkan hasil dari _predicted value_ dan _ground truth_, yang keduanya sama-sama memiliki nilai 0 dan 1.

Hasil dari _modeling_ dapat dilihat pada tabel di bawah ini. Tabel memberikan informasi detail terkait hasil _training_ dan _testing_

|		| train	    |	test      |
|---------------|-----------|-------------|
|KNN		| 0.000128  |	0.000141  |
|AdaBoost	| 0.000183  |	0.000201  |
|RandomForest	| 0.00012   |	0.000158  |

Pada tabel di bawah disajikan informasi hasil prediksi dari model yang digunakan. Dari tabel yang disajikan dapat dilihat bahwa prediksi menggunakan KNN pada baris 199, memiliki hasil paling sesuai dengan data aslinya, dibandingkan kedua model lainnya. Hasil prediksi yang diberikan oleh model KNN adalah benar, dibandingkan dengan prediksi AdaBoost dan RandomForest. Maka dapat diketahui bahwa model KNN memberikan nilai error yang paling kecil. Sehingga, model KNN lah yang dipilih sebagai model terbaik untuk melakukan klasifikasi penyakit jantung.

|     | y_true | prediksi_KNN | prediksi_AdaBoost | prediksi_RandomForest |
|-----|--------|--------------|-------------------|-----------------------|
| 199 | 0      | 0            | 1                 | 1                     |
| 44  | 1      | 1            | 1                 | 1                     |
| 103 | 1      | 1            | 1                 | 1                     |
| 852 | 1      | 1            | 1                 | 1                     |

Referensi:

[1] [Heseltine, E., Carp-Courtman, C., & McGregor, C. (2025). Machine learning to predict stroke risk from routine hospital data: A systematic review. International Journal of Medical Informatics, 105811. https://doi.org/10.1016/j.ijmedinf.2025.105811](https://www.sciencedirect.com/science/article/pii/S1386505625000280)

[2] [Heart Failure UCI Dataset](http://archive.ics.uci.edu/ml/datasets/Heart+Disease)

