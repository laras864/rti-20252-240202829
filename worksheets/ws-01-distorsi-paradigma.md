# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (DSR). Penting untuk membedakan keduanya:

| Paradigma | Cara Kerja | Contoh di TI |
|-----------|-----------|---------------|
| **Positivis** | Uji hipotesis dengan eksperimen terkontrol | Apakah CNN lebih akurat dari RF pada dataset X? |
| **Design Science Research** | Bangun artefak (sistem/model/framework) untuk menguji proposisi | Dapatkah arsitektur hybrid CNN+LSTM membuktikan peningkatan recall ≥5%? |
| **Interpretivis** | Pahami makna melalui konteks & kualitatif | Bagaimana peneliti manafsirkan anomali data sensor IoT? |

Dalam DSR, artefak **bukan tujuan akhir** — ia adalah instrumen untuk menghasilkan pengetahuan. Pertanyaan riset tetap harus difalsifikasi.

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Anindiya Larasati
Tanggal          : 12 Juli 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: Bagaimana spesifikasi testbed (hardware/software) yang digunakan dalam pengujian, dan apakah dataset yang digunakan (20.058 baris data catur) cukup representatif untuk merepresentasikan beban kerja "Big Data" yang sebenarnya di instansi?
   - Data yang dibutuhkan untuk verifikasi: Data hasil pengujian dengan skenario concurrency (banyak pengguna mengakses bersamaan) dan variasi ukuran data yang jauh lebih besar (skala jutaan baris) untuk melihat apakah PostgreSQL tetap unggul di beban kerja yang lebih berat.

2. Posisi paradigma:
   - Pendekatan: [X] Positivis  [ ] Interpretivis  [ ] Design Science  [ ] Mixed
   - Alasan: Penelitian ini menggunakan pendekatan Positivis karena bertujuan mengukur performa (respon waktu) secara objektif dan kuantitatif melalui eksperimen terkontrol dengan skenario yang sudah ditentukan.

3. Identifikasi distorsi:
   - Asumsi tersembunyi: Peneliti berasumsi bahwa pengujian pada satu tabel tanpa relasi sudah cukup adil untuk membandingkan PostgreSQL, MySQL, dan MongoDB.
   - Sumber bias potensial: Bias perangkat keras (pengujian hanya dilakukan pada satu testbed spesifik). Melakukan pengujian pada berbagai spesifikasi hardware dan sistem operasi yang berbeda untuk melihat konsistensi hasil.

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: Data raw hasil pengukuran waktu respon setiap kueri (tidak membuang data outlier tanpa alasan teknis yang jelas).
   - Batasan yang diakui sejak awal: Penelitian ini tidak menggunakan data berelasi dan terbatas pada dataset catur dari Kaggle.
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

> **Panduan pencarian paper:** Gunakan [IEEE Xplore](https://ieeexplore.ieee.org), [ACM Digital Library](https://dl.acm.org), atau Google Scholar. Pilih paper **tahun 2020 ke atas**, di topik yang Anda minati: deteksi anomali, klasifikasi citra, NLP, keamanan siber, IoT, dsb.
>
> **Contoh domain TI:** "Deteksi anomali lalu-lintas jaringan menggunakan CNN — akurasi meningkat 94% vs baseline SVM 87%." Distorsi potensial: apakah dataset normal/anomali seimbang? Apakah hanya diuji pada satu vendor traffic?

**Paper yang dipilih:**
> Judul: Perbandingan Performa Respon Waktu Kueri MySQL, PostgreSQL, dan MongoDB
> Penulis (Tahun): Yudha Yunanto Putra, Oktania Purwaningrum, Rivaldo Hadi Winata (2022)
> Sumber/Link DOI: http://ejournal.upnjatim.ac.id/index.php/sibc/article/view/1515 

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | Mengambil dataset catur dari Kaggle. | Selection Bias: Dataset catur mungkin tidak mencerminkan pola data yang biasa dihadapi sistem instansi riil. |
| Data → Processing | Melakukan eksekusi kueri INSERT, SELECT, UPDATE, DELETE, SUM, COUNT. | Measurement Bias: Pengujian mungkin dipengaruhi oleh proses background pada OS Windows yang digunakan. |
| Processing → Analysis | Menjumlahkan hasil waktu respon dari perulangan untuk mendapatkan total performa. | Oversimplification: Menjumlahkan total waktu respon bisa menyembunyikan karakteristik performa spesifik per jenis kueri. |
| Analysis → Inference | Menyimpulkan PostgreSQL paling cepat secara keseluruhan. | Overgeneralization: Mengklaim PostgreSQL paling cepat tanpa mempertimbangkan use case spesifik (misal: MongoDB mungkin lebih baik untuk data tidak terstruktur). |
| Inference → Knowledge | Memberikan acuan pemilihan DBMS bagi instansi. | Assumption: Peneliti mengasumsikan hasil lab akan sama persis dengan implementasi di instansi. |

**Distorsi paling besar di tahap:**  Analysis → Inference

**Dua distorsi spesifik yang teridentifikasi:**
1. Asumsi bahwa total waktu respon adalah metrik terbaik untuk membandingkan DBMS. 
2. Dataset yang homogen. 

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

**Perspektif:** Kejujuran ilmiah menuntut peneliti untuk melaporkan hasil apa adanya. Jika PostgreSQL ternyata lambat pada kueri tertentu (misalnya INSERT), hal tersebut harus tetap ditampilkan untuk memberikan gambaran objektif. Menghapus data demi membuat PostgreSQL terlihat selalu menang adalah tindakan manipulasi data.

**Keputusan akhir dan justifikasi:**
> Peneliti harus menampilkan hasil pengujian secara transparan. Jika ada outlier yang sangat tinggi (misalnya karena sistem Windows melakukan update otomatis saat pengujian), peneliti boleh mengeluarkan data tersebut hanya jika dijelaskan dalam bagian "Batasan Penelitian", agar pembaca tetap mendapatkan informasi yang akurat.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** Perbandingan Performa Respon Waktu Kueri MySQL, PostgreSQL, dan MongoDB.

> **Skala 1–5:** 1 = tidak sesuai sama sekali dengan topik ini, 5 = sangat sesuai dan dominan digunakan pada riset bertopik serupa.

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | *Contoh: 4 — topik kuantitatif, cocok uji hipotesis* | *Contoh: 2 — topik tidak studi makna/konteks* | *Contoh: 5 — membangun artefak untuk uji klaim* |
| Jenis data yang dikumpulkan | *Metrik numerik, log eksperimen* | *Wawancara, observasi kualitatif* | *Hasil uji artefak, komparasi kinerja* |
| Limitasi paradigma | | | |

**Paradigma yang dipilih:** positivis
**Alasan:** Fokus riset adalah mengukur fenomena (kecepatan respon DBMS) secara objektif melalui eksperimen yang dapat diulang (reproducible) dengan metrik waktu (milidetik) yang presisi.

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum mempelajari materi ini, saya cenderung menerima mentah-mentah klaim performa atau hasil riset yang disajikan dalam bentuk angka (misalnya: "Sistem X lebih cepat Y% dibanding sistem Z") tanpa memikirkan proses di balik perolehan angka tersebut. Setelah memahami rantai distorsi (Reality → Data → Processing → Analysis → Inference → Knowledge), sekarang saya akan selalu mempertanyakan hal-hal seperti Validitas Data, kondisi pengjian, Objektivitas Analisis dan keterbatasan klaim saat membaca paper.
