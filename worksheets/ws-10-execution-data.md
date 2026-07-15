# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario (paper) | Seed (iterasi) | Parameter(metriks/fokus) | Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1     | paper 1 | 1 | Latency, Throughput | Planned | 10 Min | Extract_P1.json |
| 2     | paper 2 | 1 | Latency, Throughput | Planned | 10 Min | Extract_P2.json |
| 3     | paper 3 | 1 | Latency, Throughput | Planned | 10 Min | Extract_P3.json |
| 4     | paper 4 | 1 | Latency, Throughput | Planned | 10 Min | Extract_P4.json |
| 5     | paper 5 | 1 | Latency, Throughput | Planned | 10 Min | Extract_P5.json|

Jumlah runs per skenario : 1 (Ekstraksi data kualitatif/kuantitatif dari dokumen)
Total runs               : 5 paper

DATA LOG (per run):
  Run ID    : E-P1 (Ekstraksi Paper 1)
  Timestamp : 2026-07-12
  Skenario  : analisis performa database
  Input     : pdf paper 1
  Output    : Data Latency 42ms, Throughput 1.5k RPS
  Anomali   : tidak ada
  Catatan   : Paper menggunakan benchmark YCSB, metrik sesuai kriteria inklusi.
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.
**Total skenario:** 2 (perbandingan SQL & NoSQL)
**Run per skenario:** Run per skenario: 5 paper yang ditinjau
**Total run keseluruhan:**  2 (perbandingan SQL & NoSQL

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field | Contoh |
|-------|--------|
| Run ID | E-P1 |
| Timestamp | 2026-07-12 |


**Konfigurasi:**
| Field | Contoh |
|-------|--------|
| papertahun | 2022-2026 |
| database | MYSL/MongoDB |


**Hasil:**
| Metrik | Tipe Data | Range Valid |
|--------|----------|-------------|
| Latency | float | 0-500 ms |
| Throughput | float | 0-10.0k RPS |


**Format output:** [ ] CSV / [x] JSON / [ ] Database / [ ] Lainnya: ____

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| data hilang | paper tidk mencantumkan SD/mean | Dokumentasikan sebagai Missing Data atau hubungi penulis via email |
| Metrik Berbeda | Metrik Berbeda | Lakukan konversi (Normalisasi) ke satuan standar (ms/RPS) |
| Bias Penulis | Hasil "terlalu bagus" dari paper vendor | Beri catatan kritis di pembahasan (Threats to Validity) |

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Selama ini saya sering menyimpulkan performa hanya dari satu artikel tanpa mempertimbangkan variabilitas dari paper lain, yang berisiko membuat kesimpulan saya sangat bias terhadap metode penulis tersebut.
**Yang akan dilakukan berbeda:**
> Saya akan memastikan setiap data yang saya ambil berasal dari minimal 5 paper yang berbeda untuk mendapatkan Mean dan Standard Deviation (sintesis), serta mencatat anomali data (seperti perbedaan metodologi benchmark) agar pembaca mengetahui batasan riset saya.
