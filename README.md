#  UTS Data Mining — Prediksi Kualitas Wine
**Nama:** CYNTHIA PUTRI ANAS RAMADHANI 
**NIM:** 2304020189  
**Mata Kuliah:** Data Mining  

---

## 📌 Deskripsi Proyek
Proyek ini bertujuan membangun model klasifikasi untuk memprediksi 
kualitas wine berdasarkan fitur-fitur kimiawi menggunakan algoritma 
**Random Forest Classifier**.

---

## 📂 Dataset
| File | Keterangan |
|------|-----------|
| `data_training.csv` | 857 data dengan 11 fitur kimia + kolom `quality` |
| `data_testing.csv`  | 286 data dengan 11 fitur kimia (tanpa `quality`) |

**Fitur yang digunakan:**
fixed acidity, volatile acidity, citric acid, residual sugar, 
chlorides, free sulfur dioxide, total sulfur dioxide, density, 
pH, sulphates, alcohol

---

## 🔍 Tahapan Analisis

### 1. Eksplorasi Data (EDA)
- Dataset training memiliki **857 baris dan 13 kolom**
- Dataset testing memiliki **286 baris dan 12 kolom**
- **Tidak ditemukan missing value** pada kedua dataset
- Kualitas wine berkisar antara **3 hingga 8**

### 2. Visualisasi Data

**📊 Distribusi Kualitas Wine**  
Kelas 5 dan 6 mendominasi dataset (±84% dari total data), 
sedangkan kelas 3 dan 8 sangat sedikit. Kondisi ini disebut 
*class imbalance* yang dapat mempengaruhi performa model pada 
kelas minoritas.

**🔥 Heatmap Korelasi**  
- `alcohol` memiliki korelasi **positif tertinggi** dengan quality
- `volatile acidity` memiliki korelasi **negatif** dengan quality  
- `density` dan `fixed acidity` saling berkorelasi tinggi 
  (multikolinearitas), namun Random Forest tahan terhadap hal ini

**📦 Boxplot Fitur**  
- Wine berkualitas tinggi (7–8) cenderung memiliki kadar `alcohol` 
  lebih tinggi
- Wine berkualitas rendah (3–4) memiliki `volatile acidity` lebih 
  tinggi dengan banyak outlier

### 3. Data Cleaning
- ✅ Tidak ada missing value
- ✅ Tidak ada data duplikat
- Data langsung siap digunakan untuk modeling

### 4. Pemodelan — Random Forest Classifier

**Alasan memilih Random Forest:**
- Robust terhadap outlier dan data tidak normal
- Tidak memerlukan feature scaling/normalisasi
- Memberikan *feature importance* untuk interpretasi
- Akurasi tinggi karena menggabungkan banyak pohon (ensemble)

**Parameter model:**
```python
RandomForestClassifier(n_estimators=200, random_state=42)
```

### 5. Evaluasi Model
| Metrik | Nilai |
|--------|-------|
| Accuracy | ~60% |
| Weighted F1-Score | ~0.58 |

**Interpretasi:**
- Model paling akurat memprediksi kelas **5 dan 6** karena 
  jumlah datanya dominan
- Kelas **3 dan 8** sulit diprediksi karena sampelnya sangat sedikit
- Fitur **alcohol** adalah yang paling berpengaruh terhadap 
  kualitas wine (importance tertinggi)

### 6. Hasil Prediksi
File output: `hasilprediksi_189.csv`  
Berisi **286 prediksi** kualitas wine untuk data testing.

---

## 💡 Kesimpulan
Random Forest berhasil memprediksi kualitas wine dengan akurasi ~60%. 
Performa model dipengaruhi oleh *class imbalance* pada dataset. 
Fitur `alcohol` terbukti menjadi prediktor terkuat kualitas wine.

**Saran pengembangan:**
- Gunakan SMOTE untuk menangani class imbalance
- Coba hyperparameter tuning dengan GridSearchCV
- Bandingkan dengan XGBoost atau Gradient Boosting

---

## 📁 Struktur File
```
├── UTS_DataMining_PrediksiKualitasWine.ipynb
├── data_training.csv
├── data_testing.csv
├── hasilprediksi_189.csv
└── README.md
```
