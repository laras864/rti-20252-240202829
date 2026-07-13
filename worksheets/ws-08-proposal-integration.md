# WS-08: Proposal Integration (UTS)

> **Bab 8 — Proposal & Checkpoint**

---

## Ringkasan Materi

### Proposal = Satu Argumen Utuh

Proposal riset bukan kumpulan bab yang independen. Ia adalah **satu argumen** yang mengalir dari masalah ke rencana solusi. Jika satu koneksi putus, seluruh proposal kehilangan koherensi.

### Integration Map — 6 Koneksi Kritis

```
Problem (Bab 2) → Gap (Bab 3) → RQ & H (Bab 4) → Metrik (Bab 5) → Sistem (Bab 6) → Eksperimen (Bab 7)
```

| Koneksi | Pertanyaan Verifikasi |
|---------|----------------------|
| Problem → Gap | Apakah gap muncul dari analisis literatur terhadap masalah? |
| Gap → RQ | Apakah RQ langsung menjawab gap yang teridentifikasi? |
| RQ → Metrik | Apakah setiap variabel di RQ punya metrik terdefinisi? |
| Metrik → Sistem | Apakah setiap metrik bisa diukur oleh komponen sistem? |
| Sistem → Eksperimen | Apakah desain eksperimen menggunakan sistem sebagai instrumen? |

### Koherensi Vertikal + Horizontal

- **Vertikal** — Alur logis atas-ke-bawah (problem → experiment). Setiap section menjawab pertanyaan yang diangkat section sebelumnya dan memunculkan pertanyaan baru.
- **Horizontal** — Konsistensi terminologi (nama variabel di RQ = di hipotesis = di metrik = di desain)

**Operasionalisasi Red Thread** (benang merah):
```
Bab 2 (Problem) → | memperkenalkan masalah X + evidensi |
                          ↓ menimbulkan pertanyaan: "apa akar gap-nya?"
Bab 3 (Gap)     → | menjawab pertanyaan tadi + membuka "lalu apa yang perlu diteliti?" |
                          ↓
Bab 4 (RQ/H)    → | menjawab gap dengan pertanyaan spesifik + prediksi terukur |
                          ↓
Bab 5-7 (Method)→ | menjawab RQ melalui desain eksperimen yang tepat |
```
Jika ada lompatan (section B tidak menjawab pertanyaan section A), red thread putus.

### Jebakan Kognitif

| Jebakan | Deskripsi |
|---------|----------|
| "Selling" Introduction | Menulis promosi, bukan menyajikan data dan gap |
| Copy-paste Methodology | Menyalin deskripsi tekstbook tanpa menyesuaikan ke RQ |
| Optimistic Timeline | Meremehkan waktu implementasi; selalu tambah buffer 30-50% |
| No Possibility of Failure | Mengimplikasikan hasil pasti sukses — proposal jujur mengakui H₀ mungkin tidak ditolak |

### Struktur Proposal

1. **Pendahuluan** — Latar belakang + problem statement (Bab 1-2)
2. **Tinjauan Pustaka** — Literature review + gap + baseline (Bab 3)
3. **RQ / Kontribusi / Hipotesis** — (Bab 4)
4. **Metodologi** — Metrik + sistem + desain eksperimen (Bab 5-7)
5. **Timeline & Output**

### Istilah Penting

- **Integration Map** — Diagram 6 koneksi kritis antar komponen proposal
- **Vertical Coherence** — Alur logis atas-ke-bawah
- **Horizontal Coherence** — Konsistensi terminologi di semua bagian
- **Checkpoint** — Titik self-assessment sebelum transisi dari desain ke eksekusi

---

## Template A.8 — Integration Checklist

```
PROPOSAL INTEGRATION CHECKLIST

Koneksi Vertikal (Flow Atas-Bawah):
  [x] Problem → Gap: masalah bottleneck data skala besar terdokumentasi di 5 jurnal.
  [x] Gap → RQ: RQ langsung menjawab celah evaluasi empiris arsitektur SQL vs NoSQL.
  [x] RQ → Hypothesis: Hipotesis memprediksi keunggulan throughput NoSQL vs latency SQL.
  [x] Hypothesis → Metric: atency (ms) dan Throughput (RPS) mengukur variabel dalam hipotesis.
  [x] Metric → System: Performance monitor K6 menangkap metrik tersebut saat eksperimen.
  [x] System → Experiment: Desain eksperimen menggunakan Docker sebagai instrumen pengjian.

Koneksi Horizontal (Konsistensi):
  [x] Istilah sama di semua bagian
  [x] Variabel di RQ = variabel di hipotesis = metrik di desain
  [x] Scope tidak berubah dari masalah ke eksperimen

Cognitive Trap Checklist:
  [x] Tidak ada paragraf "promosi" di pendahuluan (hanya data & gap)
  [x] Metodologi disesuaikan ke RQ, bukan copy-paste textbook
  [x] Timeline sudah ditambah buffer 30-50% dari estimasi awal
  [x] Proposal mengakui kemungkinan H0 tidak ditolak (honest uncertainty)
  [x] Tidak ada klaim "pasti berhasil" atau "meningkatkan signifikan"

Rubrik Self-Assessment:
| Kriteria     | 1 (Lemah)                                        | 2 (Cukup)                                     | 3 (Baik)                                           | Skor |
|------------- |--------------------------------------------------|-----------------------------------------------|----------------------------------------------------|------|
| Koherensi    | >2 koneksi vertikal terputus                     | 1-2 koneksi lemah, argumen masih bisa diikuti | Semua 6 koneksi terhubung, red thread jelas        |      |
| Specificity  | Variabel/metrik masih abstrak, tidak ada angka   | Sebagian metrik terdefinisi numerik           | Semua metrik + threshold + unit pengukuran jelas   |      |
| Feasibility  | Timeline >6 bulan tanpa memperhitungkan sumber   | Timeline 3-6 bulan dengan asumsi tertentu     | Timeline 1-3 bulan realistis dengan rencana detail |      |
| Rigor        | Baseline tidak jelas atau straw man              | 1-2 baseline dengan justifikasi partial       | 2+ baseline SOTA + justifikasi pemilihan lengkap   |      |
```

