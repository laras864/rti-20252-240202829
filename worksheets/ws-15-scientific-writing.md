# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## Template A.15 — Paper Structure Checklist

```
PAPER STRUCTURE CHECKLIST

Title   : Analisis Komparatif Performa Latency dan Throughput Basis Data SQL dan NoSQL pada Lingkungan Cloud-Native.
Target  : [x] Jurnal  [ ] Konferensi  [ ] Laporan

Section Check:
  [[x] Abstract — Membahas masalah skalabilitas, metode SLR, temuan keunggulan throughput NoSQL, dan implikasi.
  [x] Introduction — Konteks e-commerce, gap riset parsial, RQ mengenai performa cloud-native.
  [x] Related Work — Pemetaan literatur berbasis topik (benchmark performa & arsitektur basis data).
  [x] Method — SLR dengan PRISMA-lite, kriteria inklusi 2022-2026, metrik latency/throughput.
  [x] Results — Matriks komparatif performa SQL vs NoSQL dalam tabel & grafik sintesis.
  [x] Discussion — Interpretasi hasil, trade-off antara konsistensi dan throughput, limitasi riset.
  [x] Conclusion — Jawaban RQ, rekomendasi arsitektur, dan potensi riset masa depan.

Consistency Matrix:
  [x] RQ di Introduction = RQ di Method = RQ di Conclusion
  [x] Variabel di Method = variabel di Results
  [x] Klaim di Discussion didukung data di Results
  [x] Limitasi di Discussion di-address di Conclusion/Future Work

Writing Quality:
  [x] Clarity — mudah dipahami tanpa re-read
  [x] Precision — tidak ada istilah ambigu
  [x] Conciseness — tidak ada kalimat redundan
```

---

## Latihan 1 — Paper Outline

Buat outline paper untuk riset Anda menggunakan struktur IMRAD.

| Section | Konten Utama (2-3 kalimat) | Target Kata |
|---------|---------------------------|------------|
| Abstract | Motivasi performa cloud, metode SLR, hasil MongoDB > MySQL dalam throughput, SQL stabil | 200-250 |
| Introduction | Kebutuhan data e-commerce, gap riset lokal vs cloud, RQ: komparasi efisiensi SQL vs NoSQL | 500-700 |
| Related Work | Tinjauan paper 2022-2026 tentang benchmarking basis data dan optimasi cloud-native | 700-1000 |
| Method | Protokol SLR PRISMA-lite, kriteria inklusi paper, normalisasi metrik (latency/throughput) | 800-1200 |
| Results | Tabel sintesis data dari 5 paper terpilih dan observasi perbandingan metrik | 500-800 |
| Discussion | Interpretasi trade-off, signifikansi statistik (p=0.042), limitasi eksternal (hardware) | 600-900 |
| Conclusion | Kesimpulan akhir basis data optimal per skenario, kontribusi riset, saran riset masa depan | 200-400 |

---

## Latihan 2 — Consistency Matrix

Buat consistency matrix untuk memverifikasi internal consistency paper Anda.

|  | Intro | Method | Result | Discussion | Conclusion |
|--|-------|--------|--------|-----------|-----------|
| *Contoh: RQ1* | *✓* | *✓* | *✓* | *✓* | *✓* |
| *Contoh: Metrik | *✗ ←* | *✗ ←* | *✓* | *✗ ←* | *✗ ←* |
| RQ1 | | | | | |
| RQ2 | | | | | |
| Metrik utama | | | | | |
| Variabel IV | | | | | |
| Variabel DV | | | | | |
| Klaim/kontribusi | | | | | |

**Isi setiap sel:** ✓ (ada & konsisten), ✗ (missing), ~ (ada tapi inkonsisten)

**Inkonsistensi yang ditemukan:**
> ___________________________________________________

**Tindakan perbaikan:**
> ___________________________________________________

---

## Latihan 3 — Writing Quality Check

Ambil satu paragraf dari tulisan Anda (atau tulis paragraf baru) dan evaluasi kualitasnya.

**Paragraf asli:**
> (tempel paragraf Anda di sini)

| Kriteria | Evaluasi | Perbaikan |
|----------|---------|-----------|
| Clarity | *Contoh: kalimat ke-3 ambigu — "performa" bisa berarti accuracy atau speed* | *Ubah menjadi: "accuracy meningkat..."* |
| Precision | | |
| Conciseness | | |

**Paragraf setelah perbaikan:**
> (tulis paragraf yang sudah diperbaiki)

---

## Refleksi

> Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?

> ___________________________________________________
> ___________________________________________________
