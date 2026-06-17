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

Berikut adalah tahapan *step-by-step* eksekusi di KNIME:

### Tahap A: Data Preparation (Persiapan Data)
1.  **CSV Reader**: 
    * *Fungsi:* Mengimpor dataset `.csv` ke dalam sistem.
    * *Cara:* Tambahkan node, *Configure*, klik *Browse* dan pilih file `dataset_mahasiswa_uci_856.csv`. Centang *Has Column Header*.
2.  **Number To String**:
    * *Fungsi:* Mengubah atribut berskala nominal/ordinal (seperti kode tipe beasiswa atau gender) dari angka (Number) menjadi teks (String) agar algoritma membacanya sebagai klasifikasi, bukan perhitungan matematika.
    * *Cara:* Sambungkan dari CSV Reader. *Configure*, lalu masukkan kolom *Target* dan kolom kategori lainnya dari kotak *Exclude* ke kotak *Include*.

### Tahap B: Data Splitting (Pembagian Data)
3.  **Table Partitioner**:
    * *Fungsi:* Mem