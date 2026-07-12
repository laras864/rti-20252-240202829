# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question : Sejauh mana perbedaan performa latency dan throughput antara MySQL (SQL) dan MongoDB (NoSQL) dalam memproses transaksi data skala besar pada lingkungan cloud-native?
Hypothesis        : Arsitektur NoSQL (MongoDB) memiliki throughput yang lebih tinggi pada beban kerja write-heavy, sedangkan SQL (MySQL) lebih unggul dalam stabilitas latency pada query relasional yang kompleks.
Tipe Eksperimen   : [x] Comparison  [ ] Ablation  [ ] Parameter

Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control |Baseline Relasional (RDBMS)|MySQL|Dataset, Server, RAM, CPU, OS Identik|
| Treatment |Alternatif Dokumen (NoSQL)|MongoDB|Dataset, Server, RAM, CPU, OS Identik|

Fairness Checklist:
  [x] Dataset identik untuk semua kondisi
  [x] Preprocessing setara
  [x] Tuning effort setara
  [x] Environment identik
  [x] Metrik evaluasi sama

Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal    |Cache hit/Buffer warming saat pengujian|Melakukan Warm-up period 1000 query sebelum eksekusi|
| External    |Dataset buatan (Faker.js) tidak realistis|Menggunakan skema yang mereplikasi pola e-commerce|
| Construct   |Latensi jaringan ikut terukur dalam DB Response|Melakukan pengujian dalam isolated Docker Network|
| Conclusion  |Variansi hasil pada pengujian tunggal|Melakukan pengulangan (n=10) dan menggunakan median|

Statistical Plan:
  Uji statistik   : Independent t-test
  Justifikasi      : Membandingkan rata-rata dari dua kelompok sampel independen (MySQL vs MongoDB)
  Alpha            : 0.05
  Effect size min  : Cohen's d > 0.8
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** Sejauh mana perbedaan performa latency dan throughput antara MySQL dan MongoDB dalam memproses transaksi data skala besar pada lingkungan cloud-native?
**Tipe eksperimen:** [x] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control |MySQL 8.0 (Relational)| MySQL |4GB RAM, 2 vCPU, 100k-1jt record, Docker environment|
| Treatment |MongoDB 7.0 (NoSQL)| MongoDB |4GB RAM, 2 vCPU, 100k-1jt record, Docker environment|

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik | [x] ya | |
| Preprocessing setara | [x] ya |Data yang diuji bersumber dari seed yang sama melalui Faker.js.|
| Tuning effort setara | [x] ya |Normalisasi dilakukan pada tingkat aplikasi untuk masing-masing DBMS.|
| Environment identik | [x] ya |Menggunakan default configuration tanpa optimasi khusus (out-of-the-box).|
| Metrik evaluasi sama | [x] ya | Keduanya dijalankan dalam kontainer Docker dengan alokasi resource yang dipatok sama. |

**Ada yang tidak fair?** [ ] Ya / [x] Tidak
> Jika ya, bagaimana cara memperbaikinya? ________________

---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal |Data bias akibat alokasi memory|Menjamin alokasi resource (CPU/RAM) tetap sama di docker-compose|
| External |Hasil tidak berlaku untuk big data sebenarnya|Menguji dengan variasi dataset hingga 1 juta record|
| Construct |Pengukuran throughput terhambat bottleneck client|Memastikan workload generator tidak menjadi bottleneck dengan resource yang memadai|
| Conclusion |Adanya outlier yang merusak rata-rata|Menggunakan nilai median dan 95th percentile (P95)|

**Ancaman mana yang paling sulit dimitigasi?** External Validity
**Mengapa?**
> Karena setiap aplikasi e-commerce memiliki perilaku pengguna yang sangat unik. Apa yang kami simulasikan di lab mungkin tidak mencerminkan perilaku real-world di platform e-commerce yang sebenarnya.

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah baseline yang digunakan sudah merupakan standar industri yang setara dan teroptimasi, atau hanya versi lama yang sengaja dilemahkan?
2. Apakah hasil yang signifikan secara statistik didukung oleh effect size yang besar, atau hanya hasil dari sample size yang masif?
3. Jika metode ini diuji pada domain data yang berbeda (misal: bukan e-commerce tetapi IoT), apakah klaim keunggulannya tetap konsisten?
