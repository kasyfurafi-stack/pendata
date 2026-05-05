# Naive Bayes - Analisis Data

## Deskripsi
Analisis data ini menggunakan metode **Naive Bayes Classifier** dengan library **Scikit-learn** pada Python.  
Naive Bayes merupakan algoritma klasifikasi berbasis probabilitas yang bekerja berdasarkan Teorema Bayes.

Metode ini cocok digunakan untuk klasifikasi data numerik maupun kategorikal karena proses komputasinya cepat dan sederhana.

---

## Tools yang Digunakan
- Python
- Pandas
- Scikit-learn
- Jupyter Notebook / Google Colab / VS Code

---

## Script Python
```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import GaussianNB
from sklearn.metrics import accuracy_score, classification_report

df = pd.read_csv("target-data.csv")
X = df.drop("target", axis=1)
y = df["target"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

model = GaussianNB()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)

print("Accuracy:", accuracy_score(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

---

## Penjelasan Singkat
1. Dataset dibaca menggunakan Pandas  
2. Data dipisahkan menjadi fitur (`X`) dan target (`y`)  
3. Data dibagi menjadi data training dan testing  
4. Model Gaussian Naive Bayes dilatih menggunakan data training  
5. Model melakukan prediksi pada data testing  
6. Hasil evaluasi ditampilkan dalam bentuk akurasi dan classification report  

---

## Hasil Analisis
Output yang dihasilkan berupa:
- Nilai akurasi
- Precision
- Recall
- F1-score

Nilai tersebut digunakan untuk mengetahui performa model dalam melakukan klasifikasi.

---

## Kesimpulan
Naive Bayes merupakan metode klasifikasi yang sederhana, cepat, dan efektif untuk analisis data.  
Model ini dapat digunakan untuk memprediksi kelas data berdasarkan pola yang dipelajari dari dataset training.


---

# Tugas

## Deskripsi
Proses ini menjelaskan alur lengkap penggunaan **KNIME** dari data mentah hingga menghasilkan output klasifikasi menggunakan **Naive Bayes (GaussianNB)** melalui **Python Script (sklearn)**.

---

## 1. Import Data (Data Mentah)

### Node: CSV Reader
**Langkah:**
1. Tambahkan node **CSV Reader**
2. Pilih file `iris.csv`
3. Execute

**Penjelasan:**
- Membaca data mentah dari file CSV
- Output berupa tabel berisi fitur dan target

---

## 2. Cek & Bersihkan Data

### Node: Missing Value (Opsional)
**Langkah:**
1. Sambungkan dari CSV Reader
2. Pilih metode pengisian (Mean untuk numerik)

**Penjelasan:**
- Digunakan untuk menangani data kosong
- Bisa dilewati jika dataset sudah bersih

---

## 3. Seleksi Kolom

### Node: Column Filter
**Langkah:**
1. Sambungkan dari node sebelumnya
2. Pilih hanya:
   - Kolom fitur (numerik)
   - Kolom `target`

**Penjelasan:**
- Menghindari kolom tidak relevan masuk ke model
- Menyesuaikan struktur data untuk machine learning

---

## 4. Split Data (Training & Testing)

### Node: Partitioning
**Langkah:**
1. Sambungkan dari Column Filter
2. Atur:
   - Training: 80%
   - Testing: 20%
   - Aktifkan **Stratified Sampling**
   - Pilih kolom `target`

**Penjelasan:**
- Membagi data menjadi:
  - Data training (melatih model)
  - Data testing (evaluasi model)
- Stratified menjaga distribusi kelas tetap seimbang

---

## 5. Modeling (Python Script - sklearn)

### Node: Python Script

**Koneksi:**
- Output atas (training) → input 1
- Output bawah (testing) → input 2

---

### Script Python
```python
import pandas as pd
from sklearn.naive_bayes import GaussianNB
from sklearn.metrics import accuracy_score, classification_report

# Ambil data dari KNIME
train_df = input_table_1.copy()
test_df = input_table_2.copy()

# Pisahkan fitur & target
X_train = train_df.drop(columns=["target"])
y_train = train_df["target"]

X_test = test_df.drop(columns=["target"])
y_test = test_df["target"]

# Model
model = GaussianNB()
model.fit(X_train, y_train)

# Prediksi
y_pred = model.predict(X_test)

# Evaluasi
accuracy = accuracy_score(y_test, y_pred)
print("Accuracy:", accuracy)
print(classification_report(y_test, y_pred))

# Output ke KNIME
output_table = test_df.copy()
output_table["Predicted"] = y_pred
```

---

### Penjelasan Proses
- Data training digunakan untuk melatih model
- Data testing digunakan untuk evaluasi
- GaussianNB dipilih karena data numerik
- Output:
  - Nilai akurasi
  - Classification report
  - Hasil prediksi

---

## 6. Menampilkan Output

### Node: Table View
**Langkah:**
1. Sambungkan dari Python Script
2. Execute

**Penjelasan:**
- Menampilkan hasil akhir dalam bentuk tabel
- Terdapat kolom tambahan: **Predicted**

---

## 7. Alur Workflow

```
CSV Reader
   ↓
Missing Value (opsional)
   ↓
Column Filter
   ↓
Partitioning
  ↙      ↘
Train    Test
   ↓        ↓
   └── Python Script ──→ Table View
```

---

## 8. Ringkasan Proses

1. Data mentah dibaca dari CSV  
2. Data dibersihkan dan dipilih kolom penting  
3. Data dibagi menjadi training dan testing  
4. Model Naive Bayes dilatih menggunakan Python (sklearn)  
5. Model melakukan prediksi  
6. Hasil ditampilkan dalam bentuk tabel dan evaluasi  

---

## 9. Kesimpulan
- KNIME digunakan untuk preprocessing dan workflow visual  
- Python Script digunakan untuk modeling Naive Bayes  
- Model mampu melakukan klasifikasi dengan akurasi tinggi pada data numerik sederhana  