# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## Template A.13 — Preprocessing Documentation Log

```
PREPROCESSING LOG

Dataset: Data Performa Komparatif Basis Data (SQL vs NoSQL) dari 5 Jurnal Bereputasi (2022-2026).
Jumlah data awal: 5 Data Points (Representasi dari 5 studi literatur).

Cleaning:
| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing | 1 metrik (Std Dev) | Imputation (Mean dari sampel lain) | Mempertahankan kelengkapan untuk visualisasi error bar |
| Duplikat| 0 | - | Data sudah terverifikasi unik dari tiap paper |
| Error   | 2 unit metrik (ops/s vs RPS) | Standardisasi ke RPS | Menyamakan satuan ukur untuk validitas perbandingan |

Transformation:
| Transformasi | Variabel | Detail | Alasan |
|-------------|----------|--------|--------|
| Konversi Unit | Throughput | Ops/s ke RPS| Menyeragamkan unit ke standar industri (Requests Per Second) |
| Normalisasi Basis | Latency | Normalisasi ke ms | Menghilangkan bias perbedaan spesifikasi hardware tiap studi |

Normalization:
  Metode    : ____________________
  Alasan    : ____________________
  Parameter : (dihitung dari: training set / seluruh data)

Leakage Check:
  [x] Parameter normalisasi konsisten untuk semua data.
  [x] Tidak ada informasi "bocor" karena data diambil dari output akhir paper (bukan data mentah/privat).
  [x] Sintesis dilakukan setelah kriteria inklusi terpenuhi secara ketat.

Jumlah data akhir : 5 titik data terstandarisasi
Script tersedia   : [x] Ya → path: synthesis_matrix_final.xlsx | [ ] Belum
```

---

## Latihan 1 — Cleaning Plan

Periksa dataset Anda (atau dataset contoh) dan dokumentasikan masalah yang ditemukan.

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing Std Dev | 1 paper | Imputation (Mean dari 4 paper lainnya) | Data penting untuk error bar |
| Unit Inconsistency | 2 paper | Konversi unit (ops/s → RPS) | Menyamakan skala untuk perbandingan |
| Outlier (Hardware) | 1 paper | Winsorization (Cap nilai ekstrem) | Mencegah distorsi hasil rata-rata |

**Jumlah data sebelum cleaning:** 5 paper
**Jumlah data setelah cleaning:** 5 paper
**Persentase data yang hilang/berubah:** 40%

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel | Range Asli | Distribusi | Outlier? | Metode Normalisasi | Alasan |
|----------|-----------|-----------|----------|-------------------|--------|
| Latency | 10 -150 ms | right-skewed | ya | robust scaling | Menjaga stabilitas dari outlier hardware |
| Throughput | 500 – 5000 RPS | Normal | tidak | Min-Max Scaling | Menyamakan skala ke [0,1] untuk perbandingan |

**Apakah normalisasi diperlukan?** [x] Ya / [ ] Tidak
**Justifikasi:**
> Normalisasi diperlukan untuk menghilangkan bias akibat perbedaan spesifikasi server yang digunakan antar-peneliti di setiap paper agar data bersifat komparabel.

**Leakage check:**
- [ ] Parameter dihitung dari training set saja
- [ ] Normalisasi diterapkan setelah train-test split

---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY

1. Dataset: Matriks perbandingan MySQL & MongoDB dari literatur 2022-2026.
2. Data awal: 5 paper, 2 metrik utama.
3. Cleaning: Standardisasi satuan throughput menjadi RPS untuk semua entri.
4. Transformation: Normalisasi latency berdasarkan waktu respon query standar.
5. Normalisasi: Min-Max scaling relatif terhadap rata-rata literatur.
6. Data akhir: 5 titik data terstandarisasi yang siap di-visualisasi.
7. Leakage check: [x] Lulus(metodologi sintesis objektif)
```

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

> Ya, dulu saya sering menormalisasi semua data ke [0,1] padahal untuk metrik performa seperti latency, nilai aslinya justru lebih informatif bagi pembaca.
> Risiko utamanya adalah menghilangkan konteks asli data. Jika kita terlalu banyak melakukan transformasi, angka yang dihasilkan menjadi abstrak dan sulit diinterpretasikan secara praktis oleh praktisi yang membaca jurnal kita.
