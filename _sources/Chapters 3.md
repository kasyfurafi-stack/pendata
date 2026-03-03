# Pengantar Data Science 

## Ekplorasi data iris

<h2>korelasi antara sepal_width dan sepal_length</h2>

![Grafik](grafik/c2/gambar1.png)

<p>Dari gambar di atas menunjukkan korelasi antara sepal_widh dan sepal_length sangat lemah atau tidak ada korelasi, dikarenakan Titik-titik data tersebar tanpa membentuk pola yang jelas, menunjukkan bahwa tidak ada hubungan yang kuat antara sepal length dan sepal width. artinya Kedua variabel ini dapat dianggap sebagai fitur yang berdiri sendiri dan tidak saling mempengaruhi secara linear.</p>

---

<h2>korelasi antara petal_width dan petal_length</h2>

![Grafik](grafik/c2/gambar2.png)
<p>dari gambar di atas menunjukkan korelasi antara petal_width dan petal_length sangat kuat, dikarenakan Titik-titik data membentuk pola yang jelas dari kiri bawah ke kanan atas, menunjukkan bahwa semakin besar nilai petal_length, semakin besar pula nilai petal_width. artinya kedua variabel sangat rapat membentuk pola linear yang jelas. namun terdapat Dua cluster yang terpisah kemungkinan besar merepresentasikan iris yang berbeda, tetapi tidak menyebabkan ambigu.</p>

---

<h2>korelasi antara sepal_length dan petal_length</h2>

![Grafik](grafik/c2/gambar3.png)
<p>Dari gambar di atas menunjukkan korelasi antara sepal_length dan petal_length sangat kuat, dikarenakan titik-titik data membentuk pola yang jelas dari kiri bawah ke kanan atas, menunjukkan bahwa semakin besar nilai sepal_length, semakin besar pula nilai petal_length. Artinya kedua variabel sangat rapat membentuk pola linear yang jelas. Namun terdapat dua cluster yang terpisah kemungkinan besar merepresentasikan iris yang berbeda, tetapi tidak menyebabkan ambigu.</p>

---
<h2>korelasi antara sepal_length dan petal_width</h2><br>

