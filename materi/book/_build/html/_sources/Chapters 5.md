# Mengukur Jarak/Similaritas Data

## Prepocessing 
### Normalisasi




---
## Normalisasi data 
Normalisasi data adalah teknik pra-pemrosesan yang sangat penting dalam *data mining* dan *machine learning*. Tujuannya adalah menyamakan skala seluruh variabel/fitur agar tidak ada satu atribut pun yang mendominasi atribut lain hanya karena memiliki rentang angka yang lebih besar (misalnya, membandingkan atribut "gaji" dalam jutaan dengan "umur" dalam puluhan).

Berikut adalah macam-macam teknik normalisasi data yang paling sering digunakan:

---
### 1. Min-Max Normalization (Rescaling)

Teknik ini mengubah ukuran data sehingga jatuh pada rentang nilai tertentu, paling sering antara **0 dan 1** (atau -1 hingga 1). Ini sangat cocok digunakan untuk algoritma yang menghitung jarak antar titik data, seperti *K-Means clustering*.

* **Kelebihan:** Mempertahankan hubungan asli antar data.
* **Kelemahan:** Sangat sensitif terhadap *outlier* (pencilan data/nilai ekstrem).
* **Rumus:**

$$x_{norm} = \frac{x - x_{min}}{x_{max} - x_{min}}$$

Misal kita punya array data: **`X = [10, 20, 30, 40, 50]`**

#### Contoh : 

Mengubah skala data agar masuk ke dalam rentang 0 sampai 1.

* **Rumus:** 
$$X_{norm} = \frac{X - X_{min}}{X_{max} - X_{min}}$$


* **Data kita:** $X_{min} = 10$, $X_{max} = 50$.
* **Contoh hitung (untuk nilai 30):**

$$X_{norm} = \frac{30 - 10}{50 - 10} = \frac{20}{40} = 0.5$$


* **Hasil seluruh data:** `[0.0, 0.25, 0.5, 0.75, 1.0]`


---
### 2. Z-Score Normalization (Standardization)

Teknik ini mengubah data sedemikian rupa sehingga nilai rata-rata (*mean*) dari kumpulan data menjadi 0 dan standar deviasinya menjadi 1.

* **Kelebihan:** Jauh lebih kebal terhadap *outlier* dibandingkan Min-Max karena menggunakan metrik penyebaran data.
* **Kelemahan:** Data hasil normalisasi tidak memiliki batas rentang angka yang pasti seperti 0 hingga 1.
* **Rumus:**

$$x_{norm} = \frac{x - \mu}{\sigma}$$
*(Keterangan: $\mu$ adalah rata-rata, dan $\sigma$ adalah standar deviasi).*

---
#### Contoh :

Mengubah data supaya nilai rata-rata (*mean*) menjadi 0 dan standar deviasi menjadi 1. Paling aman kalau datamu banyak *outlier* (nilai ekstrem).

* **Rumus:** 
$$X_{norm} = \frac{X - \mu}{\sigma}$$


* **Data kita:** * Rata-rata ($\mu$) = $30$
* Standar deviasi populasi ($\sigma$) $\approx 14.14$


* **Contoh hitung (untuk nilai 40):**

$$X_{norm} = \frac{40 - 30}{14.14} = \frac{10}{14.14} \approx 0.707$$


* **Hasil seluruh data:** `[-1.414, -0.707, 0.0, 0.707, 1.414]`

---
### 3. Decimal Scaling

Teknik ini bekerja dengan menggeser titik desimal dari nilai data. Jumlah pergeseran desimal bergantung pada nilai absolut maksimum di dalam atribut tersebut.

* **Kelebihan:** Sederhana dan mudah dihitung.
* **Rumus:**

$$x_{norm} = \frac{x}{10^j}$$

*(Keterangan: $j$ adalah bilangan bulat terkecil yang membuat nilai mutlak maksimum dari $x_{norm}$ kurang dari 1).*

#### Contoh :
Menggeser koma desimal. Pembaginya ditentukan oleh nilai angka terbesar di dataset supaya nilai akhirnya kurang dari 1.

* **Rumus:** 
$$X_{norm} = \frac{X}{10^j}$$


* **Data kita:**
* Angka absolut paling besar = 50.
* Kita cari nilai $j$ yang kalau 50 dibagi $10^j$ hasilnya $< 1$.
* Maka $j = 2$ (karena $10^2 = 100$, dan $50 / 100 = 0.5$). Semua data akan dibagi 100.


* **Contoh hitung (untuk nilai 20):**

$$X_{norm} = \frac{20}{10^2} = 0.2$$


* **Hasil seluruh data:** `[0.1, 0.2, 0.3, 0.4, 0.5]`

---
## Implementasi dengan Sklearn dan Fungsi Kustom
Berikut adalah script Python menggunakan scikit-learn untuk Min-Max, Z-Score, dan Robust, serta satu fungsi manual untuk Decimal Scaling.

