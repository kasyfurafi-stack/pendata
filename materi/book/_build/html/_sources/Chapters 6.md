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

df = pd.read_csv("data.csv")
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