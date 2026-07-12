# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : Kurangnya evaluasi empiris mengenai kinerja arsitektur basis data hibrida (Polyglot Persistence) dibandingkan dengan sistem basis data tunggal (monolitik) pada lingkungan cloud-native.

Research Question:
  Tipe         : [x] Comparison  [ ] Improvement  [ ] Exploratory
  Formulasi    : Apakah implementasi arsitektur basis data hibrida (MySQL + MongoDB) menghasilkan waktu respon (latency) yang lebih rendah dibandingkan arsitektur basis data monolitik (MySQL saja) pada lingkungan cloud-native?
  Variabel IV  : Tipe arsitektur basis data (Hibrida vs Monolitik) 
  Variabel DV  : Waktu respon (latency) dan throughput
  Metrik       : Average response time (ms) dan Requests Per Second (RPS) 
  Dataset      : Dataset transaksi e-commerce (misal: TPC-C benchmark) 
  Baseline     : Arsitektur monolitik (MySQL) 

Quality Check RQ:
  [x] Variabel spesifik
  [x] Metrik jelas
  [x] Baseline ada
  [x] Konteks disebutkan
  [x] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : ukti empiris mengenai efisiensi operasional dari penggunaan Polyglot Persistence pada beban kerja e-commerce di lingkungan cloud.
  Jenis kontribusi        : [ ] Improvement  [x] Comparison  [ ] Novel approach
  Gap yang diisi          : Mengisi celah penelitian yang sebelumnya hanya membandingkan performa database secara terisolasi

Hypothesis Pair:
  H₀ : Tidak ada perbedaan signifikan pada average response time antara arsitektur hibrida dan monolitik pada beban kerja yang sama.
  H₁ : Arsitektur hibrida memiliki average response time yang lebih rendah secara signifikan dibandingkan arsitektur monolitik.
  Threshold              :  p < 0.05$ (uji statistik t-test atau Mann-Whitney).
  Justifikasi threshold  : Standar umum dalam signifikansi statistik untuk menolak hipotesis nol.
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:** Kurangnya evaluasi empiris arsitektur hibrida (SQL+NoSQL) pada lingkungan cloud-native

**RQ versi pertama (tulis bebas):**
> Apakah menggabungkan MySQL dan MongoDB lebih baik untuk e-commerce daripada pakai satu saja?

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik |ya|Hibrida vs Monolitik|
| Metrik terukur |tidak|"Lebih baik" terlalu ambigu|
| Baseline |ya|MySQL (Monolitik)|
| Dataset/konteks |ya|E-commerce|

**Tipe RQ:** [x] Comparison / [ ] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> Apakah implementasi arsitektur basis data hibrida (MySQL + MongoDB) menghasilkan waktu respon yang lebih rendah dibandingkan arsitektur basis data monolitik (MySQL) pada dataset transaksi e-commerce di lingkungan cloud?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ | Tidak ada perbedaan latency signifikan antara arsitektur hibrida dan monolitik pada sistem e-commerce |
| H₁ | Arsitektur hibrida menunjukkan latency yang lebih rendah secara signifikan dibandingkan monolitik |
| Metrik | Average response time dalam milidetik (ms) |
| Threshold | p<0.05 |
| Justifikasi threshold | Standar alpha untuk pengujian hipotesis |

**Apakah hipotesis ini falsifiable?** [x] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? Jika data hasil eksperimen menunjukkan hasil statistik p> 0.05$ atau rata-rata latency hibrida lebih tinggi daripada monolitik, maka H₁ ditolak

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ | Apakah arsitektur hibrida menghasilkan latency yang lebih rendah dari monolitik pada e-commerce? |
| Variable (IV) | Tipe arsitektur (Hibrida: SQL+NoSQL, Monolitik: SQL) |
| Variable (DV) | Latency (Waktu respon dalam ms) |
| Metric | Mean latency & Confidence Interval 95% |
| Data source | Dataset transaksi e-commerce (TPC-C) |
| Analysis method | Independent t-test untuk menguji perbedaan rata-rata |

**Apakah rantai lengkap?** [x] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi? ______________

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Studi Performa Basis Data SQL dan NoSQL dalam Menangani Transaksi Data Skala Besar
**RQ yang diekstrak:** Apakah arsitektur hibrida memberikan performa yang lebih baik dibanding monolitik pada aplikasi cloud?
**Komponen yang hilang:** Metrik yang spesifik (misal: berapa ms latency), dataset spesifik, dan nilai ambang batas signifikansi statistik.
