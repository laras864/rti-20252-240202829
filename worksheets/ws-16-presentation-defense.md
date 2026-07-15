# WS-16: Presentation & Defense (UAS)

> **Bab 16 — Presentasi & Pertahanan Ilmiah**

---

## Ringkasan Materi

### Scientific Defense Model

```
Research Work → Presentation → Questioning → Defense → Evaluation → Acceptance
```

### Presentasi ≠ Ringkasan Paper

| Paper | Presentasi |
|-------|-----------|
| Dibaca (self-paced) | Didengar (presenter-paced) |
| Detail lengkap | Ide kunci + highlight |
| Tabel numerik detail | Grafik visual + angka kunci |
| Pembaca bisa re-read | Audiens dengar sekali |

**Prinsip:** Presentasi membutuhkan **reformulasi**, bukan kompresi. Medium berbeda = pendekatan berbeda.

### Claim-Evidence-Reasoning (CER)

Setiap jawaban defense harus memiliki:
1. **Claim** — Pernyataan yang dijawab
2. **Evidence** — Data/fakta pendukung
3. **Reasoning** — Logika yang menghubungkan evidence ke claim

**Contoh:**
| Pertanyaan | Bad Answer | Good Answer (CER) |
|-----------|-----------|-------------------|
| "Kenapa hanya 3 dataset?" | "Tiga sudah cukup" | "3 dataset mewakili variasi: small-clean, medium-clean, medium-noisy [E]. Generalisasi perlu validasi lanjut — listed as limitation [R]" |
| "Hasil DS-3 menurun?" | "Itu outlier" | "Ya, karena distribusi heavy-tail melanggar asumsi Gaussian [E]. Ini menunjukkan boundary condition metode [R]" |
| "Effect size?" | "p=0.003, jadi signifikan" | "Cohen's d=1.2 (large effect) [E] — bukan hanya signifikan tapi substansial [R]" |

### Slide Design — One Slide, One Message

**Optimal 9-Slide Plan (15 menit):**

| # | Slide | Waktu | Pesan |
|---|-------|-------|-------|
| 1 | Title + context | 1 min | Apa ini tentang apa |
| 2 | Problem + motivation | 2 min | Mengapa penting |
| 3 | Gap + RQ | 1.5 min | Apa yang belum terjawab |
| 4 | Method overview | 2 min | Bagaimana dijawab (diagram) |
| 5 | Key result — tabel | 2 min | Temuan utama |
| 6 | Key result — grafik | 2 min | Pola visual |
| 7 | Interpretation + failure | 2 min | Apa artinya |
| 8 | Limitation + future | 1.5 min | Batasan & arah |
| 9 | Conclusion + contribution | 1 min | Closing message |

### Anticipatory Defense

Prediksi pertanyaan berdasarkan kategori:

| Kategori | Contoh Pertanyaan |
|---------|------------------|
| Problem | "Mengapa masalah ini penting?" |
| Gap | "Bagaimana dengan studi X yang sudah menjawab ini?" |
| Method | "Mengapa metode ini, bukan Y?" |
| Results | "Bagaimana menjelaskan anomali di DS-3?" |
| Generalization | "Apakah bisa diterapkan di domain lain?" |

### Tiga Prinsip Jawaban

1. **Direct** — Jawab dulu, elaborasi kemudian
2. **Data-based** — Tunjuk evidence spesifik
3. **Honest** — Akui limitasi jika memang ada

### Jebakan Kognitif

1. "Presentasi = semua yang ada di paper" → terlalu padat
2. "Slide cantik = presentasi bagus" → konten > estetika
3. "Tidak bisa jawab = gagal" → "I don't know, but..." menunjukkan kejujuran
4. "Tidak perlu latihan — saya paham riset saya" → latihan = menemukan celah

---

## Template A.16 — Defense Preparation Sheet

```
DEFENSE PREPARATION

Slide Deck Plan:
  Total slides   :  9 slide
  Time per slide : ~1.5-2 min
  Total time     : 15 menit

Slide Outline:
| # | Pesan Utama | Visual | Waktu |
|---|-------------|--------|-------|
| 1 | Title       | Judul & Diagram Ekosistem | 1min   |
| 2 | Problem     | Grafik pertumbuhan data | 2min  |
| 3 | Gap + RQ    | Tabel gap literatur | 1.5min  |
| 4 | Metodologi: PRISMA-lite | Flowchart seleksi paper | 2 min|
| 5 | Key Result: Tabel Sintesis | Tabel 1 (Matriks Performa) | 2 min|
| 6 | Key Result: Pola Throughput | Grafik Bar Performa | 2 min |
| 7 | Interpretasi: SQL vs NoSQL | Skema Use-Case (Trade-off) | 2 min|
| 8 | Limitasi & Future Work | Checklist (Hardware bias) | 1.5 min|
| 9 |Kesimpulan & Kontribusi| Poin-poin utama | 1min|


Anticipatory Defense Matrix:
| Kategori | Pertanyaan Potensial | Jawaban (CER) | 
|----------|---------------------|---------------|
| Problem  | Mengapa SQL vs NoSQL masih relevan? | Pilihan tepat krusial bagi biaya & skala, Data e-commerce terus meningkat eksponensial, Arsitektur yang salah menyebabkan degradasi performa jangka panjang. |
| Method   | Mengapa hanya 5 paper? |5 paper sudah mewakili tren 2022-2026, Kriteria inklusi ketat pada jurnal bereputasi, Kualitas > Kuantitas untuk sintesis literatur yang mendalam.|
| Results  | Mengapa NoSQL lebih unggul? | Unggul pada write-heavy & skalabilitas horizontal, Data Throughput NoSQL lebih tinggi (rata-rata 2.8k RPS), Skema fleksibel & eliminasi JOIN kompleks mempercepat I/O. |
| Generalization | Apakah hasil ini berlaku untuk semua aplikasi? | Tidak, ada boundary condition, SQL masih unggul di JOIN kompleks/ACID ketat, NoSQL bukan silver bullet, pemilihan bergantung pada kebutuhan integrasi data. |

Latihan:
  Latihan 1: [tanggal] — [catatan timing & feedback] - isi setelah kamu latihan presentasi sendiri dengan stopwatch
  Latihan 2: [tanggal] — [catatan timing & feedback] - isi setelah latihan kedua
  Latihan 3: [tanggal] — [catatan timing & feedback] - isi setelah simulasi Q&A dengan teman/kolega
```

