
# Laporan Proyek Machine Learning Terapan - Indradi Rahmatullah
## Predictive Analysis

## Domain Proyek
Menurut Organisasi Kesehatan Dunia (WHO), stroke merupakan penyebab kematian terbanyak ke-2 di dunia, yang menyebabkan sekitar 11% dari total kematian.

Proyek ini berfokus pada analisis data kesehatan untuk memprediksi risiko stroke pada individu berdasarkan faktor-faktor risiko yang relevan, seperti usia, riwayat medis, gaya hidup, dan kondisi kesehatan lainnya. Dengan menggunakan teknik pembelajaran mesin, proyek ini bertujuan untuk membantu penyedia layanan kesehatan mengidentifikasi individu dengan risiko tinggi sehingga tindakan pencegahan dapat dilakukan lebih dini. 

Oleh karena itu, diperlukan model prediksi risiko stroke yang lebih akurat. Pembelajaran mesin (ML) dapat memberikan solusi untuk hal ini dengan memanfaatkan basis data yang ada untuk membangun model prediksi risiko stroke yang akurat dan mengidentifikasi faktor risiko baru untuk stroke [1](https://www.sciencedirect.com/science/article/pii/S1386505625000280).

## Business Understanding

### Problem Statements
1. Bagaimana cara mengembangkan model prediksi untuk menentukan apakah seorang pasien berisiko mengalami stroke berdasarkan riwayat kesehatannya?
2. Faktor-faktor apa saja yang paling berpengaruh terhadap kemungkinan terjadinya stroke berdasarkan data kesehatan pasien?

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
Dataset yang digunakan pada proyek _machine learning_ merupakan **5110 data observasi** yang didapat dari situs [kaggle](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset). Terdapat 12 fitur yang dapat digunakan untuk memprediksi kemungkinan Stroke.

**Variabel-variabel pada Stroke Prediction Dataset adalah sebagai berikut:**
1) id: Identifikasi unik untuk setiap pasien.
2) gender: Jenis kelamin pasien, terdiri dari "Male" (Laki-laki), "Female" (Perempuan), atau "Other" (Lainnya).
3) age: Usia pasien dalam tahun.
4) hypertension: Indikator hipertensi, 0 jika tidak memiliki hipertensi, 1 jika memiliki hipertensi.
5) heart_disease: Indikator penyakit jantung, 0 jika tidak memiliki penyakit jantung, 1 jika memiliki penyakit jantung.
6) ever_married: Status pernikahan pasien, "No" (Belum menikah) atau "Yes" (Sudah menikah).
7) work_type: Jenis pekerjaan pasien, terdiri dari:
"children" (Anak-anak)
"Govt_job" (Pekerjaan pemerintah)
"Never_worked" (Belum pernah bekerja)
"Private" (Pekerjaan di sektor swasta)
"Self-employed" (Wirausaha)
8) Residence_type: Jenis tempat tinggal pasien, terdiri dari "Rural" (Pedesaaan) atau "Urban" (Perkotaan).
9) avg_glucose_level: Rata-rata kadar glukosa dalam darah pasien.
10) bmi: Indeks Massa Tubuh (Body Mass Index/BMI) pasien.
11) smoking_status: Status merokok pasien, terdiri dari:
"formerly smoked" (Dulu merokok)
"never smoked" (Tidak pernah merokok)
"smokes" (Saat ini merokok)
"Unknown" (Tidak diketahui)
12) stroke: Indikator apakah pasien pernah mengalami stroke, 1 jika pernah mengalami stroke, 0 jika tidak.

### Kondisi Dataset

