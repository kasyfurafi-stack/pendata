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

# Naive Bayes Classification (KNIME + Python Script)

## Deskripsi
Proyek ini mengimplementasikan klasifikasi **Naive Bayes (GaussianNB)** menggunakan:
- KNIME → untuk preprocessing data
- Python Script (sklearn) → untuk model classifier

---

## Alur Proses di KNIME

1. **File Reader / CSV Reader**
   - Membaca dataset (contoh: Iris.csv)

2. **Data Preprocessing**
   - Missing Value (jika ada)
   - Normalisasi (opsional)
   - Column Filter (pilih fitur & target)

3. **Partitioning**
   - Membagi data:
     - 80% training
     - 20% testing

4. **Python Script Node (CORE MODEL)**
   - Model Naive Bayes dibuat di sini menggunakan sklearn

5. **Output**
   - Menampilkan hasil prediksi dan evaluasi

---

## Script Python (di dalam KNIME Python Script Node)

```python
import pandas as pd
from sklearn.naive_bayes import GaussianNB
from sklearn.metrics import accuracy_score, classification_report

# Ambil data dari KNIME
X_train = input_table_1.drop("target", axis=1)
y_train = input_table_1["target"]

X_test = input_table_2.drop("target", axis=1)
y_test = input_table_2["target"]

# Model Naive Bayes
model = GaussianNB()
model.fit(X_train, y_train)

# Prediksi
y_pred = model.predict(X_test)

# Evaluasi
accuracy = accuracy_score(y_test, y_pred)
report = classification_report(y_test, y_pred)

# Output ke KNIME
output_table = X_test.copy()
output_table["Actual"] = y_test
output_table["Predicted"] = y_pred

print("Accuracy:", accuracy)
print(report)
```

---
![python](hasilCode.png)
## Penjelasan Proses

1. **KNIME digunakan untuk preprocessing**
   - Membaca data mentah
   - Membersihkan dan membagi data

2. **Python Script digunakan untuk modeling**
   - Data training dan testing dikirim ke Python
   - Model GaussianNB dilatih menggunakan data training
   - Model memprediksi data testing

3. **Evaluasi hasil**
   - Accuracy → seberapa akurat model
   - Classification Report → detail performa tiap kelas

---

## Dataset
Gunakan dataset bebas (contoh: Iris CSV)

Format:
- Kolom fitur (numerik)
- 1 kolom target (label)

---

## Kesimpulan
Kombinasi KNIME dan Python memungkinkan:
- Visual workflow (KNIME)
- Fleksibilitas modeling (Python + sklearn)

Naive Bayes (GaussianNB) terbukti efektif untuk klasifikasi data numerik sederhana dengan akurasi tinggi.



