# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

> **Mengapa reproducibility penting?** Sains dibangun di atas prinsip verifikasi — temuan harus bisa dikonfirmasi oleh peneliti lain. _Replicability crisis_ yang terjadi di banyak paper riset ML/AI disebabkan oleh environment tidak terdokumentasi: orang lain tidak bisa reproduksi, hasil diragukan, kepercayaan terhadap temuan hilang. Prinsip: **dokumentasi environment = snapshot kredibilitas riset Anda.**

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
   - **Docker** = teknologi container yang "membungkus" aplikasi beserta seluruh dependency-nya dalam satu unit terisolasi. Hasilnya: kode berjalan identik di laptop, server, maupun reviewer lain. Intro singkat: `docker run -v $(pwd):/workspace environment-image python run_experiment.py`
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Dependency Locking

Mengandalkan "install library terbaru" berbahaya: versi berbeda = perilaku berbeda = hasil tidak reproducible. Praktik:
- **Python**: buat `requirements.txt` dengan versi eksplisit: `scikit-learn==1.3.2`, lalu kunci dengan `pip freeze > requirements.txt`
- **Conda**: gunakan `conda env export > environment.yml` untuk snapshot lengkap
- **Node.js/R/Julia**: gunakan `package-lock.json` / `renv.lock` / `Project.toml` — semua fungsi serupa: lock versi + hash

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : ____________________
  RAM     : ____________________
  GPU     : ____________________
  Storage : ____________________

Software:
  OS        : ____________________
  Runtime   : ____________________
  Framework : ____________________

Dependencies:
| Library | Version | Sumber | Hash/Checksum |
|---------|---------|--------|---------------|
|         |         |        |               |
|         |         |        |               |

Konfigurasi:
  Config file     : ____________________
  Random seed     : ____________________
  Hyperparameters : ____________________

Reproducibility Check:
  [ ] Dependency terdokumentasi (requirements.txt / lock file)
  [ ] Seed ditetapkan di semua level (Python, NumPy, framework)
  [ ] Config di version control
  [ ] README instruksi reproduksi lengkap
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| tools/software | Zotero (Reference Manager), MS Excel (Matriks Analisis) |
| search engine | Google Scholar, IEEE Xplore |
| Protocol | Kueri: "MySQL vs MongoDB" AND "Performance" AND "Cloud" |
| Inclusion Criteria | Paper terbitan 2022-2026, fokus pada perbandingan performa DBMS |
| Exlusion Criteria | Paper tanpa data empiris/benchmarking, paper dalam bahasa selain Indonesia/Inggris |


**Dependencies (sumber literatur):**

| Library | tahun | relevansi |
|---------|---------|-------------------|
| Putra et al. | 2022 | Benchmark dasar MySQL, PostgreSQL, MongoDB |
| Hilman et al. | 2025 | Analisis skalabilitas SQL vs NoSQL |
| Ilham et al. | 2026 | Performa e-commerce skala kecil |
| Saputra et al. | 2024 | Performa beban data besar |
| Avrylya & Susetyo | 2024 | Text indexing MongoDB vs ArangoDB |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Query String | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | "SQL vs NoSQL performance comparison" | 25 | — |
| 2 | "SQL vs NoSQL performance comparison" | 25 | [x] Ya / [ ] Tidak |
| 3 | "SQL vs NoSQL performance comparison" | 25 | [x] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**

> Penyebab umum non-repeatability:
> - Update database: Search engine (seperti Google Scholar) indeksnya berubah setiap waktu.
> - Variasi Kueri: Search engine memiliki algoritma personalized ranking.
> - Checklist kontrol: [x] Gunakan mode Incognito, [x] Catat tanggal akses, [x] Simpan URL permanen (DOI).
___________________________________________________

**Checklist kontrol yang sudah diterapkan:**
- [x] Random seed di-set di semua level
- [x] Tidak ada background process yang mengganggu
- [ ] Cache dibersihkan antar-run
- [ ] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Studi Literatur Performa Basis Data SQL dan NoSQL

## 1. Protocol
> Penelusuran literatur dilakukan menggunakan PRISMA-lite framework untuk memastikan sistematika pengumpulan data.

## 2. Tools
> Zotero untuk manajemen referensi; Excel untuk pemetaan literatur (concept-centric table).

## 3. Data Source
> 5 jurnal utama (Putra, Hilman, Ilham, Saputra, Avrylya) dengan rentang tahun 2022-2026.

## 4. Execution
> Langkah: Pencarian kueri → Screening Judul → Membaca Abstrak → Sintesis Data.

## 5. Configuration
> Kriteria inklusi: Riset empiris atau SLR; Kriteria eksklusi: Tutorial/Opini tanpa data.

## 6. Expected Output
> Tabel matriks perbandingan performa dan identifikasi research gap.
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [x] Repeatability / [ ] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Mungkin perlu catatan lebih detail mengenai Search Engine Algorithms yang tidak selalu deterministik.
