# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question: Sejauh mana perbedaan performa latency dan throughput antara SQL dan NoSQL dalam menangani transaksi data skala besar?
Metrik Utama: Latency (ms) dan Throughput (RPS)

Tabel Hasil(Sintesis Literatur):
| DBMS | Avg Latency (ms) |Avg Throughput (RPS) | Dataset Size | Referensi (Paper) |
|----------|----------------------|----------------------|----------|----------------|
| MySQL | 45.2 ± 5.2 | 1.2k ± 0.2k | 100k - 1jt | P1, P2 |
| MongoDB | 38.5 ± 4.1 | 2.5k ± 0.5k | 100k - 1jt | P1, P3, P4 |

Visualisasi yang Direncanakan:
| # | Jenis Grafik | Pesan Utama | Metrik |
|---|-------------|-------------|--------|
| 1 | Grouped Bar Chart | MongoDB unggul di throughput pada large scale | Throughput |
| 2 | Box Plot (Sintesis) | MySQL memiliki stabilitas latency yang lebih konsisten | Latency |
| 3 | Trade-off Scatter | NoSQL untuk Write-Heavy, SQL untuk Complex Read | Latency vs RPS |

Bias Check:
  [x] Y-axis mulai dari 0 (untuk menghindari kesan "jauh lebih unggul" yang semu).
  [x] Error bar ditampilkan (menggambarkan rentang dari 5 paper berbeda).
  [x] Semua data disertakan (tidak cherry-picking paper yang memenangkan satu vendor).
  [x] Tidak menggunakan 3D (tetap 2D agar data mudah dibaca).
```

---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| DBMS | Metrik Latency (ms) | Metrik Throughput (RPS) | Paper Sumber |
|----------|----------------------|----------------------|-------------|
| MySQL | 42.0 ± 8.5 | 1.5k ± 0.3k | P1, P2, P5 |
| MongoDB | 35.5 ± 7.2 | 2.8k ± 0.7k | P1, P3, P4 |

**Checklist tabel:**
- [ ] Self-contained (judul jelas, satuan ada, N tercantum)
- [ ] Mean ± std (bukan single number)
- [ ] Diurutkan berdasarkan metrik utama
- [ ] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|-------------|-------|---------------------|
| 1 | Grouped Bar Chart | Perbandingan Throughput MySQL vs MongoDB | Nilai Mean RPS |
| 2 | Error Bar Plot | Rentang variasi Latency antar literatur | Mean ± Std Dev |
| 3 | Radar Chart | Trade-off fitur (Read vs Write vs Scalability) | Skor kualitatif (1-5) |

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah Y-axis menyesatkan? | Tidak, kami menetapkan Y-axis dari 0 agar perbedaan performa terlihat proporsional (tidak manipulatif) |
| Apakah error bar ditampilkan? | Ya, ini krusial untuk menunjukkan bahwa data berasal dari 5 paper yang berbeda (variabilitas antar paper)|
| Apa solusinya jika data dari paper tidak mencantumkan Std Dev? | Kami akan menggunakan rentang minimum dan maksimum dari paper tersebut sebagai batas error bar |

**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [ ] Semua bias check lulus
- [ ] Ada yang perlu diperbaiki: ____

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> Mengapa tabel dan grafik keduanya diperlukan dalam SLR?
Tabel diperlukan agar pembaca dapat melakukan verifikasi data mentah dari setiap paper yang disintesis (presisi). Grafik diperlukan agar pembaca bisa langsung menangkap "benang merah" dari riset yang kita lakukan tanpa harus membaca angka satu per satu.
> Pernahkah Anda membuat grafik yang menyesatkan?
Seringkali grafik dibuat tanpa menyertakan referensi (N), sehingga pembaca mengira angka tersebut adalah hasil riset penulis sendiri, padahal itu hasil sintesis dari paper lain. Hal ini bisa menyesatkan secara etik.
