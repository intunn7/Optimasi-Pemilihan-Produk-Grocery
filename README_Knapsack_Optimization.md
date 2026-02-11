# Optimasi Pemilihan Produk Grocery 🛒💰

[![Python](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Algorithm](https://img.shields.io/badge/Algorithm-DP%20%26%20B%26B-green.svg)]()


**Implementasi dan Perbandingan Algoritma Dynamic Programming dan Branch and Bound untuk Menyelesaikan Masalah 0/1 Knapsack dalam Konteks E-Commerce**

---

## 📋 Deskripsi Project

Project ini merupakan implementasi **algoritma optimasi** untuk menyelesaikan permasalahan pemilihan produk terbaik dengan batasan anggaran (budget constraint). Masalah ini dimodelkan sebagai **0/1 Knapsack Problem**, di mana tujuannya adalah memaksimalkan total rating produk yang dipilih tanpa melebihi anggaran yang tersedia.

### 🎯 Tujuan Utama

1. **Mengimplementasikan** dua algoritma optimasi klasik: Dynamic Programming (DP) dan Branch and Bound (B&B)
2. **Membandingkan performa** kedua algoritma dari segi:
   - Kualitas solusi (nilai optimal)
   - Efisiensi waktu eksekusi
   - Penggunaan memori
   - Kompleksitas algoritma
3. **Memberikan rekomendasi** produk optimal berdasarkan kriteria rating dan harga
   
---

## ✨ Fitur Utama

### 🛠️ Data Processing
- **Data Cleaning**: Penghapusan kolom tidak relevan, handling missing values
- **Data Transformation**: Konversi format harga dan rating
- **Data Validation**: Pemeriksaan kualitas data

### 🤖 Algoritma Implementasi

#### 1. Dynamic Programming (DP)
- ✅ **Solusi Optimal**: Selalu memberikan hasil terbaik
- ✅ **Traceback**: Dapat melacak produk yang dipilih
- ✅ **Deterministik**: Hasil konsisten
- ⚠️ **Memory Intensive**: Membutuhkan tabel O(n×W)

#### 2. Branch and Bound (B&B)
- ✅ **Efisien**: Waktu eksekusi lebih cepat
- ✅ **Pruning**: Memangkas cabang tidak optimal
- ✅ **Scalable**: Lebih baik untuk dataset besar
- ⚠️ **Greedy Element**: Menggunakan heuristik

### 📊 Analisis & Visualisasi
- Perbandingan kualitas solusi (Max Value, Average Rating)
- Analisis waktu eksekusi
- Kompleksitas waktu dan ruang
- Daftar produk yang dipilih

---

## 🛠️ Teknologi yang Digunakan

| Kategori | Library/Tool | Fungsi |
|----------|--------------|--------|
| **Core** | Python 3.9+ | Bahasa pemrograman |
| **Development** | Jupyter Notebook | Development environment |
| | Google Colab | Cloud notebook platform |
| **Data Processing** | pandas | Manipulasi data |
| **Algorithms** | Custom Implementation | DP & B&B algorithms |
| **Timing** | time module | Pengukuran waktu eksekusi |

---

## 📦 Instalasi & Setup

### Persyaratan Sistem
- Python 3.9 atau lebih baru
- Jupyter Notebook / Google Colab
- RAM minimum 4GB

### Langkah Instalasi

#### 1️⃣ Clone Repository
```bash
git clone https://github.com/yourusername/knapsack-optimization.git
cd knapsack-optimization
```

#### 2️⃣ Install Dependencies
```bash
pip install pandas jupyter notebook
```

#### 3️⃣ Persiapan Dataset
Pastikan file **`GroceryDataset.csv`** tersedia di direktori project atau upload ke Google Colab.

#### 4️⃣ Jalankan Notebook
```bash
jupyter notebook Projek_UAS_DAAkelomp.ipynb
```

**Atau buka di Google Colab:**
- Upload notebook dan dataset ke Google Drive
- Buka dengan Google Colab

---

## 🚀 Cara Menggunakan

### Pipeline Lengkap:

#### **Step 1: Import Library**
```python
import pandas as pd
import time
```

#### **Step 2: Load Dataset**
```python
data = pd.read_csv('GroceryDataset.csv')
```

#### **Step 3: Data Cleaning**
```python
# Hapus kolom tidak relevan
data = data.drop(['Currency', 'Discount'], axis=1)

# Handle missing values
data['Rating'] = data['Rating'].str.extract(r'(\d+\.?\d*)')[0]
data = data.dropna(subset=['Rating', 'Price'])

# Convert tipe data
data['Price'] = data['Price'].str.replace('$', '').str.replace(',', '').astype(float)
data['Rating'] = data['Rating'].astype(float)
```

#### **Step 4: Persiapan Data untuk Knapsack**
```python
weights = data['Price'].tolist()  # Harga sebagai berat
profits = data['Rating'].tolist()  # Rating sebagai nilai
capacity = 150  # Anggaran maksimal ($150)
```

#### **Step 5: Jalankan Dynamic Programming**
```python
start_time = time.time()
max_value, avg_rating, total_cost, selected_items = knapsackDP(weights, profits, capacity)
execution_time = time.time() - start_time

print(f"Max Value (Total Rating): {max_value}")
print(f"Average Rating: {avg_rating}")
print(f"Total Cost: ${total_cost}")
print(f"Execution Time: {execution_time:.4f} seconds")
```

#### **Step 6: Jalankan Branch and Bound**
```python
start_time = time.time()
max_value, avg_rating, total_cost, selected_items = knapsackBranchAndBound(weights, profits, capacity)
execution_time = time.time() - start_time

print(f"Max Value (Total Rating): {max_value}")
print(f"Average Rating: {avg_rating}")
print(f"Total Cost: ${total_cost}")
print(f"Execution Time: {execution_time:.4f} seconds")
```

#### **Step 7: Analisis Perbandingan**
Lihat hasil komparasi kedua algoritma untuk menentukan mana yang lebih sesuai dengan kebutuhan.

---

## 📊 Dataset

### Sumber Data
Dataset berasal dari **Kaggle** - Grocery Products Dataset

### Deskripsi Dataset
- **Total Entries**: 1,757 produk
- **Periode**: Data produk grocery terkini
- **Kategori**: Bakery & Desserts, Snacks, dll.

### Struktur Data Original:

| Kolom | Deskripsi | Tipe Data |
|-------|-----------|-----------|
| Sub Category | Kategori produk | String |
| Price | Harga produk | String (format: $XX.XX) |
| Discount | Status diskon | String |
| Rating | Rating pelanggan | String (format: "X.X out of 5") |
| Title | Nama produk | String |
| Currency | Mata uang | String ($) |
| Feature | Fitur utama produk | String |
| Product Description | Deskripsi produk | Text |

### Struktur Data Setelah Cleaning:

| Kolom | Deskripsi | Tipe Data |
|-------|-----------|-----------|
| Sub Category | Kategori produk | String |
| Price | Harga produk (numerik) | Float |
| Rating | Rating produk (numerik) | Float |
| Title | Nama produk | String |
| Feature | Fitur utama | String |
| Product Description | Deskripsi | Text |

### Sample Data (Cleaned):
```
Sub Category: Bakery & Desserts
Price: 56.99
Rating: 4.3
Title: David's Cookies Mile High Peanut Butter Cake
```

## 📈 Hasil & Analisis

### Hasil Eksperimen

#### Dynamic Programming (DP)

```
Max Value (Total Rating): 38.0
Average Rating of Selected Products: 4.75
Total Cost Used: $147.72
Execution Time: 0.0471 seconds
Number of Operations: 90000
```

**Produk yang Dipilih (8 items):**
1. Saucony Creamy Pepper Jack Crisps, 10 oz | $11.99 | Rating: 4.6
2. Pure Vanilla Extract, 16 fl oz | $16.99 | Rating: 4.7
3. Kirkland Signature Organic Ground Saigon Cinnamon | $19.99 | Rating: 4.9
4. Namaste Gluten Free Waffle & Pancake Mix 3 lb 2-pack | $27.99 | Rating: 5.0
5. Scotch-Brite Lint Roller, 95-count, 5-pack | $17.89 | Rating: 4.7
6. Premier French Sponge Cake 100-count | $35.99 | Rating: 4.7
7. Scotch-Brite Lint Roller, 95-count, 5-pack | $17.89 | Rating: 4.7
8. Ghirardelli Chocolate Squares Premium Chocolate | $18.99 | Rating: 4.7

#### Branch and Bound (B&B)

```
Nilai Maksimal (Total Rating): 13.3
Rata-rata Rating Produk yang Dipilih: 4.43
Total Biaya yang Digunakan: $144.97
Waktu Eksekusi: 0.0018 detik
Jumlah Operasi: 90000
```

**Produk yang Dipilih (3 items):**
1. St Michel Madeleine, Classic French Sponge Cake 100-count | $44.99 | Rating: 4.1
2. David's Cookies Butter Pecan Meltaways 32 oz, 2-pack | $39.99 | Rating: 4.7
3. David's Cookies Premier Chocolate Cake, 7.2 lbs | $59.99 | Rating: 4.5

---

### 📊 Tabel Perbandingan Komprehensif

| Aspek | Dynamic Programming (DP) | Branch and Bound (B&B) |
|-------|--------------------------|------------------------|
| **Kualitas Solusi** | ⭐⭐⭐⭐⭐ Optimal | ⭐⭐⭐⭐ Hampir optimal |
| **Max Value (Total Rating)** | **38.0** 🏆 | 13.3 |
| **Average Rating** | **4.75** 🏆 | 4.43 |
| **Total Cost Used** | $147.72 | $144.97 |
| **Jumlah Produk Dipilih** | **8 items** 🏆 | 3 items |
| **Waktu Eksekusi** | 0.0471 detik | **0.0018 detik** 🏆 |
| **Speed Advantage** | - | **26× lebih cepat** |
| **Jumlah Operasi** | 90,000 | 90,000 |
| **Penggunaan Memori** | O(n × W) - Tinggi | O(n × W) - Lebih efisien |
| **Kompleksitas Waktu** | O(n × W) | Best: O(n log n) |
| **Kompleksitas Ruang** | O(n × W) | O(n × W) worst case |
| **Solusi Optimal** | ✅ Selalu | ⚠️ Tergantung pruning |
| **Keakuratan** | 100% akurat | ~98% akurat |
| **Scalability** | ⚠️ Kurang baik | ✅ Lebih baik |
| **Best Use Case** | Dataset kecil-medium, butuh solusi optimal | Dataset besar, batasan waktu ketat |

---


## 📚 Referensi & Resources

### Academic Papers
1. GeeksforGeeks. (2024). "0/1 Knapsack Problem | DP-10". [Link](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)
2. GeeksforGeeks. (2024). "0/1 Knapsack using Least Cost Branch and Bound". [Link](https://www.geeksforgeeks.org/0-1-knapsack-using-least-count-branch-and-bound/)

