
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
Untuk memahami data _Stroke Prediction_ dilakukan visualisasi menggunakan _bar chart_ dan _pie chart_. Dalam memvisualisasikannya, dilakukan dengan _Univariate Analysis_ dan _Multivariate Analysis_. Untuk keseluruhannya, dataset dibagi menjadi dua fitur, yakni fitur _categorical_ dan fitur _numerical_.

#### *Univariate Analysis - Categorical Feature*

1. _Univariate Analysis_ terhadap Stroke
![ua_Stroke](https://github.com/Indradi-R/Stroke-Predictive-Analysis/blob/main/img/stroke%20distribution.png)	

Dari _plot_ yang dibuat, dapat diketahui bahwa data lebih banyak menunjukkan kondisi _Stroke_(95.1%) dibanding kondisi normal (4.9%).

2. _Univariate Analysis_ terhadap Jenis Kelamin
![ua_Gender](https://github.com/Indradi-R/Stroke-Predictive-Analysis/blob/main/img/gender%20distri.png)	

Dari _pie plot_ yang dibuat, ditunjukkan bahwa pada dataset memiliki jumlah Wanita yang lebih banyak dan persentase Pria yang mengalami stroke lebih tinggi.

#### *Multivariate Analysis - Categorical Feature*

- Pada fitur `gender`, rerata _Stroke_ menyerang seseorang berjenis kelamin wanita, dibanding pria. Hal ini dapat dilihat pada bar chart [1] yang melambangkan pasien memiliki penyakit stroke dan tidak memiliki penyakit stroke, dilambangkan dengan [0].

![mu_gender](https://github.com/Indradi-R/Stroke-Predictive-Analysis/blob/main/img/avg%20stroke%20gender.png)

- Pada fitur `hypertension`, rerata pasien yang memiliki penyakit stroke ditambah dengan hypertesnion (dilambangkan dengan [1] dan warna oranye) sebanyak 66 kasus.

![mu_hypertension](https://github.com/Indradi-R/Stroke-Predictive-Analysis/blob/main/img/avg%20stroke%20hypertension.png)

- Pada fitur `heart_disease`, rerata pasien yang memiliki penyakit stroke ditambah dengan penyakit jantung (dilambangkan dengan [1] dan warna oranye) sebanyak 47 kasus.

![mu_heart_disease](https://github.com/Indradi-R/Stroke-Predictive-Analysis/blob/main/img/avg%20stroke%20heart%20disease.png)

- Pada fitur `work_type`, rerata pasien yang memiliki penyakit stroke (dilambangkan dengan [1]) didominasi private worker sebanyak 149 kasus.

![mu_wt](https://github.com/Indradi-R/Stroke-Predictive-Analysis/blob/main/img/avg%20stroke%20work%20type.png)

- Pada fitur `smoking_status`, rerata pasien yang memiliki penyakit stroke (dilambangkan dengan [1]) didominasi oleh yang bukan perokok (90 kasus) diikuti oleh mantan perokok (70 kasus).

![mu_smoking](https://github.com/Indradi-R/Stroke-Predictive-Analysis/blob/main/img/avg%20stroke%20smoking%20status.png)

#### *Univariate Analysis - Numerical Feature*
Melihat histogram masing-masing fitur _numerical_ yaitu `Age`, `Hypertension`, `Heart Disease`, `Glucose Level`, `BMI` dan `Stroke`

![ua_num](https://user-images.githubusercontent.com/57740421/191168159-71ab5b4c-7a70-4409-ace8-c34d49f3c35c.png)

#### *Multivariate Analysis - Numerical Feature*
Melakukan observasi korelasi antara fitur numerical dengan fitur target
![mu_num](https://github.com/Indradi-R/Stroke-Predictive-Analysis/blob/main/img/numerical%20hist%20analysis.png)

![mu_corr](https://github.com/Indradi-R/Stroke-Predictive-Analysis/blob/main/img/corr%20matrix%20numerical.png)


## Data Preparation

_Data preparation_ yang digunakan di antaranya:

1. Seleksi Data: Menyeleksi data apakah data tersebut ada yang kosong atau tidak, jika ada data kosong maka akan dihapus. Pada data `Stroke` yang mana terdapat 201 data kosong pada numerical feature yaitu _bmi_
2. Melakukan _feature engineering_, seperti menghapus kolom `id`
3. Melakukan _encoding_, pada feature seperti `gender`, `smoking_status`, `work_type`, `residence_type`, dan `ever_married`
4. Melakukan Splitting: membagi data menjadi _training_ dan _testing_ untuk _modeling_. Dalam melakukan _splitting_, digunakan rasio 80:20, yang berarti 80% data training, dan 20% data testing.
5. Standarisasi: membantu membuat fitur data menjadi bentuk yang lebih mudah diolah oleh algoritma. Dalam standarisasi, digunakan _module_ `StandarScaler` yang dapat ditemukan pada _library_ `sklearn`.


## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Proses ini dilakukan dengan menggunakan tiga algoritma, yakni Decision Tree, Logistic Regression, dan Support Vector Machine (SVM). Hasil akhirnya adalah untuk mencari algoritma yang memiliki performa paling baik dari ketiga algoritma yang digunakan. Dapat dilihat dari _bar chart_ yang menunjukkan tiga model algoritma yang digunakan. Diketahui bahwa algoritma KNN merupakan algoritma yang memiliki error yang paling kecil dibanding model lainnya.

![eval](https://github.com/Indradi-R/Stroke-Predictive-Analysis/blob/main/img/plotting%20mse%20result.png)

- Dalam membangun model Decision Tree, digunakan module `DecisionTreeClassifier` dari _library_ `sklearn`. Untuk melakukan _training_, maka digunakan `.fit(X_train, Y_train)` untuk _fitting_.
  Dalam membangun model Logistic Regression, digunakan module `LogisticRegression` dari _library_ `sklearn`. Untuk melakukan _training_, maka digunakan `.fit(X_train, Y_train)` untuk _fitting_.
  Dalam membangun model Support Vector Machine, digunakan module `SVC` dari _library_ `sklearn`. Untuk melakukan _training_, maka digunakan `.fit(X_train, Y_train)` untuk _fitting_.

## Evaluation
Metrik evaluasi yang digunakan untuk menilai kinerja model adalah Mean Squared Error (MSE). Pemilihan metrik ini didasarkan pada sifat proyek yang berfokus pada klasifikasi. MSE berfungsi untuk menghitung rata-rata kuadrat selisih antara nilai prediksi dan nilai target. Dengan cara ini, metrik ini mengukur sejauh mana prediksi berbeda dari hasil sebenarnya. Semakin tinggi nilai MSE, semakin buruk performa model. Sebaliknya, nilai MSE yang lebih rendah menunjukkan kinerja model yang lebih baik, dengan nilai MSE yang sempurna adalah nol.

Hasil dari _modeling_ dapat dilihat pada tabel di bawah ini. Tabel memberikan informasi detail terkait hasil _training_ dan _testing_

|		| train	    |	test      |
|---------------|-----------|-------------|
|DecisionTree		| 0.0  |	0.000101  |
|LogisticRegression	| 0.000046  |	0.000062  |
|SVM	| 0.000045   |	0.000061  |


Pada tabel di bawah disajikan informasi hasil prediksi dari model yang digunakan. Dari tabel yang disajikan dapat dilihat bahwa prediksi data random yang berasal dari dataset yaitu baris 4616, 543, dan 2083.

|     | y_true | prediksi_KNN | prediksi_AdaBoost | prediksi_RandomForest |
|-----|--------|--------------|-------------------|-----------------------|
| 4616 | 0      | 0            | 0                 | 0                     |
| 543  | 0      | 0            | 0                 | 0                     |
| 2083 | 0      | 0            | 0                 | 0                     |


Referensi:

[1] [Heseltine, E., Carp-Courtman, C., & McGregor, C. (2025). Machine learning to predict stroke risk from routine hospital data: A systematic review. International Journal of Medical Informatics, 105811. https://doi.org/10.1016/j.ijmedinf.2025.105811](https://www.sciencedirect.com/science/article/pii/S1386505625000280)

[2] [Kaggle Stroke Prediction Dataset](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset)

