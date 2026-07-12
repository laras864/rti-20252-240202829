# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Manajemen Basis Data (Database Management Systems) 
  Konteks  : Pemilihan teknologi database untuk kebutuhan pengolahan data berskala besar (Big Data) pada instansi

System Context
  Input       : Dataset permainan catur (16 kolom, 20.058 baris)
  Process     : Eksekusi kueri INSERT, SELECT, UPDATE, DELETE, SUM, dan COUNT pada MySQL, PostgreSQL, dan MongoDB 
  Output      : Respon waktu eksekusi dalam satuan milidetik (ms)
  Outcome     : Rekomendasi pemilihan DBMS yang efisien bagi instansi
  Constraints : Pengujian menggunakan satu tabel tanpa relasi, hardware tunggal, dan sistem operasi Windows
  Stakeholders: Pengembang sistem dan instansi yang membutuhkan efisiensi pemrosesan data

Fenomena → Problem
  Fenomena yang diamati             : Kecepatan aplikasi sangat dipengaruhi oleh performa DBMS dalam memproses data
  Gejala (symptom) yang terukur     : Adanya perbedaan waktu respon yang signifikan saat mengeksekusi kueri pada jenis DBMS yang berbeda
  Masalah yang didiagnosis          : Ketidakpastian instansi dalam memilih antara DBMS relasional (MySQL, PostgreSQL) dan NoSQL (MongoDB) untuk performa terbaik
  Masalah riset (researchable)      : Belum ada perbandingan performa respon waktu yang komprehensif antara MySQL, PostgreSQL, dan MongoDB pada skenario kueri standar (CRUD & Aggregation) menggunakan dataset yang sama
  Variabel yang terukur             : Respon waktu kueri (response time) dalam milidetik (ms) 

Problem Quality Check
  [ X ] Clarity — Apakah satu orang membaca akan paham?
  [ X ] Measurability — Apakah ada metrik kuantitatif?
  [ X ] Relevance — Apakah penting untuk domain?
  [ X ] Testability — Apakah bisa gagal?
  [ X ] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
  Pemilihan DBMS yang tepat sangat krusial bagi instansi untuk menjamin kecepatan akses data pada aplikasi yang menangani volume data besar. Namun, terdapat ketidakpastian dalam menentukan jenis DBMS (relasional vs NoSQL) yang paling optimal karena performa sering kali bergantung pada skenario penggunaan. Riset ini mengukur dan membandingkan secara empiris waktu respon kueri pada MySQL, PostgreSQL, dan MongoDB untuk memberikan acuan teknis yang objektif bagi instansi dalam memilih teknologi basis data yang efisien.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Perbandingan performa DBMS untuk Big Data.

| Tahap | Hasil |
|-------|-------|
| Reality | Instansi membutuhkan database cepat namun sering bingung memilih antara SQL atau NoSQL |
| Observed Issue (Symptom) | Aplikasi berjalan lambat saat memproses ribuan data |
| Diagnosed Problem (Root Cause) | Efisiensi kueri DBMS yang belum teruji pada kasus penggunaan spesifik |
| Researchable Problem | Membandingkan performa respon waktu MySQL, PostgreSQL, dan MongoDB dalam skenario kueri CRUD |
| Measurable Variable | Waktu respon eksekusi kueri (milidetik) |

**Apakah terjebak solution-first thinking?** [ ] Ya / [x] Tidak
> Jika ya, kembali ke tahap mana? ________________________

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Data catur |
| Process | Operasi kueri |
| Output | Tabel dan grafik waktu respon |
| Outcome | Keputusan pemilihan database |
| Constraints | Dataset tunggal tanpa relasi |
| Stakeholders |Instansi |

**Komponen mana yang paling relevan dengan masalah riset?** Process (karena membandingkan efisiensi kueri setiap DBMS) 

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 5 | Masalah sangat spesifik(membandingkan 3 Database) |
| Measurability | 5 | Menggunakan satuan milidetik |
| Relevance | 4 | Sangat relevan bagi pengembangan sistem |
| Testability | 5 | Eksperimen dapat diulang |
| Impact | 4 | Memberikan acuan pada pemelihan teknoogi |

**Skor total:** 23 / 25

**Problem statement versi final (1 paragraf):**
> Meskipun pemilihan Database Management System (DBMS) merupakan faktor krusial bagi efisiensi sistem informasi di instansi, pengembang sering kali menghadapi ketidakpastian dalam memilih antara DBMS relasional (seperti MySQL dan PostgreSQL) dan NoSQL (seperti MongoDB) karena performa yang sangat bervariasi bergantung pada beban kerja kueri. Hingga saat ini, belum terdapat acuan teknis yang komprehensif mengenai perbandingan performa respon waktu kueri ketiga DBMS tersebut dalam skenario operasional yang seragam. Riset ini bertujuan untuk memberikan landasan empiris dengan mengukur dan membandingkan secara objektif waktu eksekusi kueri CRUD dan Aggregation pada dataset yang sama, sehingga hasil penelitian ini dapat menjadi referensi teknis yang objektif bagi instansi dalam memilih infrastruktur basis data yang paling efisien sesuai dengan kebutuhan operasionalnya.
---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Perbedaan mendasar terletak pada tujuan dan eksistensi masalahnya. Bug atau error saat coding adalah masalah praktis yang memiliki jawaban benar/salah (solusi teknis); jika bug diperbaiki, masalah selesai. Sebaliknya, masalah riset mendefinisikan sebuah celah pengetahuan (gap) yang belum terjawab. Riset tidak hanya mencari "perbaikan", tetapi mencari pemahaman mengapa suatu fenomena terjadi (misalnya, mengapa PostgreSQL lebih cepat dari MongoDB dalam skenario tertentu), dengan hasil yang harus teruji secara empiris dan dapat direplikasi oleh peneliti lain untuk memperkaya pengetahuan ilmiah.
