# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

  Contoh config YAML dengan feature toggles:
  ```yaml
  model:
    type: cnn          # IV: ganti "rf" untuk kondisi baseline
  features:
    use_temporal: true  # toggle komponen temporal
    use_normalization: true  # toggle preprocessing
  experiment:
    seed: 42
    runs: 5
  ```
  Dengan pendekatan ini, berbeda kondisi eksperimen = berbeda satu baris config, **tanpa mengubah kode**.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question: Sejauh mana perbedaan performa latency dan throughput antara MySQL (SQL) dan MongoDB (NoSQL) dalam memproses transaksi data skala besar pada lingkungan cloud-native?

Variable → Component Mapping:
| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
|----------|------|-----------------|---------------------------|
|Jenis DBMS| IV   |Database Instance (MySQL vs MongoDB)|Swap kontainer Docker (Feature Toggles)|
|Latency/Troughtput| DV   |Performance Monitor (K6 Metrics Collector)|Log extraction dari output hasil load test|
|Hardware & Dataset| CV   |Cloud Resource Config & Data Generator||Fixed environment & Fixed seed pada Faker.js

4 Prinsip Desain:
  [x] Traceability — Modul load test diatur untuk memanggil endpoint yang berbeda untuk setiap DBMS.
  [x] Variable Isolation — Dataset (CV) tetap sama, hanya engine (IV) yang ditukar.
  [x] Measurement Integration — engukuran DV (latency/RPS) dilakukan secara real-time oleh K6.
  [x] Reproducibility — Setup menggunakan Docker Compose agar mudah direplikasi di lingkungan lain.

Experimental Setup:
  Input data     : JSON dataset skala besar (100k, 500k, 1juta record)
  Parameter      : Concurrency (100 user simultan), Duration (5 menit per test)
  Output format  : CSV (berisi statistik latency rata-rata, P95, dan throughput RPS) 
```

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:** __________________________________________________

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|---------------------------|
| Jenis DBMS | *IV* | Container Orchestrator (Docker) | Mengganti image database pada script |
|Waktu Respon | DV |K6 Metrics Collector|Aggregated metric dari summary report K6|
|Skala Data| CV |Python/JS Data Generator|Menyesuaikan parameter count pada generator data|

**Apakah semua variabel bisa di-map?** [x] Ya / [ ] Tidak
> Jika tidak, komponen apa yang perlu ditambahkan? _________

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|-------------------|
| Traceability | ✅ | Komponen load test terhubung langsung ke database instance |
| Modularity | ✅ | Database layer terpisah secara logis dari application layer |
| Controllability | ✅ | Konfigurasi sistem dikontrol melalui environment variables |
| Measurability | ✅ | Tool K6 menghasilkan output statistik yang terukur secara otomatis |

**Prinsip mana yang paling sulit dipenuhi?** Controllability.
**Strategi untuk mengatasinya:**
> Menggunakan Docker dan YAML configuration sehingga setiap parameter (seperti alokasi RAM/CPU) terkunci dan bisa dipastikan konsisten antara MySQL dan MongoDB

---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.

> **Panduan jumlah kondisi:** Untuk 3 komponen (A, B, C), kondisi minimal yang direkomendasikan:
> Full + (-A) + (-B) + (-C) = **4 kondisi dasar**. Jika waktu memungkinkan, tambahkan kombinasi ganda: (-A,-B), (-A,-C), (-B,-C) = **7 kondisi**. Sesuaikan dengan *computational cost* dan tenggat waktu penelitian.

| Kondisi | Komponen A | Komponen B | Komponen C | Hasil yang Diharapkan |
|---------|-----------|-----------|-----------|----------------------|
| Full | ✅ | ✅ | ✅ | Baseline performa total |
| – A | ❌ | ✅ | ✅ | Dampak performa pada operasi tulis |
| – B | ✅ | ❌ | ✅ | Dampak performa pada operasi baca |
| – C | ✅ | ✅ | ❌ | Dampak performa pada kueri kompleks (JOIN/Agg) |

**Komponen mana yang diprediksi paling berkontribusi?** Skenario C (Complex).
**Mengapa?**
> Karena perbedaan arsitektur SQL (relasional) dan NoSQL (dokumen) akan terlihat paling tajam saat memproses kueri agregasi atau join data yang kompleks.

---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
> Risiko jika sistem dibangun seperti produk (fitur lengkap) lalu baru bereksperimen adalah "Confounding Variables". Kita tidak akan tahu apakah performa buruk disebabkan oleh database, atau karena adanya overhead dari fitur lain (seperti logging yang berlebihan, sistem caching yang tidak disengaja, atau bottleneck di aplikasi). Arsitektur modular penting agar kita bisa melakukan isolasi variabel, memastikan bahwa perbedaan hasil performa benar-benar berasal dari DBMS yang diuji, bukan dari faktor luar.
