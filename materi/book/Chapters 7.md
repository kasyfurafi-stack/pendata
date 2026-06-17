# Laporan Analisis: Prediksi Performa Mahasiswa Menggunakan Algoritma Decision Tree di KNIME

**Disusun oleh:** [Nama Anda]  
**Tanggal:** [Tanggal Laporan]  

---

## 1. Penjelasan Data
Dataset yang digunakan dalam analisis ini adalah **"Higher Education Students Performance Evaluation"** yang bersumber dari *UCI Machine Learning Repository (ID: 856)*. 

* **Konteks Data:** Data ini merupakan hasil survei kuisioner yang dikumpulkan pada tahun 2019 dari 145 mahasiswa yang kuliah di Fakultas Teknik dan Ilmu Pendidikan di Siprus.
* **Karakteristik Data:** Memiliki 145 baris (mahasiswa) dengan lebih dari 30 kolom atribut (fitur). Seluruh data kategorikal telah di-encode menjadi bentuk angka (1, 2, 3, dst).
* **Struktur Variabel:**
    * **Demografi Pribadi:** Umur, jenis kelamin, tipe beasiswa, tipe akomodasi, dsb.
    * **Latar Belakang Keluarga:** Pendidikan orang tua, pekerjaan orang tua, status orang tua, jumlah saudara.
    * **Kebiasaan Akademik:** Jam belajar mingguan, frekuensi membaca buku, tingkat kehadiran kelas/seminar.
    * **Target (Kunci Jawaban):** *Grade* (Nilai Akhir Semester) atau Tipe Beasiswa yang didapat mahasiswa.

---

## 2. Permasalahan yang Diselesaikan
Dalam ruang lingkup *Educational Data Mining (EDM)*, permasalahan utama yang ingin diselesaikan adalah **ketidakmampuan institusi untuk memprediksi secara dini potensi kegagalan atau kesuksesan seorang mahasiswa** hanya dari kebiasaan dan latar belakangnya.

**Tujuan Analisis:**
1.  Membangun model *Machine Learning* yang dapat memprediksi nilai/prestasi mahasiswa di masa depan berdasarkan data profil dan kebiasaan belajar.
2.  Mengidentifikasi atribut/faktor mana yang paling berpengaruh signifikan terhadap kesuksesan akademik mahasiswa.
3.  Memberikan wawasan agar pihak kampus dapat memberikan intervensi dini (bimbingan khusus) kepada mahasiswa yang diprediksi akan mendapat nilai buruk.

---

## 3. Workflow Node dari KNIME
Untuk menyelesaikan permasalahan klasifikasi di atas, dirancang sebuah *workflow* di KNIME Analytics Platform. Alur kerja ini menggunakan algoritma **Decision Tree** (Pohon Keputusan).

Berikut adalah rancangan urutan node yang digunakan:
1.  **CSV Reader** (Membaca data)
2.  **Number To String** (Konversi tipe data kategori)
3.  **Table Partitioner** (Membagi data latih dan uji)
4.  **Color Manager** [Opsional] (Visualisasi kelas)
5.  **Decision Tree Learner** (Melatih model/Membangun pohon)
6.  **Decision Tree Predictor** (Menguji model pada data baru)
7.  **Scorer** (Mengevaluasi akurasi mesin)

---

## 4. Penjelasan dan Cara Membuat Node Hingga Akhir

Berikut adalah tahapan perakitan *workflow* dan sambungan kabel (*port*) antar node secara spesifik:

### Tahap A: Data Preparation (Persiapan Data)

**1. CSV Reader**
* **Fungsi:** Mengimpor dataset `.csv` ke dalam lembar kerja KNIME.
* **Cara Perakitan:** 1. Tarik node *CSV Reader* ke *workspace*.
    2. Klik ganda (Configure). Pada tab *Settings*, klik tombol *Browse* dan masukkan file `dataset_mahasiswa_uci_856.csv`.
    3. Pastikan kotak *Has Column Header* dicentang agar baris pertama dibaca sebagai judul. Klik OK dan *Execute*.

**2. Number To String**
* **Fungsi:** Mengubah atribut kategori yang berwujud angka (seperti kode gender 1=Pria) menjadi *String* agar terbaca sebagai label, bukan angka matematis.
* **Cara Perakitan:**
    1. Tarik node *Number To String*.
    2. **Sambungkan garis** dari port segitiga hitam (kanan) milik *CSV Reader* ke port segitiga putih (kiri) milik *Number To String*.
    3. *Configure*. Pindahkan kolom Target (contoh: `Grade` atau `Scholarship type`) dan kolom nominal lainnya dari kotak *Exclude* ke kotak *Include*. Klik OK dan *Execute*.

### Tahap B: Data Splitting (Pembagian Data)