```Python
import numpy as np
from sklearn.preprocessing import MinMaxScaler, StandardScaler, RobustScaler

# Data asli (sklearn membutuhkan format array 2D, misal kolom ke-bawah)
X = np.array([[10], [20], [30], [40], [50]])
print("Data Asli:\n", X.flatten())
print("-" * 40)

# 1. Min-Max Scaling (Sklearn)
minmax_scaler = MinMaxScaler()
X_minmax = minmax_scaler.fit_transform(X)
print("1. Hasil Min-Max Scaling:\n", X_minmax.flatten())

# 2. Z-Score / Standardization (Sklearn)
standard_scaler = StandardScaler()
X_standard = standard_scaler.fit_transform(X)
print("2. Hasil Z-Score (Standardization):\n", X_standard.flatten())

# 3. Robust Scaling (Sklearn)
robust_scaler = RobustScaler()
X_robust = robust_scaler.fit_transform(X)
print("3. Hasil Robust Scaling:\n", X_robust.flatten())

# 4. Decimal Scaling (Custom Function)
def decimal_scaling(data):
    # Cari nilai j (pangkat 10) dari nilai mutlak maksimum
    max_abs_val = np.max(np.abs(data))
    j = np.ceil(np.log10(max_abs_val))
    
    # Bagi data dengan 10 pangkat j
    data_scaled = data / (10**j)
    return data_scaled

X_decimal = decimal_scaling(X)
print("4. Hasil Decimal Scaling:\n", X_decimal.flatten())
```

---
## Tugas - Missing Values
Berikut adalah transkripsi ulang dari data yang ada di foto Anda, beserta penjelasan langkah demi langkah untuk mencari nilai yang diberi tanda tanya (`?`).

### 1. Transkripsi Data

**Tabel Data Asli (Kiri) & Data Normalisasi (Kanan)**

| No  | IPK Asli | PO Asli | JML Asli |     | IPK Norm | PO Norm | JMK Norm | WKNN |
| --- | ---      | ---     | ---      | --- | ---       | --- | --- | --- |
| 1   | 2        | 200000  | 2        |     | 0         | 0 | 0 |  |
| 2   | 3        | 300000  | 3        |     | 0.5       | 0.5 | 1 |  |
| 3   | 4        | 200000  | 2        |     | 1         | 0 | 0 |  |
| 4   | 2        | 200000  | 3        |     | 0         | 0 | 1 |  |
| 5   | 3        | 300000  | 2        |     | 0.5       | 0.5 | 0 |  |
| 6   | 4        | 400000  | 3        |     | 1         | 1 | 1 |  |
|**7**| **2**    |**300000**| **?**   |     | **0**     | **0.5** | **?** |  |

---

### 2. Penjelasan Proses yang Sedang Terjadi
 
* **Min-Max Normalization:** Data asli (IPK rentang 2–4, PO rentang 200000–400000) diubah menjadi skala 0 hingga 1 agar atribut PO yang angkanya ratusan ribu tidak mendominasi perhitungan jarak.
* **Encoding Target:** Kolom kelas target `JML` (berisi angka 2 dan 3) diubah menjadi biner `JMK` (angka 0 dan 1) untuk mempermudah perhitungan model.
* **Tujuan:** Anda diminta untuk memprediksi nilai target `?` pada baris ke-7 menggunakan data latih dari baris 1 sampai 6.

---

### 3. Mencari Nilai Tanda Tanya (?) dengan WKNN

Untuk memprediksi kelas baris ke-7 dengan data yang sudah dinormalisasi `(IPK = 0, PO = 0.5)`, kita harus menghitung jarak *Euclidean* dari data target ini ke semua data latih (baris 1-6).

Rumus jarak Euclidean:


$$d = \sqrt{(IPK_2 - IPK_1)^2 + (PO_2 - PO_1)^2}$$

**Perhitungan Jarak Target ke Setiap Baris:**

* **Ke Baris 1** (0, 0): $d = \sqrt{(0-0)^2 + (0.5-0)^2} = \sqrt{0 + 0.25} = 0.5$ *(Kelas JMK: 0)*
* **Ke Baris 2** (0.5, 0.5): $d = \sqrt{(0.5-0)^2 + (0.5-0.5)^2} = \sqrt{0.25 + 0} = 0.5$ *(Kelas JMK: 1)*
* **Ke Baris 3** (1, 0): $d = \sqrt{(1-0)^2 + (0-0.5)^2} = \sqrt{1 + 0.25} = \sqrt{1.25} \approx 1.118$ *(Kelas JMK: 0)*
* **Ke Baris 4** (0, 0): $d = \sqrt{(0-0)^2 + (0.5-0)^2} = 0.5$ *(Kelas JMK: 1)*
* **Ke Baris 5** (0.5, 0.5): $d = \sqrt{(0.5-0)^2 + (0.5-0.5)^2} = 0.5$ *(Kelas JMK: 0)*
* **Ke Baris 6** (1, 1): $d = \sqrt{(1-0)^2 + (1-0.5)^2} = \sqrt{1 + 0.25} = \sqrt{1.25} \approx 1.118$ *(Kelas JMK: 1)*