![Grafik](grafik/c2/gambar4.png"/>
<p>Dari gambar di atas menunjukkan korelasi antara sepal_length dan petal_width sangat kuat, dikarenakan titik-titik data membentuk pola yang jelas dari kiri bawah ke kanan atas, menunjukkan bahwa semakin besar nilai sepal_length, semakin besar pula nilai petal_width. Artinya kedua variabel sangat rapat membentuk pola linear yang jelas. Namun terdapat dua cluster yang terpisah kemungkinan besar merepresentasikan iris yang berbeda, tetapi tidak menyebabkan ambigu.</p>

---
<h2>korelasi antara sepal_width dan petal_length</h2><br>

![Grafik](grafik/c2/gambar5.png)
<p>Dari gambar di atas menunjukkan korelasi antara sepal_width dan petal_length cenderung lemah, dikarenakan titik-titik data tidak membentuk pola linear yang konsisten dari kiri bawah ke kanan atas. Terlihat adanya dua cluster yang sangat terpisah secara vertikal, di mana cluster bawah memiliki petal_length rendah dan cluster atas memiliki petal_length tinggi, namun dalam masing-masing cluster tidak ada hubungan yang jelas dengan sepal_width. Artinya kedua variabel tidak menunjukkan pola yang rapat dan penyebaran data relatif acak. Dua cluster yang terpisah ini kemungkinan besar merepresentasikan spesies iris yang berbeda dengan karakteristik yang sangat berbeda, dan pemisahan yang sangat jelas ini tidak menyebabkan ambigu.</p>

---
<h2>korelasi antara sepal_width dan petal_width</h2><br>

![Grafik](grafik/c2/gambar6.png)
<p>Dari gambar di atas menunjukkan korelasi antara sepal_width dan petal_width lemah atau tidak konsisten, dikarenakan titik-titik data tidak membentuk pola linear yang jelas dari kiri bawah ke kanan atas. Terlihat adanya dua cluster yang sangat terpisah secara vertikal, di mana cluster bawah memiliki petal_width sangat rendah dan cluster atas memiliki petal_width lebih tinggi, namun dalam masing-masing cluster penyebaran data relatif acak tanpa menunjukkan hubungan yang kuat dengan sepal_width. Artinya kedua variabel tidak membentuk pola linear yang rapat dan peningkatan sepal_width tidak diikuti oleh peningkatan petal_width secara konsisten. Dua cluster yang terpisah ini kemungkinan besar merepresentasikan spesies iris yang berbeda, dan pemisahan yang sangat jelas ini tidak menyebabkan ambigu.</p>

---
<h2>statistik dikriptif</h2><br>

![Grafik](grafik/c2/statistik.jpg)
<p>Berdasarkan tabel statistik deskriptif di atas, dataset Iris menunjukkan karakteristik yang menarik untuk setiap variabel pengukuran. Pada sepal_length, nilai rata-rata sebesar 5.84 cm sangat dekat dengan median 5.8 cm, mengindikasikan distribusi data yang relatif simetris dan terkonsentrasi di kisaran 5-6 cm dengan variasi yang kecil. Sementara itu, sepal_width memiliki mean 3.05 cm dengan median dan mode sama-sama bernilai 3 cm, menunjukkan bahwa lebar sepal cenderung homogen antar spesies dengan penyebaran data yang rapat.
Berbeda dengan pengukuran sepal, variabel petal_length dan petal_width menunjukkan pola yang lebih kompleks. Nilai mode pada petal_length (1.5 cm) dan petal_width (0.2 cm) sangat berbeda dengan median masing-masing (4.35 cm dan 1.3 cm), yang mengindikasikan adanya distribusi bimodal atau dua kelompok data yang terpisah jelas. Hal ini diperkuat oleh nilai dispersi yang lebih tinggi pada petal_width (0.63) dibandingkan variabel lainnya, menunjukkan bahwa pengukuran petal memiliki variabilitas yang lebih besar dan lebih efektif untuk membedakan antar spesies.</p>

---
<h2>python (google colab)</h2><br>
<h2>bukti screenshot</h2><br>

![Grafik](grafik/c2/ch1.png)

![Grafik](grafik/c2/ch2.png)

---
<h2>link program</h2><br>

https://colab.research.google.com/drive/1GSy-86MX61px6TsFmbnX_iAG0U7MrHCT?usp=sharing

---
<h2>kode lengkap</h2><br>
<p>

```python
import pandas as pd
from scipy import stats

df = pd.read_csv("IRIS.csv")

print("Daftar Kolom:", df.columns.tolist())
print("-" * 60)

kolom_numerik = ['sepal_length', 'sepal_width', 'petal_length', 'petal_width']

for kolom in kolom_numerik:
    print(f"\n Statistik untuk kolom: {kolom.upper()}")
    print("-" * 40)
    print("Jumlah data     :", df[kolom].count())
    print("Rata-rata       :", "{0:.2f}".format(df[kolom].mean()))
    print("Nilai minimal   :", df[kolom].min())
    print("Q1              :", "{0:.2f}".format(df[kolom].quantile(0.25)))
    print("Q2 (Median)     :", "{0:.2f}".format(df[kolom].quantile(0.5)))
    print("Q3              :", "{0:.2f}".format(df[kolom].quantile(0.75)))
    print("Nilai Max       :", df[kolom].max())
    print("Kemencengan 1   :", "{0:.2f}".format(round(df[kolom].skew(), 2)))
    print("Kemencengan 2   :", "{0:.6f}".format(round(df[kolom].skew(), 6)))
    print("Standar Deviasi :", "{0:.2f}".format(round(df[kolom].std(), 2)))
    print("Variansi        :", "{0:.2f}".format(round(df[kolom].var(), 2)))
    
    mode_result = stats.mode(df[kolom].dropna(), keepdims=True)
    if len(mode_result.mode) > 0 and not pd.isna(mode_result.mode[0]):
        print("Nilai modus     : {} dengan frekuensi {}".format(
            mode_result.mode[0], mode_result.count[0]))
    else:
        print("Nilai modus     : Tidak ada modus tunggal")

print(f"\n🌸 Statistik untuk kolom: SPECIES")
print("-" * 40)
print("Jumlah data     :", df['species'].count())
print("Jumlah unik     :", df['species'].nunique())
print("Nilai unik      :", df['species'].unique().tolist())
print("\nDistribusi frekuensi:")
print(df['species'].value_counts())
print("\nModus (kategori paling sering):", df['species'].mode().values[0])
```
</p>

---
<h2>output </h2><br>

<p>

```text
Daftar Kolom: ['sepal_length', 'sepal_width', 'petal_length', 'petal_width', 'species']
------------------------------------------------------------

 Statistik untuk kolom: SEPAL_LENGTH
----------------------------------------
Jumlah data     : 150
Rata-rata       : 5.84
Nilai minimal   : 4.3
Q1              : 5.10
Q2 (Median)     : 5.80
Q3              : 6.40
Nilai Max       : 7.9
Kemencengan 1   : 0.31
Kemencengan 2   : 0.314911
Standar Deviasi : 0.83
Variansi        : 0.69
Nilai modus     : 5.0 dengan frekuensi 10

 Statistik untuk kolom: SEPAL_WIDTH
----------------------------------------
Jumlah data     : 150
Rata-rata       : 3.05
Nilai minimal   : 2.0
Q1              : 2.80
Q2 (Median)     : 3.00
Q3              : 3.30
Nilai Max       : 4.4
Kemencengan 1   : 0.33
Kemencengan 2   : 0.334053
Standar Deviasi : 0.43
Variansi        : 0.19
Nilai modus     : 3.0 dengan frekuensi 26

 Statistik untuk kolom: PETAL_LENGTH
----------------------------------------
Jumlah data     : 150
Rata-rata       : 3.76
Nilai minimal   : 1.0
Q1              : 1.60
Q2 (Median)     : 4.35
Q3              : 5.10
Nilai Max       : 6.9
Kemencengan 1   : -0.27
Kemencengan 2   : -0.274464
Standar Deviasi : 1.76
Variansi        : 3.11
Nilai modus     : 1.5 dengan frekuensi 14

 Statistik untuk kolom: PETAL_WIDTH
----------------------------------------
Jumlah data     : 150
Rata-rata       : 1.20
Nilai minimal   : 0.1
Q1              : 0.30
Q2 (Median)     : 1.30
Q3              : 1.80
Nilai Max       : 2.5
Kemencengan 1   : -0.10
Kemencengan 2   : -0.104997
Standar Deviasi : 0.76
Variansi        : 0.58
Nilai modus     : 0.2 dengan frekuensi 28

🌸 Statistik untuk kolom: SPECIES
----------------------------------------
Jumlah data     : 150
Jumlah unik     : 3
Nilai unik      : ['Iris-setosa', 'Iris-versicolor', 'Iris-virginica']

Distribusi frekuensi:
species
Iris-setosa        50
Iris-versicolor    50
Iris-virginica     50
Name: count, dtype: int64

Modus (kategori paling sering): Iris-setosa
```
</p>

## penjelasan mengukur Jarak dengan tipe data campuran
<h2>Latar Belakang</h2><br>
<p>Dalam praktik nyata, database yang digunakan untuk analisis data sering kali tidak hanya mengandung satu jenis tipe data saja, melainkan berbagai tipe data yang tercampur menjadi satu kesatuan. Sebagai contoh, sebuah dataset dapat memuat atribut nominal seperti warna atau jenis produk, atribut binary simetris seperti jenis kelamin, atribut binary asimetris seperti hasil tes medis yang bernilai Y/N, atribut numerik berupa data interval atau rasio seperti suhu atau pendapatan, serta atribut ordinal yang memiliki tingkatan atau peringkat seperti level kepuasan atau tingkat pendidikan. Karena setiap tipe data tersebut memiliki karakteristik dan cara pengukuran yang berbeda-beda, kita tidak dapat menerapkan satu rumus jarak secara langsung untuk menghitung kemiripan atau perbedaan antar objek. Sebagai solusi, pendekatan yang dapat digunakan adalah metode pembobotan, yaitu dengan menghitung jarak untuk setiap atribut secara terpisah sesuai dengan tipe datanya, kemudian menggabungkan seluruh hasil perhitungan tersebut menggunakan rumus jarak campuran yang memperhitungkan indikator validitas setiap atribut. Dengan pendekatan ini, seluruh jenis atribut dapat berkontribusi secara proporsional dalam perhitungan jarak akhir, sehingga hasil analisis menjadi lebih akurat dan mencerminkan karakteristik data yang sebenarnya.
</p>

---
<h2>Rumus mengukur jarak data campuran</h2><br>

![Grafik](grafik/c2/image.png)
<p>Keterangan:</p>
<table>
<tr>
<td>simbol</td>
<td>penjelasan</td>
</tr>
<tr>
<td>d(i,j)</td>
<td>Jarak antara objek i dan j</td>
</tr>
<tr>
<td>p</td>
<td>umlah total atribut</td>
</tr>
<tr>
<td>δ 
ij
(f)
​
</td>
<td>Indikator: 1 jika atribut ke-f valid untuk dibandingkan, 0 jika tidak (misal: data missing)</td>
</tr>
<tr>
<td>d 
ij
(f)
​
</td>
<td>	
Jarak untuk atribut ke-f saja</td>
</tr>
</table>

<h2> Cara Menghitung d(f)ij per Tipe Atribut</h2><bf>
<h3>1. Atribut Nominal atau Binary</h3><br>
<p>ij(f) = 0, jika xif = xjf  (nilai sama)</p><br>
<p>dij(f) = 1, jika xif ≠ xjf  (nilai berbeda)</p><br>
<p>cara penghitungannya Menggunakan metode simple matching.</p><br>
<h3>2. Atribut Numerik</h3><br>
<p>Lakukan normalisasi terlebih dahulu agar skala seragam, misalnya dengan:</p><br>
![Grafik](grafik/c2/image-1.png"/>
<p>Mean Absolute Deviation: lebih robust terhadap outlier</p><br>
<p>Setelah dinormalisasi, hitung jarak dengan metode numerik (Euclidean, Manhattan, dll).</p><br>
<h3>Atribut Ordinal</h3><br>
<p>Langkah-langkah:</p><br>
<p>Ganti nilai dengan ranking 
r
i
f
​ (misal: rendah=1, sedang=2, tinggi=3)</p><br>
![Grafik](grafik/c2/image-2.png"/>
<p>Hitung jarak menggunakan metode numerik pada nilai 
z
i
f
​</p><br>

---
## analisi mengunakan orange data mining untuk data yang campuran

![Grafik](grafik/c2/a_page-0001.png)
<p>contoh data saya untuk menganalisis penghitungan jarak di orange</p><br>
![Grafik](grafik/c2/image-3.png"/>
<p>Widget Distances digunakan untuk menghitung matriks dissimilarity (jarak) antar objek dalam dataset. arameter Compare diset ke Rows yang berarti perhitungan jarak dilakukan antar objek/data point (baris dalam dataset), bukan antar atribut. Hal ini sesuai dengan konsep matriks dissimilarity, dimana matriks segitiga dihasilkan dari perhitungan jarak antar n titik data. Metric jarak yang dipilih adalah Manhattan (normalized) karena data yang saya pakai memiliki data campuran</p>
![Grafik](grafik/c2/image-4.png"/>
<p>Gambar tersebut menampilkan Matriks Dissimilarity (Distance Matrix) yang dihasilkan melalui widget Distance Matrix pada Orange Data Mining. matriks ini berbentuk segitiga (single mode) yang memuat data jarak antar n titik data. Struktur matriks ini bersifat simetris, dimana jarak antara objek i ke objek j sama dengan jarak objek j ke objek i atau d(i,j) = d(j,i), dan memiliki nilai diagonal nol yang menunjukkan jarak objek terhadap dirinya sendiri. nilai dissimilarity dalam matriks ini merupakan ukuran numerik dari perbedaan dua objek data. Interpretasi nilai jarak mengikuti prinsip dimana nilai yang sangat rendah menunjukkan benda yang lebih mirip, sedangkan nilai yang tinggi menunjukkan perbedaan yang besar. Hal ini terlihat jelas pada data pelanggan dalam matriks. Sebagai contoh, jarak antara customer 7590-VHVEG dan 5575-GNVDE adalah 2,074, yang menunjukkan tingkat perbedaan sedang. Namun, customer 7590-VHVEG memiliki nilai jarak yang lebih kecil yaitu 0,554 terhadap customer 3668-QPYBK, yang mengindikasikan bahwa kedua customer tersebut memiliki karakteristik yang sangat mirip.
Sebaliknya, perbedaan yang signifikan terlihat pada pasangan customer 8091-TTVAX dan 3668-QPYBK yang memiliki nilai jarak sebesar 4,519. Nilai yang besar ini menandakan bahwa kedua objek tersebut sangat berbeda secara karakteristik. Secara keseluruhan, matriks ini memenuhi sifat-sifat jarak yaitu positive definiteness (nilai > 0 untuk objek berbeda), symmetry, dan triangle inequality. Hasil matriks dissimilarity ini menjadi dasar utama untuk tahapan selanjutnya yaitu Hierarchical Clustering dalam mengelompokkan pelanggan berdasarkan kemiripan karakteristiknya.</p>

![Grafik](grafik/c2/image-5.png"/>
![Grafik](grafik/c2/image-6.png"/>

---
<p>Berdasarkan dendrogram, hierarchical 
clustering dilakukan dengan metode linkage Ward dan 
menghasilkan 4 cluster optimal. Pemotongan dendrogram 
dilakukan pada ketinggian tertentu sehingga diperoleh:

Cluster 1: sejumlah X customer,
Cluster 2: sejumlah X customer,
Cluster 3: sejumlah X customer,
Cluster 4: sejumlah X customer,

Metode Ward linkage dipilih karena mampu menghasilkan 
cluster yang lebih kompak dengan meminimalkan varians 
dalam setiap cluster.</p>

---
## implementasikan data iris untuk mengukur jara di orange
![Grafik](grafik/c2/image-7.png)

<p>gambar diatas merupakan sebagian data mentah dari iris untuk diimplementasikan dalam menghitung jarak</p><br>

---
![Grafik](grafik/c2/image-8.png)
<p>gambar di atas merupakan hasil dari menghitung jarak pada data iris dimana prosesnya sama dengan yang tadi </p>

---
![alt text](image-9.png)
![Grafik](grafik/c2/image-9.png)
<p>gambar di atas merupakan visualiasi pengukuran jarak pada orange, tetapi sementara saya menggunakan widget csv file impor untuk mengimpor data iris bukan menggunakan sql table karena widget tersebut masih ada erornya atau tidak bisa di pakai dan belum menemukan solusinya</p>

---