# WS-14: Analysis, Interpretation & Failure Analysis

> **Bab 14 — Analisis Data, Interpretasi & Failure Analysis**

---

## Ringkasan Materi

### Data → Knowledge Model

```
Data → Analysis → Interpretation → Explanation → Knowledge
```

Tiga level yang berbeda:
- **Analysis** — "Apa yang terjadi?" (deskriptif + inferensial)
- **Interpretation** — "Apa artinya?" (konteks RQ + literatur)
- **Failure Analysis** — "Mengapa tidak berhasil?" (boundary conditions)

### Beyond p-value

**Statistical significance ≠ practical significance.** Selalu laporkan:
1. p-value (signifikansi statistik)
2. Effect size (besarnya efek)
3. Confidence interval (rentang ketidakpastian)

| Effect Size (Cohen's d) | Interpretasi |
|-------------------------|-------------|
| < 0.2 | Small |
| 0.2 – 0.8 | Medium |
| > 0.8 | Large |

### Pemilihan Uji Statistik

| Kondisi | Uji yang Tepat |
|---------|---------------|
| 2 grup, normal, paired | Paired t-test |
| 2 grup, non-normal | Wilcoxon signed-rank |
| > 2 grup, normal | One-way ANOVA + post-hoc |
| > 2 grup, non-normal | Kruskal-Wallis + post-hoc |
| 2 variabel kontinu | Pearson (normal) / Spearman (rank) |

### Failure Analysis as Contribution

Hipotesis yang ditolak adalah **temuan yang berharga**:

| Dataset | New (F1) | Baseline (F1) | p-value | Cohen's d |
|---------|---------|--------------|---------|-----------|
| DS-1 (small, clean) | 94.2±1.1 | 89.3±1.5 | <0.001 | **3.7** |
| DS-4 (medium, noisy) | 78.3±3.2 | 82.1±2.8 | 0.008 | **-1.3** |
| DS-5 (large, noisy) | 71.6±4.1 | 80.5±3.0 | <0.001 | **-2.5** |

**Insight:** Metode baru unggul di data bersih tapi gagal di data noisy → asumsi Gaussian dilanggar → **boundary condition** ditemukan → hybrid approach direkomendasikan.

**Partial failure + deep analysis = kontribusi lebih kaya daripada full success tanpa analisis.**

### Limitation Types

| Jenis | Contoh |
|-------|--------|
| Internal validity | Confounders yang tidak dikontrol |
| External validity | Generalisasi ke domain lain |
| Construct validity | Metrik mengukur apa yang dimaksud? |
| Statistical limitation | Sample size, asumsi distribusi |

### Jebakan Kognitif

1. "Signifikan statistik = penting secara praktis" → cek effect size
2. "Hipotesis tidak didukung → cari sudut baru" → p-hacking
3. "Kegagalan tidak perlu dilaporkan detail" → missed insight
4. "Limitasi cukup disebutkan, tidak perlu dianalisis" → kedalaman hilang

---

## Template A.14 — Analysis & Interpretation Report

```
ANALYSIS & INTERPRETATION

1. Statistik Deskriptif:
   | Skenario | Mean | Std | Median | Min | Max | n |
   |----------|------|-----|--------|-----|-----|---|
   | MySQL | 42.0 | 8.5 |40.5 | 35.0| 55.0| 5 |
   | MongoDB | 35.5 |7.2 | 34.0 | 28.0  | 45.0 | 5 |

2. Uji Hipotesis:
   Uji yang digunakan  : Welch’s t-test
   Justifikasi          : Varians tidak sama antar studi literatur
   Hasil: p = 0.042 (Signifikan), effect size (d/r/η²) = 0.82 (Large Effect)
   CI 95%               : [0.8, 12.2] ms

3. Keputusan:
   [x] H₀ ditolak → H₁ diterima
   [ ] H₀ tidak ditolak

4. Interpretasi:
   Hubungan ke RQ       : MongoDB secara empiris memberikan latency yang lebih rendah pada sistem cloud-native.
   Practical significance: Perbedaan ~6.5ms mungkin terlihat kecil, namun pada skala jutaan transaksi per detik, hal ini berdampak besar pada pengalaman pengguna.
   Perbandingan literatur: Hasil ini mengonfirmasi temuan Saputra (2024) mengenai efisiensi MongoDB pada write-heavy workload.

5. Limitation:
   | Jenis | Ancaman | Dampak | Mitigasi |
   |-------|---------|--------|----------|
   | External Validity | Variasi Hardware | Performa tidak mutlak | Normalisasi per-skenario |
   | Construct Validity | Definisi "Latency" | Inkonsistensi data | Standarisasi metrik respon |

6. Failure Analysis (jika H₀ tidak ditolak):
   Penyebab potensial  : Penggunaan index yang salah pada MongoDB di paper P2.
   Boundary condition   : MySQL tetap unggul saat melakukan JOIN tabel yang sangat kompleks (data relasional).
   Insight              : Pemilihan basis data tidak boleh hanya berdasar performa mentah, tetapi juga struktur data yang akan dikelola.
```

---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan | Jawaban |
|-----------|---------|
| Berapa grup yang dibandingkan? | 2 (SQL vs NoSQL) |
| Apakah data berpasangan (paired)? | Tidak (studi independen) |
| Apakah distribusi normal? (uji normalitas) | Diasumsikan normal (untuk sampel literatur) |
| **Uji yang dipilih:** | Independent Samples t-test |
| **Justifikasi:** | Membandingkan dua rata-rata dari populasi berbeda |

**Effect size yang akan dilaporkan:** [x] Cohen's d / [ ] Eta-squared / [ ] Lainnya: ____

---

## Latihan 2 — Interpretasi Hasil

Gunakan data berikut (atau data riil Anda) untuk berlatih interpretasi.

**Data:**
| Model | Accuracy (mean ± std) | n |
|-------|----------------------|---|
| A | 89.2 ± 1.5 | 10 |
| B | 87.8 ± 2.1 | 10 |

p = 0.045, Cohen's d = 0.74, CI 95% = [0.03, 2.77]

| Aspek | Interpretasi |
|-------|-------------|
| Signifikansi statistik | p < 0.05 (signifikan secara statistik) |
| Effect size | d=0.82 (dampak performa cukup besar) |
| Practical significance | Sangat krusial untuk optimasi sistem high-traffic |
| Hubungan ke RQ | MongoDB lebih efisien untuk cloud-native workload |
| Perbandingan literatur | Mendukung temuan Saputra (2024) |

---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

**Skenario:** Metode baru Anda mendapat F1 = 83.2%, baseline = 84.7%. p = 0.12 (tidak signifikan).

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah ini "gagal"? | Tidak, hasil kontradiktif (MySQL unggul di complex query) adalah temuan penting (Boundary Condition) |
| Insight | SQL tidak "kalah", melainkan memiliki domain aplikasi yang berbeda (Relational vs Non-Relational). |
| Apakah layak dilaporkan? Mengapa? | Sangat layak, agar pembaca jurnal Anda tidak salah memilih teknologi untuk sistem JOIN-berat. |

**Limitation terkait:**
| Jenis | Ancaman | Dampak |
|-------|---------|--------|
| *Contoh: Statistical* | *Contoh: Hanya 5 run per skenario* | *Power test rendah* |
| | | |
| | | |

---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

> Kegagalan hipotesis (saat NoSQL tidak selalu lebih cepat dari SQL) adalah kontribusi terbesar. Hal ini mencegah peneliti lain melakukan kesalahan pemilihan teknologi (misalnya: menggunakan NoSQL untuk Accounting System yang butuh ACID transaction ketat).
> ___________________________________________________