**3. Table Partitioner**
* **Fungsi:** Memecah data menjadi dua jalur: Data Latih (untuk belajar) dan Data Uji (untuk tes akurasi).
* **Cara Perakitan:**
    1. Tarik node *Table Partitioner*.
    2. **Sambungkan garis** dari port kanan *Number To String* ke port kiri *Table Partitioner*.
    3. *Configure*. Pilih opsi **Relative** dan ketik persentase **80%**. Klik OK dan *Execute*.
    *(Catatan: Node ini memiliki 2 output. Segitiga atas adalah 80% data latih, segitiga bawah adalah 20% data uji).*

**4. Color Manager (Opsional)**
* **Fungsi:** Mewarnai baris data berdasarkan kategori target (misal: Lulus = Hijau, Gagal = Merah).
* **Cara Perakitan:**
    1. Tarik node *Color Manager*.
    2. **Sambungkan garis** dari **port segitiga ATAS** milik *Table Partitioner* ke port kiri *Color Manager*.
    3. *Configure*. Pilih kolom Target Anda pada menu *Column*, lalu atur warna tiap nilai. Klik OK.

### Tahap C: Modeling (Pelatihan & Prediksi)

**5. Decision Tree Learner**
* **Fungsi:** Membangun aturan percabangan pohon keputusan berdasarkan hitungan *Information Gain* dari Data Latih.
* **Cara Perakitan:**
    1. Tarik node *Decision Tree Learner*.
    2. **Sambungkan garis** dari port kanan *Color Manager* ke port kiri *Decision Tree Learner*. (Jika tidak pakai Color Manager, sambungkan dari port ATAS Partitioner).
    3. *Configure*. Pada kotak **Class column**, pilih kolom Target (kunci jawaban) yang ingin diprediksi. Klik OK dan *Execute*.
    *(Catatan: Node ini menghasilkan output berupa objek model, ditandai dengan port kotak berwarna biru).*

**6. Decision Tree Predictor**
* **Fungsi:** Menerapkan model/pola yang sudah dipelajari untuk menebak data baru (*Testing Data*).
* **Cara Perakitan:**
    1. Tarik node *Decision Tree Predictor*. Node ini butuh 2 input (Model dan Data Uji).
    2. **Sambungan 1 (Input Model):** Tarik garis dari **port kotak biru** (kanan) milik *Decision Tree Learner* ke **port kotak biru** (kiri atas) milik *Predictor*.
    3. **Sambungan 2 (Input Data):** Tarik garis dari **port segitiga BAWAH** milik *Table Partitioner* (Data Uji 20%) ke **port segitiga** (kiri bawah) milik *Predictor*.
    4. *Configure*. Biarkan *default*, node ini akan membuat kolom baru bernama *Prediction*. Klik OK dan *Execute*.

### Tahap D: Evaluation (Evaluasi)

**7. Scorer**
* **Fungsi:** Menilai seberapa akurat tebakan mesin dengan membandingkan kolom prediksi dan kolom aktual.
* **Cara Perakitan:**
    1. Tarik node *Scorer*.
    2. **Sambungkan garis** dari port kanan *Decision Tree Predictor* ke port kiri *Scorer*.
    3. *Configure*. Pada *First Column*, pilih kolom jawaban asli (misal: `Grade`). Pada *Second Column*, pilih kolom tebakan mesin (misal: `Prediction (Grade)`). Klik OK dan *Execute*.

---

## 5. Hasil
Setelah keseluruhan *workflow* dieksekusi (berstatus lampu hijau), hasil analisis dapat diinterpretasikan melalui dua cara utama:

1.  **Akurasi Model (Scorer Node)**
    Dengan melakukan klik kanan pada node *Scorer* dan memilih **Accuracy Statistics**, kita dapat melihat nilai **Accuracy**. Nilai ini merepresentasikan persentase tebakan mesin yang benar (misalnya 85%). Selain itu, tabel **Confusion Matrix** menunjukkan secara detail rincian tebakan (berapa banyak data mahasiswa berprestasi yang berhasil ditebak benar, dan berapa prediksi yang meleset).

2.  **Penemuan Pola Aturan (Decision Tree View)**
    Dengan melakukan klik kanan pada node *Decision Tree Learner* dan memilih **View: Decision Tree View**, sistem menampilkan diagram pohon keputusan secara visual. Dari grafik ini, dapat disimpulkan atribut apa yang terpilih sebagai *Root Node* (Akar tertinggi). Atribut yang berada paling atas merupakan faktor paling penting dan paling kuat dalam menentukan nilai akhir seorang mahasiswa (misalnya, atribut *Weekly study hours* atau *Scholarship type*). Pola rentetan *If-Then* ini dapat dijadikan rujukan pengambil kebijakan kampus untuk memantau performa mahasiswanya.