---

## Latihan 1 — Slide Outline

Rencanakan presentasi 15 menit untuk riset Anda.

| # | Pesan Utama | Visual yang Digunakan | Waktu |
|---|-------------|----------------------|-------|
| 1 | Judul & Konteks Cloud-Native | Title slide & Diagram Ekosistem Cloud | 1 min |
| 2 | Problem: Tantangan E-Commerce | Grafik tren data eksponensial | 2 min |
| 3 | Gap & Research Question | Tabel perbandingan gap literatur | 1.5 min |
| 4 | Metode: SLR PRISMA-lite | Flowchart seleksi literatur | 2 min |
| 5 | Key Result: Tabel Sintesis | Tabel performa (MySQL vs MongoDB) | 2 min |
| 6 | Key Result: Pola Throughput | Grafik bar throughput (RPS) | 2 min|
| 7 | Interpretasi: Trade-off & Failures | Skema Use-Case (SQL vs NoSQL) | 2 min |
| 8 | Limitasi & Arah Masa Depan | Checklist limitasi riset | 1.5 min|
| 9 | Kesimpulan & Kontribusi | Poin kunci kontribusi riset | 1 min |

**Total waktu estimasi:** 15 menit

---

## Latihan 2 — Anticipatory Defense

Prediksi 5 pertanyaan yang mungkin diajukan penguji, lalu siapkan jawaban CER.

| # | Kategori | Pertanyaan | Claim | Evidence | Reasoning |
|---|----------|-----------|-------|----------|-----------|
| 1 | Problem | Mengapa SQL vs NoSQL masih relevan? | Pilihan database krusial untuk biaya & skala | Data e-commerce naik eksponensial | Arsitektur salah = degradasi performa sistem |
| 2 | Method | Mengapa hanya 5 paper? | 5 paper sudah mewakili tren 2022-2026. | Kriteria inklusi jurnal bereputasi | Kualitas > Kuantitas untuk sintesis literatur |
| 3 | Result | Mengapa NoSQL lebih unggul? | Unggul pada write-heavy & skalabilitas | Throughput NoSQL rata-rata 2.8k RPS | Eliminasi JOIN kompleks mempercepat I/O |
| 4 | Generalization | Apakah hasil ini mutlak? | Tidak, ada boundary condition | SQL masih unggul di JOIN kompleks/ACID | NoSQL bukan silver bullet untuk semua kasus |
| 5 | Analysis | Bagaimana jika hasil paper berbeda? | Hasil berbeda adalah temuan (boundary) | Analisis variasi hardware per paper | Kontradiksi menunjukkan ketergantungan pada use-case |

---

## Latihan 3 — Simulasi Q&A

Minta teman/kolega mengajukan 3 pertanyaan tentang riset Anda. Catat pertanyaan dan evaluasi jawaban Anda.

| # | Pertanyaan | Jawaban Saya | Evaluasi |
|---|-----------|-------------|---------|| *1* | *Contoh: "Mengapa tidak membandingkan dengan metode Y?"* | *Contoh: "Karena Y memerlukan dataset labeled yang tidak tersedia. Disebutkan sebagai limitasi di halaman X."* | *[✓] Direct [✓] Data-based [✓] Honest* || 1 | | | [ ] Direct [ ] Data-based [ ] Honest |
| 2 | | | [ ] Direct [ ] Data-based [ ] Honest |
| 3 | | | [ ] Direct [ ] Data-based [ ] Honest |

**Pertanyaan yang paling sulit dijawab:**
> (isi setelah simulasi Q&A dilakukan)

**Apa yang perlu disiapkan lebih baik:**
> (isi setelah simulasi Q&A dilakukan)


---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-16 — dari paradigma riset hingga presentasi — bagian mana yang paling mengubah cara Anda berpikir tentang riset? Apa satu hal yang akan selalu Anda terapkan di riset berikutnya?

**Insight terbesar:**
> Saya menyadari bahwa riset literatur (SLR) bukan sekadar merangkum, melainkan "menghakimi" data yang ada dari berbagai sumber untuk menarik kesimpulan baru yang objektif.

**Yang akan selalu diterapkan:**
> Prinsip CER (Claim-Evidence-Reasoning). Setiap argumen atau jawaban saya harus selalu berbasis pada data (Evidence) dan alur logika (Reasoning), bukan sekadar opini pribadi.