**Analisis Hasil (Ada Masalah pada Dataset):**
Jika Anda perhatikan jarak di atas, terdapat 4 tetangga terdekat yang memiliki jarak persis sama ke data target, yaitu **0.5** (Baris 1, 2, 4, dan 5).

Algoritma WKNN memberikan bobot (*weight*) berdasarkan kebalikan dari jarak ($w = 1/d$). Karena keempat jarak ini sama persis ($0.5$), maka bobotnya juga sama persis ($w = 2$).

* Total bobot untuk Kelas 0 (dari baris 1 & 5) = $2 + 2 = 4$
* Total bobot untuk Kelas 1 (dari baris 2 & 4) = $2 + 2 = 4$

**Kesimpulan untuk Nilai `?`:**
Dataset Excel ini memiliki anomali/kontradiksi (Baris 1 dan 4 datanya sama persis tapi kelasnya beda, begitu juga baris 2 dan 5). Akibatnya, perhitungan WKNN menghasilkan **seri (tie)** dengan bobot 50:50 antara Kelas 0 dan Kelas 1.

---
### kode untuk menghitung Missing values

```sql
import math

# 1. Menyiapkan Data Latih (Baris 1 - 6) berdasarkan hasil normalisasi
# Format: [IPK_Norm, PO_Norm, JMK_Norm (Kelas)]
train_data = [
    {"baris": 1, "ipk": 0,   "po": 0,   "kelas": 0},
    {"baris": 2, "ipk": 0.5, "po": 0.5, "kelas": 1},
    {"baris": 3, "ipk": 1,   "po": 0,   "kelas": 0},
    {"baris": 4, "ipk": 0,   "po": 0,   "kelas": 1},
    {"baris": 5, "ipk": 0.5, "po": 0.5, "kelas": 0},
    {"baris": 6, "ipk": 1,   "po": 1,   "kelas": 1}
]

# 2. Menyiapkan Data Target (Baris 7 yang dicari nilainya)
target_ipk = 0
target_po = 0.5

print("=== PERHITUNGAN JARAK (EUCLIDEAN DISTANCE) ===")
hasil_jarak = []

for data in train_data:
    # Rumus Euclidean Distance: akar( (x2 - x1)^2 + (y2 - y1)^2 )
    jarak = math.sqrt((data["ipk"] - target_ipk)**2 + (data["po"] - target_po)**2)
    hasil_jarak.append({
        "baris": data["baris"],
        "jarak": jarak,
        "kelas": data["kelas"]
    })

# Urutkan data dari jarak yang paling dekat ke paling jauh
hasil_jarak_urut = sorted(hasil_jarak, key=lambda x: x["jarak"])

for h in hasil_jarak_urut:
    print(f"Ke Baris {h['baris']} -> Jarak = {h['jarak']:.4f} | Kelas (JMK) = {h['kelas']}")


print("\n=== PERHITUNGAN BOBOT (WEIGHT) WKNN ===")
# Misal kita menggunakan K = 4 (karena ada 4 baris yang jaraknya sama-sama terdekat yaitu 0.5)
K = 4 
tetangga_terdekat = hasil_jarak_urut[:K]

bobot_kelas_0 = 0.0
bobot_kelas_1 = 0.0

for t in tetangga_terdekat:
    # Rumus bobot WKNN: weight = 1 / jarak
    bobot = 1 / t["jarak"]
    
    if t["kelas"] == 0:
        bobot_kelas_0 += bobot
    elif t["kelas"] == 1:
        bobot_kelas_1 += bobot
        
    print(f"Baris {t['baris']} (Kelas {t['kelas']}): Bobot = {bobot:.2f}")

print("\n=== HASIL AKHIR WKNN ===")
print(f"Total Bobot Kelas 0 : {bobot_kelas_0:.2f}")
print(f"Total Bobot Kelas 1 : {bobot_kelas_1:.2f}")

if bobot_kelas_0 > bobot_kelas_1:
    print("=> Kesimpulan: Baris ke-7 diklasifikasikan sebagai Kelas 0")
elif bobot_kelas_1 > bobot_kelas_0:
    print("=> Kesimpulan: Baris ke-7 diklasifikasikan sebagai Kelas 1")
else:
    print("=> Kesimpulan: SERI (Tie)! Bobot kelas 0 dan 1 sama kuat karena data latih Baris 1/4 dan 2/5 saling bertentangan nilainya.")
```
---