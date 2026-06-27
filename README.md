---

# 🛒 Analisis Pola Penjualan Supermarket di Myanmar
### Pendekatan Korelasi, Time Series, dan Regresi Panel Data

> **Mata Kuliah:** SD211123 – Analisis Data Eksploratif
> **Program Studi:** Sains Data, Fakultas Ilmu Komputer
> **Universitas:** Universitas Pembangunan Nasional Veteran Jawa Timur
> **Tahun:** 2025

---

## 👥 Tim Peneliti — Kelompok CIPCUP

| Nama | NPM |
|------|-----|
| Olivia Natasya Yuniar | 24083010012 |
| Zelga Rahma Salsa Aziza | 24083010015 |
| Lila Fifa Ardani | 24083010025 |
| Eris Alfionita | 24083010032 |

**Dosen Pengampu:**
- Shindi Shella May Wara, M.Stat.
- Amri Muhaimin, S.Stat., M.Stat., M.S.

---

## 📌 Deskripsi Proyek

Proyek ini menganalisis pola penjualan supermarket di Myanmar menggunakan **Supermarket Sales Dataset** periode **Januari–Maret 2019** yang bersumber dari [Kaggle](https://www.kaggle.com/datasets/faresashraf1001/supermarket-sales). Dataset mencakup **1.000 transaksi** dari tiga cabang supermarket di tiga kota (Yangon, Mandalay, Naypyitaw).

Analisis dilakukan melalui tiga pendekatan utama:
1. **Analisis Korelasi** — mengukur kekuatan hubungan antar variabel
2. **Regresi Data Panel** — mengestimasi pengaruh variabel independen terhadap gross income
3. **Analisis Deret Waktu (Time Series)** — memodelkan dan meramalkan pola penjualan harian

---

## 📁 Struktur Repository

```
├── EDA_PROJECT_ANALISIS_KORELASI.ipynb        # Analisis korelasi (revisi)
├── PROJECT_KORELASI.ipynb                     # Analisis korelasi awal
├── analisis-time-series.ipynb                 # ARIMA, GRU, dan LSTM forecasting
├── line_product_regresi_data_panel_eda.ipynb  # Regresi data panel
└── README.md
```

---

## 📊 Dataset

- **Sumber:** [Supermarket Sales – Kaggle](https://www.kaggle.com/datasets/faresashraf1001/supermarket-sales)
- **Periode:** Januari – Maret 2019
- **Jumlah data:** 1.000 baris transaksi
- **Cabang:** A (Yangon), B (Mandalay), C (Naypyitaw)

| Variabel | Tipe | Keterangan |
|----------|------|------------|
| Branch / City | Nominal | Cabang dan kota supermarket |
| Customer Type | Nominal | Member / Normal |
| Gender | Nominal | Male / Female |
| Product Line | Nominal | 6 kategori produk |
| Payment | Nominal | Cash, E-wallet, Credit card |
| Unit Price | Rasio | Harga per unit produk |
| Quantity | Rasio | Jumlah barang yang dibeli |
| Tax 5% | Rasio | Pajak transaksi |
| Sales | Rasio | Total nilai penjualan |
| COGS | Rasio | Harga pokok penjualan |
| Gross Income | Rasio | Pendapatan kotor (**variabel dependen**) |
| Rating | Rasio | Kepuasan pelanggan (skala 1–10) |

---

## 🔍 Metodologi

### 1. Analisis Korelasi

- Uji Normalitas Shapiro-Wilk → semua variabel **tidak normal** (p < 0.05), sehingga digunakan metode non-parametrik
- **Spearman** untuk variabel numerik: Sales, Tax 5%, COGS, Gross Income berkorelasi sempurna (r = 1.00); Quantity kuat (r = 0.74); Unit Price sedang (r = 0.63); Rating sangat lemah (r ≈ -0.02)
- **Point-Biserial** untuk variabel biner: Gender signifikan namun sangat lemah (r = -0.084); Customer Type tidak signifikan
- **ETA** untuk variabel nominal ≥3 kategori: City, Branch, Payment, Product Line semua η² < 0.01

### 2. Regresi Data Panel

| Uji | Statistik | p-value | Keputusan |
|-----|-----------|---------|-----------|
| Uji Chow | F = 19.78 | < 0.001 | Fixed Effect lebih baik dari Pooled OLS |
| Uji Hausman | χ² = 2.96 | 0.565 | **Random Effect lebih baik dari Fixed Effect** |

**Model terpilih: Random Effect Model (REM)**

```
Ŷ = -15.888 + 2.8014 * Quantity + 0.2820 * Unit Price
```

| Metrik | Nilai |
|--------|-------|
| Overall R² | **88.65%** |
| Within R² | 88.68% |
| Between R² | 79.22% |

### 3. Analisis Deret Waktu

Preprocessing: uji ADF (stasioner pada mean), transformasi Box-Cox (λ = 0.36), differencing.

| Model | RMSE | MAE | MAPE |
|-------|------|-----|------|
| ARIMA(3,0,0) | 3,669 | 3,333.6 | 99.29% |
| GRU | 1,334.70 | 1,200.17 | 50.08% |
| **LSTM** | **1,294.75** | **1,170.34** | **48.69%** ✅ |

---

## 📈 Kesimpulan

1. Gross Income paling dipengaruhi oleh variabel transaksi numerik, bukan variabel kategorikal
2. Random Effect Model (R² = 88.65%) menunjukkan Quantity dan Unit Price berpengaruh positif signifikan
3. LSTM memberikan akurasi terbaik dibanding ARIMA dan GRU, namun semua model masih terbatas dalam menangkap fluktuasi harian yang tinggi

---

## 🛠️ Tools & Libraries

```python
pandas, numpy, scipy, statsmodels, matplotlib, seaborn,
scikit-learn, tensorflow/keras, linearmodels
```

---

## 🚀 Cara Menjalankan

```bash
# 1. Clone repo
git clone https://github.com/ErisAlfionita8/<nama-repo>.git

# 2. Install dependencies
pip install pandas numpy scipy statsmodels matplotlib seaborn scikit-learn tensorflow linearmodels

# 3. Download dataset dari Kaggle dan jalankan notebook sesuai urutan
```

---

<p align="center">Universitas Pembangunan Nasional Veteran Jawa Timur · Sains Data · 2025</p>

---
