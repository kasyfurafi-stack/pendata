# UTS


## Analisa Data Kesuburan Tanah 

### 1. Lakukan analisis data dengan menggunakan 

- **K-Nearest Neighbors (KNN)** 
  

### 2. Lakukan Pemrosesan Data tersebut



### 3. Hitung Metrik Evaluasi

| Metrik | Keterangan |
|---|---|
| **Accuracy** | Persentase prediksi benar dari total data |
| **Precision** | Ketepatan prediksi kelas positif |
| **Recall** | Kemampuan mendeteksi seluruh kelas positif |
| **F1-Score** | Harmonic mean antara Precision dan Recall |
| 

---





# Dataset Klasifikasi Kesuburan Tanah

## Deskripsi Umum

 Dataset berisi **2.000 sampel** data tanah dengan **10 fitur agronomis** dan **1 kolom label** yang membagi kondisi tanah menjadi dua kelas: **Subur** dan **Tidak Subur**. Data mengandung missing values (data hilang)
[Unduh data Kesuburan Tanah](https://docs.google.com/spreadsheets/d/1_VTOGjavAI1Axd4gFRhXrIKRVVjY9zvM/edit?usp=sharing&ouid=108447658857677622027&rtpof=true&sd=true)

---

## Informasi `Dataset`

| Atribut | Keterangan |
|---|---|
| Jumlah Sampel | 2.000 baris |
| Jumlah Fitur | 10 fitur (9 numerik, 1 kategorikal) |
| Jumlah Kelas | 2 kelas |
| Target / Label | `Subur` / `Tidak Subur` |
|                |                                     |
|                |                                     |

---

## Penjelasan Fitur

### 1. `pH Tanah`
- **Satuan:** Skala pH (0–14)
- **Deskripsi:** Tingkat keasaman atau kebasaan tanah. pH optimal untuk pertanian berkisar 6,0–7,5.
- **Nilai Subur:** 6,0 – 7,5
- **Nilai Tidak Subur:** 3,5 – 5,4 (asam kuat) atau 7,6 – 9,0 (basa kuat)

### 2. `N Total (%)`
- **Satuan:** Persen (%)
- **Deskripsi:** Kandungan nitrogen total dalam tanah. Nitrogen sangat penting untuk pertumbuhan vegetatif tanaman.
- **Nilai Subur:** 0,21 – 0,50%
- **Nilai Tidak Subur:** 0,01 – 0,20%

### 3. `P Tersedia (ppm)`
- **Satuan:** Parts per million (ppm)
- **Deskripsi:** Fosfor tersedia yang dapat diserap tanaman. Fosfor berperan dalam pembentukan akar dan buah.
- **Nilai Subur:** 15 – 60 ppm
- **Nilai Tidak Subur:** 1 – 14 ppm

### 4. `K Tersedia (meq/100g)`
- **Satuan:** Milliequivalent per 100 gram tanah
- **Deskripsi:** Kalium tersedia dalam tanah. Penting untuk ketahanan tanaman dan proses fotosintesis.
- **Nilai Subur:** 0,30 – 0,80 meq/100g
- **Nilai Tidak Subur:** 0,05 – 0,29 meq/100g

### 5. `C Organik (%)`
- **Satuan:** Persen (%)
- **Deskripsi:** Kandungan karbon organik tanah, indikator utama kesuburan dan kesehatan biologi tanah.
- **Nilai Subur:** 2,0 – 5,0%
- **Nilai Tidak Subur:** 0,2 – 1,9%

### 6. `KTK (meq/100g)`
- **Satuan:** Milliequivalent per 100 gram tanah
- **Deskripsi:** Kapasitas Tukar Kation — kemampuan tanah mengikat dan menyediakan unsur hara bagi tanaman. Semakin tinggi semakin subur.
- **Nilai Subur:** 20 – 45 meq/100g
- **Nilai Tidak Subur:** 5 – 19 meq/100g

### 7. `Kejenuhan Basa (%)`
- **Satuan:** Persen (%)
- **Deskripsi:** Persentase kation basa (Ca, Mg, K, Na) dari total KTK. Menggambarkan kualitas kesuburan kimia tanah.
- **Nilai Subur:** 60 – 100%
- **Nilai Tidak Subur:** 10 – 59%

### 8. `Tekstur Tanah`
- **Tipe:** Kategorikal
- **Deskripsi:** Komposisi partikel tanah yang memengaruhi drainase, aerasi, dan kemampuan menahan air.

| Kelas | Tekstur yang Umum |
|---|---|
| **Subur** | Lempung, Lempung Berpasir, Lempung Berliat |
| **Tidak Subur** | Pasir, Liat, Debu |

### 9. `Kadar Air (%)`
- **Satuan:** Persen (%)
- **Deskripsi:** Persentase kadar air dalam tanah. Terlalu kering atau terlalu basah sama-sama merugikan pertumbuhan tanaman.
- **Nilai Subur:** 25 – 45%
- **Nilai Tidak Subur:** 5 – 20% (terlalu kering) atau 55 – 75% (terlalu basah)

### 10. `Bulk Density (g/cm³)`
- **Satuan:** Gram per sentimeter kubik
- **Deskripsi:** Kerapatan tanah. Nilai tinggi menandakan tanah padat, aerasi buruk, dan sulit ditembus akar.
- **Nilai Subur:** 0,9 – 1,2 g/cm³
- **Nilai Tidak Subur:** 1,4 – 1,9 g/cm³

---

## Definisi Kelas

| Label | Deskripsi |
|---|---|
| **Subur** | Tanah dengan kondisi fisik, kimia, dan biologi yang optimal untuk pertumbuhan tanaman. Ditandai dengan pH seimbang, unsur hara cukup, tekstur ideal, dan struktur tanah yang baik. |
| **Tidak Subur** | Tanah yang memiliki satu atau lebih kondisi pembatas seperti pH ekstrem, kekurangan unsur hara, tekstur buruk, kadar air tidak ideal, atau kerapatan tanah tinggi. |

---

## Distribusi Kelas

```
Subur        : 1.000 sampel (50%)
Tidak Subur  : 1.000 sampel (50%)
Total        : 2.000 sampel
```

---

## penjelasan dari soal diatas

## Melakukan analisis data menggunakan K-Nearest Neighbors (KNN)

Berikut adalah urutan kerja (workflow)  untuk menyelesaikan tugas Analisis Kesuburan Tanah :

- Tahap 1 & 2: Menjawab tuntutan "Lakukan Pemrosesan Data" (menggunakan node CSV Reader, Column Filter, Missing Value, Category to Number, Normalizer).

- Tahap 3: Menjawab tuntutan "Lakukan analisis data dengan KNN" (menggunakan node Partitioning dan K Nearest Neighbor).

- Tahap 4: Menjawab tuntutan "Hitung Metrik Evaluasi" (menggunakan node Scorer).

### Tahap 1: Memasukkan dan Membersihkan Data
1. CSV Reader

- Fungsi: Untuk membaca file data Anda.

- Cara setting: Klik kanan -> Configure. Browse dan pilih file dataset_kesuburan_tanah_missing.xlsx - Dataset.csv. Pastikan datanya terbaca rapi di kotak preview bawah, lalu klik OK.

Klik kanan -> Execute.

2. Column Filter

Fungsi: Untuk membuang kolom ID karena tidak ada hubungannya dengan kesuburan tanah dan akan merusak perhitungan jarak KNN.

Cara setting: Hubungkan dari CSV Reader. Klik kanan -> Configure. Pindahkan kolom ID ke kotak kiri (Exclude), sisanya biarkan di kotak kanan (Include).

Klik kanan -> Execute.

3. Missing Value

Fungsi: Untuk mengisi data yang kosong (berisi tanda ? merah di KNIME).

Cara setting: Hubungkan dari Column Filter. Klik kanan -> Configure.

Di tab Default, atur kolom Number (double/integer) menjadi Median.

Atur kolom String menjadi Most Frequent Value (untuk mengisi kolom Tekstur Tanah yang kosong dengan nilai modus).

Klik kanan -> Execute.

### Tahap 2: Transformasi Data (Preprocessing)
4. Category To Number

Fungsi: KNN adalah algoritma matematika yang menghitung jarak, jadi teks seperti "Lempung" atau "Pasir" di kolom Tekstur Tanah harus diubah jadi angka.

Cara setting: Hubungkan dari Missing Value. Klik kanan -> Configure. Masukkan kolom Tekstur Tanah ke kotak Include. (Catatan: Jangan masukkan kolom Label Subur/Tidak Subur ke sini, biarkan Label tetap berbentuk teks).

Klik kanan -> Execute.

5. Normalizer

Fungsi: Menyamakan skala angka (seperti yang kita bahas di Min-Max / Z-Score).

Cara setting: Hubungkan dari Category To Number. Klik kanan -> Configure. Pilih semua fitur numerik. Di bagian bawah, pilih Z-Score Normalization (Standardization) atau Min-Max Normalization (0 to 1). Keduanya bagus untuk KNN.

Klik kanan -> Execute.

### Tahap 3: Pemodelan (Machine Learning)
6. Partitioning

Fungsi: Membagi data menjadi 80% Data Latih (Train) dan 20% Data Uji (Test).

Cara setting: Hubungkan dari Normalizer. Klik kanan -> Configure.

Di opsi Relative [%], isi 80.

Centang kotak Stratified sampling, lalu pilih kolom Label. Ini memastikan porsi Subur dan Tidak Subur dibagi sama rata di data latih dan uji.

Klik kanan -> Execute. (Node ini punya dua titik output di kanan: atas untuk Train, bawah untuk Test).

7. K Nearest Neighbor

Fungsi: Ini adalah algoritma prediksinya.

Cara menghubungkan: Tarik garis dari output atas Partitioning (data latih) ke input atas node KNN. Lalu tarik garis dari output bawah Partitioning (data uji) ke input bawah node KNN.

Cara setting: Klik kanan -> Configure.

Number of neighbors (k): Isi 5 (atau angka ganjil lain seperti 3 atau 7).

Class column: Pilih Label (karena ini yang mau kita tebak).

Klik kanan -> Execute.

### Tahap 4: Evaluasi Hasil (Hitung Metrik)
8. Scorer

Fungsi: Untuk memunculkan nilai Accuracy, Precision, Recall, dan F1-Score sesuai permintaan tugas Anda.

Cara setting: Hubungkan dari K Nearest Neighbor. Klik kanan -> Configure.

First column: Pilih Label (ini kunci jawaban aslinya).

Second column: Pilih Prediction (Label) (ini tebakan dari model KNN).

Klik kanan -> Execute.

Cara melihat nilai akhirnya:
Klik kanan pada node Scorer yang sudah di-execute (berwarna hijau), lalu pilih Accuracy Statistics. Di jendela baru tersebut, Anda akan melihat tabel lengkap yang berisi nilai persentase Accuracy, Precision, Recall, dan F-Measure (F1-Score) untuk dimasukkan ke laporan analisis Anda.