1. Missing Value
Terdapat 201 data yang hilang (missing values) pada fitur bmi.
Perlu dilakukan penanganan nilai yang hilang, seperti pengisian menggunakan rata-rata (mean), median, atau metode lain yang sesuai.
2. Outlier
![outlier before handling](https://github.com/user-attachments/assets/6b3dcbac-76f3-4276-b19d-15d85d13f299)
Berdasarkan visualisasi data, terdapat outlier pada fitur avg_glucose_level dan bmi.
Outlier pada avg_glucose_level terlihat pada nilai yang jauh di atas rata-rata, menunjukkan adanya data ekstrem.
Outlier pada bmi juga menunjukkan adanya nilai-nilai yang menyimpang dari distribusi normal.

### Explanatory Data Analysis
Untuk memahami data _Stroke Prediction_ dilakukan visualisasi menggunakan _bar chart_ dan _pie chart_. Dalam memvisualisasikannya, dilakukan dengan _Univariate Analysis_ dan _Multivariate Analysis_. Untuk keseluruhannya, dataset dibagi menjadi dua fitur, yakni fitur _categorical_ dan fitur _numerical_.

#### *Univariate Analysis - Categorical Feature*

1. _Univariate Analysis_ terhadap Stroke
![stroke distribution](https://github.com/user-attachments/assets/688ccd56-f754-4387-bf1c-b001205af94f)

Dari _plot_ yang dibuat, dapat diketahui bahwa data lebih banyak menunjukkan kondisi _Stroke_(95.1%) dibanding kondisi normal (4.9%).

2. _Univariate Analysis_ terhadap Jenis Kelamin
![gender distri](https://github.com/user-attachments/assets/969dacc3-f904-420f-b68a-23523ae94177)

Dari _pie plot_ yang dibuat, ditunjukkan bahwa pada dataset memiliki jumlah Wanita yang lebih banyak dan persentase Pria yang mengalami stroke lebih tinggi.

#### *Multivariate Analysis - Categorical Feature*

- Pada fitur `gender`, rerata _Stroke_ menyerang seseorang berjenis kelamin wanita, dibanding pria. Hal ini dapat dilihat pada bar chart [1] yang melambangkan pasien memiliki penyakit stroke dan tidak memiliki penyakit stroke, dilambangkan dengan [0].

![avg stroke gender](https://github.com/user-attachments/assets/1c00fa97-a6f9-4984-87f4-a55a6fc383cb)

- Pada fitur `hypertension`, rerata pasien yang memiliki penyakit stroke ditambah dengan hypertesnion (dilambangkan dengan [1] dan warna oranye) sebanyak 66 kasus.

![avg stroke hypertension](https://github.com/user-attachments/assets/2662e19a-e0ff-4f67-b1d0-7266f864c3a1)

- Pada fitur `heart_disease`, rerata pasien yang memiliki penyakit stroke ditambah dengan penyakit jantung (dilambangkan dengan [1] dan warna oranye) sebanyak 47 kasus.

![avg stroke heart disease](https://github.com/user-attachments/assets/07fb3542-0071-4712-bc4a-6ac106c36a66)

- Pada fitur `work_type`, rerata pasien yang memiliki penyakit stroke (dilambangkan dengan [1]) didominasi private worker sebanyak 149 kasus.

![avg stroke work type](https://github.com/user-attachments/assets/7bac763c-9c99-4396-be1e-ef91dfc0d23b)

- Pada fitur `smoking_status`, rerata pasien yang memiliki penyakit stroke (dilambangkan dengan [1]) didominasi oleh yang bukan perokok (90 kasus) diikuti oleh mantan perokok (70 kasus).

![avg stroke smoking status](https://github.com/user-attachments/assets/7dee3807-2f31-43c5-abf4-27a1779f77ab)

#### *Univariate Analysis - Numerical Feature*
Melihat histogram masing-masing fitur _numerical_ yaitu `Age`, `Hypertension`, `Heart Disease`, `Glucose Level`, `BMI` dan `Stroke`

![numerical hist](https://github.com/user-attachments/assets/6cbef9db-f4fb-49ea-b01d-2d85f118ed9f)

#### *Multivariate Analysis - Numerical Feature*
Melakukan observasi korelasi antara fitur numerical dengan fitur target
![numerical hist analysis](https://github.com/user-attachments/assets/b0429296-1852-4e99-a2a4-37ff504c4d8a)

![corr matrix numerical](https://github.com/user-attachments/assets/b2ff51b0-b046-4f0b-a638-16c95a68f26d)

## Data Preparation

## 1. Mendeteksi dan Menangani Nilai Kosong
Pada dataset ini, terdapat **201 nilai kosong** pada fitur numerik **bmi**. Untuk menangani nilai kosong tersebut, dilakukan pengisian menggunakan **nilai rata-rata (_mean_)** dari fitur **bmi**.

## 2. Menangani Outlier
Outlier terdeteksi pada fitur **avg_glucose_level** dan **bmi** berdasarkan visualisasi boxplot. Outlier ditangani menggunakan metode **Interquartile Range (IQR)**, dengan menghapus data yang berada di luar batas bawah dan batas atas.

**Rumus IQR untuk Menghapus Outlier:**
IQR = Q3 - Q1  
Lower Bound = Q1 - 1.5 × IQR  
Upper Bound = Q3 + 1.5 × IQR 

## 3. Feature Engineering
Menghapus kolom **id**, karena tidak memiliki pengaruh terhadap prediksi stroke.

## 4. Encoding
Mengubah fitur kategorikal menjadi numerik menggunakan **Label Encoding** pada fitur berikut:

- Gender
- Smoking Status
- Work Type
- Residence Type
- Ever Married

## 5. Splitting Data
Membagi dataset menjadi **data training (80%)** dan **data testing (20%)** menggunakan metode **train-test split**.

## 6. Standarisasi Data
Standarisasi dilakukan untuk memastikan setiap fitur memiliki skala yang sama, terutama untuk algoritma seperti **SVM** dan **Logistic Regression**.

**Rumus Standarisasi:**
x' = (x - μ) / σ  

dengan:  
- x' = nilai setelah standarisasi  
- x = nilai asli  
- μ = rata-rata fitur  
- σ = standar deviasi fitur 



## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Proses ini dilakukan dengan menggunakan tiga algoritma, yakni Decision Tree, Logistic Regression, dan Support Vector Machine (SVM). Hasil akhirnya adalah untuk mencari algoritma yang memiliki performa paling baik dari ketiga algoritma yang digunakan. Dapat dilihat dari _bar chart_ yang menunjukkan tiga model algoritma yang digunakan. Diketahui bahwa algoritma KNN merupakan algoritma yang memiliki error yang paling kecil dibanding model lainnya.

![plotting mse result](https://github.com/user-attachments/assets/d5e3b8b1-158b-44be-8dd0-de2a86f647a1)

### 1. Decision Tree
#### Cara Kerja
Decision Tree bekerja dengan membagi dataset menjadi cabang-cabang berdasarkan fitur tertentu yang menghasilkan keputusan terbaik. Algoritma ini membangun model berbentuk pohon di mana setiap node internal mewakili suatu fitur dalam dataset, setiap cabang mewakili keputusan, dan setiap leaf node mewakili hasil akhir.

#### Parameter
- Menggunakan parameter default dari `DecisionTreeClassifier()`.
- Model ini dapat menggunakan parameter seperti:
  - `criterion`: Fungsi untuk mengukur kualitas pemisahan (default: `gini`).
  - `max_depth`: Kedalaman maksimum pohon.
  - `min_samples_split`: Jumlah minimum sampel yang dibutuhkan untuk membagi node.

### 2. Logistic Regression
#### Cara Kerja
Logistic Regression adalah metode klasifikasi berbasis probabilitas yang menggunakan fungsi sigmoid untuk memprediksi probabilitas suatu kelas. Model ini menghitung hubungan linier antara fitur dan kelas target, kemudian mengaplikasikan fungsi logistik untuk mendapatkan probabilitas keluaran.

#### Parameter
- Menggunakan parameter default dari `LogisticRegression()`.
- Parameter yang dapat digunakan:
  - `penalty`: Jenis regulasi yang diterapkan (default: `l2`).
  - `solver`: Algoritma optimasi yang digunakan (default: `lbfgs`).
  - `C`: Parameter regulasi untuk mengontrol kompleksitas model.

### 3. Support Vector Machine (SVM)
#### Cara Kerja
SVM bekerja dengan mencari hyperplane terbaik yang memisahkan kelas dalam data. Model ini menggunakan kernel trick untuk menangani data yang tidak dapat dipisahkan secara linear dengan mengubahnya ke dimensi yang lebih tinggi.

#### Parameter
- Menggunakan parameter default dari `SVC()`.
- Parameter yang dapat digunakan:
  - `kernel`: Fungsi kernel yang digunakan (default: `rbf`).
  - `C`: Parameter regulasi untuk mengontrol margin pemisahan.
  - `gamma`: Parameter kernel untuk mengontrol kompleksitas model.

## Evaluation

### 1. Metrik Evaluasi
Metrik evaluasi yang digunakan untuk menilai kinerja model adalah **Mean Squared Error (MSE)**. MSE menghitung rata-rata kuadrat selisih antara nilai prediksi dan nilai target, mengukur sejauh mana prediksi berbeda dari hasil sebenarnya. 

- **Semakin tinggi nilai MSE, semakin buruk performa model.**
- **Semakin rendah nilai MSE, semakin baik performa model, dengan nilai MSE sempurna adalah nol.**

#### Hasil Evaluasi
| Model | Train MSE | Test MSE |
|---------------|-----------|-------------|
| Decision Tree | 0.0       | 0.000101    |
| Logistic Regression | 0.000046  | 0.000062  |
| SVM           | 0.000045  | 0.000061  |

### 2. Dampak Evaluasi terhadap Bisnis
Evaluasi model sangat penting untuk memastikan bahwa model yang digunakan dapat memberikan prediksi yang akurat dalam mendukung pengambilan keputusan bisnis. Dalam konteks prediksi stroke:

- **Model dengan MSE rendah** menunjukkan bahwa prediksi memiliki tingkat akurasi yang baik, membantu dalam mendeteksi risiko stroke lebih awal.
- **Jika MSE terlalu tinggi**, maka keputusan yang diambil bisa tidak akurat, yang dapat berakibat pada rekomendasi medis yang salah.
- **Dengan model yang optimal**, tenaga medis dapat lebih cepat mengidentifikasi pasien berisiko tinggi dan mengambil langkah pencegahan yang tepat.

#### Contoh Hasil Prediksi
Dari dataset, berikut hasil prediksi untuk beberapa sampel data:

| Index | y_true | Prediksi Decision Tree | Prediksi Logistic Regression | Prediksi SVM |
|-------|--------|-----------------------|-----------------------------|-------------|
| 1173  | 0      | 0                     | 0                           | 0           |
| 1775  | 0      | 0                     | 0                           | 0           |
| 4169  | 0      | 0                     | 0                           | 0           |

Dari hasil evaluasi yang dilakukan, dapat disimpulkan bahwa:

- Semua model memberikan prediksi yang sama untuk sampel ini.
- **Decision Tree Classifier** memiliki MSE yang lebih tinggi pada data uji dibandingkan dengan Logistic Regression dan SVM, menunjukkan bahwa Decision Tree mungkin overfitting terhadap data latih.
- **Logistic Regression** dan **SVM** memiliki MSE yang lebih rendah pada data uji, menunjukkan bahwa kedua model ini memiliki generalisasi yang lebih baik dibandingkan dengan Decision Tree.

Dengan demikian, Logistic Regression dan SVM dapat dianggap sebagai model yang lebih andal untuk prediksi stroke berdasarkan dataset yang digunakan. Evaluasi lebih lanjut diperlukan untuk memastikan model dapat diimplementasikan secara efektif dalam lingkungan nyata dan memberikan manfaat yang signifikan dalam mendeteksi risiko stroke pada pasien.

Referensi:

[1] [Heseltine, E., Carp-Courtman, C., & McGregor, C. (2025). Machine learning to predict stroke risk from routine hospital data: A systematic review. International Journal of Medical Informatics, 105811. https://doi.org/10.1016/j.ijmedinf.2025.105811](https://www.sciencedirect.com/science/article/pii/S1386505625000280)

[2] [Kaggle Stroke Prediction Dataset](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset)

