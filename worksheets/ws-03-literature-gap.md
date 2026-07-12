# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

**Perbandingan pendekatan Author-centric vs Concept-centric:**

| Aspek | Author-centric (Hindari) | Concept-centric (Gunakan) |
|-------|--------------------------|---------------------------|
| Struktur | Per penulis/paper ("Rahman et al. menyatakan...") | Per konsep/metode ("Pendekatan berbasis transformer") |
| Tujuan | Ringkasan isi paper | Perbandingan metode & identifikasi gap |
| Contoh paragraph | "Rahman (2023) pakai CNN. Lee (2022) pakai LSTM. Zhang (2021) pakai RF." | "Tiga pendekatan dominan: CNN digunakan oleh 4 paper untuk representasi fitur visual; LSTM untuk data sekuensial; RF sebagai baseline klasik." |
| Hasil akhir | Daftar paper | Peta pengetahuan + gap yang teridentifikasi |

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database utama**: IEEE Xplore, ACM DL, Scopus
   - Akses IEEE/ACM melalui jaringan kampus atau VPN institusi
   - Alternatif bebas biaya: Google Scholar, ResearchGate ([researchgate.net](https://www.researchgate.net)), arXiv ([arxiv.org](https://arxiv.org))
2. **Boolean query** yang terdokumentasi eksplisit
   - Contoh: `("anomaly detection" OR "intrusion detection") AND ("deep learning" OR "neural network") NOT ("medical imaging")`
   - Gunakan tanda kutip untuk frasa eksak; AND/OR/NOT mengontrol scope
3. **Snowballing** — dua arah:
   - **Backward snowballing**: buka daftar referensi di paper kunci → telusuri paper yang dikutip
   - **Forward snowballing**: di Google Scholar, klik "Cited by" di bawah paper kunci → temukan paper yang mengutipnya
   - Ulangi 1–2 tingkat untuk membangun cakupan komprehensif
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Perbandingan Performa SQL (MySQL) vs NoSQL (MongoDB) pada Sistem Berbasis Web
Database   : Google Scholar
Query      : MYSQL, SQL, MongoDB, NoSQL, performance, response time
Tahun      : 2021-2026
Hasil awal : 9 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
|Avrylya & Susetyo|2024|Eksperimen|1JT record|MongoDB lebih cepat dalam text indexing dibanding ArangoDB|Hanya Fokus pada pencarian teks|
|Putra et al|2022|Eksperimen|20rb baris catur|PostgreSQL tercepat, MySQL & MongoDB bersaing|Beluum menguji sharding|
|Hilman et al|2025|Studi literatur|13 paper|NoSQL unggul di skalabilitas, SQL unggul di konsistensi|Analisis bersifat sintesis, bukan uji empiris|
|Ilham e al|2026|SLR|20 paper|MongoDB unggul di write-heavy, MySQL unggul di JOIN|Terbatas pada e-commerce skala kecil|
|Saputra et al|2024|eksperimen|100rb data|MongoDB unggul di load data besar|belum ada pengujian sharding|

   

Pola yang ditemukan:
  Metode dominan     : Benchmarking berbasis waktu respon (latency) pada operasi CRUD
  Dataset umum       : Dataset dari Kaggle atau data transaksi e-commerce/permainan
  Limitasi berulang  : Banyak penelitian hanya menguji single-node dan belum mengeksplorasi arsitektur hibrida (Polyglot Persistence) 

GAP IDENTIFICATION

Gap 1: [Jenis: method gap]
  Deskripsi    : Kurangnya implementasi arsitektur basis data hibrida (menggabungkan SQL & NoSQL).
  Bukti        : Kebanyakan penelitian hanya membandingkan head-to-head mana yang lebih cepat, bukan bagaimana mengintegrasikan keduanya
  Signifikansi : Penting untuk sistem modern agar mendapatkan integritas transaksi (SQL) sekaligus fleksibilitas data (NoSQL) 

Gap 2: [Jenis: Context gap]
  Deskripsi    : Kurangnya evaluasi pada cloud-native deployment dengan container
  Bukti        : Sebagian besar pengujian dilakukan di lingkungan lokal
  Signifikansi : Performa di lingkungan cloud akan berbeda karena adanya faktor latensi jaringan dan resource isolation

Baseline Selection:
| Baseline | Relevansi | Representatif |
|----------|-----------|---------------|
|MySQL|standar industri|paling banyak digunkan sebagai pembanding dalam penelitian performa database|
|MongoDB|paradigma document-oriented|standar utama penelitian databaseNoSQL yang menonjolkan skalabilitas horizontal|

```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:** ________________________________________
**Query pencarian:** ____________________________________
**Database:** ___________________________________________

| # | Study | Tahun | Method | Data | Result | Limitation |
|---|-------|-------|--------|------|--------|------------|
| 1 |Avrylya & Susetyo|2024|Eksperimen|1JT record|MongoDB lebih cepat dalam text indexing dibanding ArangoDB|Hanya Fokus pada pencarian teks|
| 2 |Putra et al|2022|Eksperimen|20rb baris catur|PostgreSQL tercepat, MySQL & MongoDB bersaing|Beluum menguji sharding|
| 3 |Hilman et al|2025|Studi literatur|13 paper|NoSQL unggul di skalabilitas, SQL unggul di konsistensi|Analisis bersifat sintesis, bukan uji empiris|
| 4 |Ilham e al|2026|SLR|20 paper|MongoDB unggul di write-heavy, MySQL unggul di JOIN|Terbatas pada e-commerce skala kecil|
| 5 |Saputra et al|2024|eksperimen|100rb data|MongoDB unggul di load data besar|belum ada pengujian sharding|

   


**Pola yang terlihat — Metode dominan:** Metode dominan: Benchmarking berbasis waktu respon (latency) pada operasi CRUD.
**Limitasi yang berulang:** Mayoritas penelitian dilakukan di lingkungan single-node dan belum mengeksplorasi arsitektur hibrida (Polyglot Persistence). 

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [x] Ya / [ ] Tidak | Performa belum diuji pada arsitektur cloud-native yang terdistribusi |
| Method Gap | [x] Ya / [ ] Tidak | Belum ada pendekatan hibrida (Polyglot Persistence) yang diuji secara empiris |
| Data Gap | [ ] Ya / [ ] Tidak | - |
| Context Gap | [x] Ya / [ ] Tidak | Evaluasi masih didominasi pengujian lokal (lab-based) |

**Gap utama yang dipilih:** Implementasi Arsitektur Hibrida (Polyglot Persistence) pada Lingkungan Cloud-Native.
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Karena di dunia nyata, jarang ada sistem besar yang hanya bergantung pada satu jenis database. Kebutuhan industri saat ini adalah sinergi antara integritas data SQL dan skalabilitas fleksibel NoSQL. Meneliti bagaimana kedua sistem ini berinteraksi dalam satu ekosistem yang terdistribusi adalah kontribusi yang jauh lebih relevan dibandingkan hanya membandingkan kecepatan CRUD dasar yang sudah sering dilakukan.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | MySQL (RDBMS) | Standar integritas data transaksional | Paling sering digunakan sebagai pembanding utama | Common Practice | Putra et al., 2022 |
| 2 | MongoDB (NoSQL) | Standar integritas data transaksional | Standar utama skalabilitas horizontal NoSQL | Common Practice | Saputra et al., 2024 |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [x] Tidak
> Justifikasi: Tidak, karena kedua baseline ini adalah industry standard yang digunakan dalam kelima jurnal yang kita bahas. Menggunakan standar industri sebagai pembanding justru membuat riset Anda lebih kredibel, bukan "curang".

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Perbedaan fundamentalnya adalah: "Belum ada yang meneliti" hanyalah klaim subjektif jika tidak didasarkan pada mapping literatur yang sistematis. Sedangkan research gap yang valid adalah kesimpulan logis yang muncul setelah kita memetakan banyak riset terdahulu dan menemukan pola atau keterbatasan yang berulang. Cara membuktikan gap adalah dengan melakukan Systematic Literature Review (SLR) atau memetakan temuan-temuan dari 5 paper tersebut; jika kita melihat bahwa 5 paper tersebut semuanya memiliki keterbatasan yang sama (misal: semuanya di lingkungan lokal), maka di situlah letak gap yang valid untuk kita ambil sebagai topik riset baru.