---

## Latihan 1 — Kompilasi Proposal Mini

Kumpulkan hasil dari WS-02 sampai WS-07 menjadi satu ringkasan proposal.

| Komponen | Sumber | Isi (1-2 kalimat) |
|----------|--------|-------------------|
| Problem Statement | WS-02 | Pertumbuhan data e-commerce yang masif menuntut efisiensi DBMS yang belum teruji konsistensinya. |
| Gap | WS-03 | Kurangnya evaluasi empiris performa antara SQL dan NoSQL pada lingkungan terdistribusi/cloud-native. |
| RQ | WS-04 | Apakah terdapat perbedaan performa latency dan throughput antara MySQL dan MongoDB pada sistem e-commerce berskala besar? |
| Hipotesis | WS-04 | H₁: MongoDB memiliki throughput lebih tinggi, sedangkan MySQL unggul dalam latency konsisten pada beban kerja tertentu. |
| Variabel & Metrik | WS-05 | IV: Jenis DBMS; DV: Latency (ms) & Throughput (RPS). |
| Sistem | WS-06 | Dockerized MySQL dan MongoDB dengan K6 Load Generator. |
| Desain Eksperimen | WS-07 | Comparison study dengan 5-10 kali pengulangan pada 100k-1juta record. |

---

## Latihan 2 — Integration Checklist

Verifikasi 6 koneksi kritis. Isi dengan merujuk tabel di Latihan 1.

| Koneksi | Status | Bukti |
|---------|--------|-------|
| Problem → Gap |✅ | Literasi menunjukkan bias pada pengujian lokal, kami mengisi gap dengan cloud-native test. |
| Gap → RQ | ✅ | RQ secara eksplisit bertanya tentang performa di cloud-native untuk mengisi gap tersebut. |
| RQ → Hypothesis | ✅ | Hipotesis memberikan prediksi terukur atas pertanyaan di RQ. |
| Hypothesis → Metric | ✅ | Latency dan RPS adalah cerminan langsung dari prediksi performa di hipotesis. |
| Metric → System | ✅ | K6 di sistem kami dirancang untuk mengeluarkan log latency dan RPS secara otomatis. |
| System → Experiment | ✅ | Desain eksperimen kami menggunakan sistem tersebut untuk menjalankan skenario uji. |

**Koneksi mana yang paling lemah?** _______________________
**Bagaimana cara memperkuatnya?**
> ___________________________________________________

**Konsistensi horizontal — apakah istilah dan scope konsisten?** [x] Ya / [ ] Tidak
> Jika tidak, di bagian mana terjadi inkonsistensi?

---

## Latihan 3 — Rubrik Self-Assessment

Evaluasi proposal mini menggunakan rubrik.

| Kriteria | Skor (1-3) | Justifikasi |
|----------|-----------|-------------|
| Koherensi | 3 | Alur dari masalah ke desain eksperimen sudah sangat sinkron. |
| Specificity | 3 | Metrik (ms, RPS) dan Threshold (p < 0.05) sudah sangat jelas. |
| Feasibility | 3 | Menggunakan Docker dan K6 sangat realistis untuk dijalankan dalam 1-2 bulan. |
| Rigor | 3 | Menggunakan standar industri dan threat analysis yang komprehensif. |

**Skor total:** 12 / 12

**Apakah proposal siap untuk fase eksekusi?** [x] Ya / [ ] Belum
> Jika belum, apa yang perlu diperbaiki?

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-08, bagian mana yang paling mudah dan paling sulit? Mengapa? Apa yang akan dilakukan berbeda jika mengulang dari awal?

**Bagian termudah:** WS-05 (Variabel & Metrik), karena secara teknis saya sudah memahami apa yang ingin diukur.
**Bagian tersulit:** WS-03 (Gap Identification), karena harus membedakan antara "apa yang belum diteliti" dan "apa yang secara logis harus diteliti".
**Yang akan dilakukan berbeda:**  Di awal, saya seharusnya tidak terlalu terobsesi mencari database yang "paling baru", tetapi fokus pada membandingkan standar industri yang paling relevan dengan masalah nyata.
