# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question: Sejauh mana perbedaan performa latency dan throughput antara MySQL (SQL) dan MongoDB (NoSQL) dalam memproses transaksi data skala besar pada lingkungan cloud-native?

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
|Jenis DBMS| IV   |Arsiktektur Basis Data|Perbandingan SQL vs NoSQL|Nominal|-|Konfigurasi sistem|Menentukan paradigma data yang dibandingkan|
|Latency| DV   |Kecepatan Respon|Average Response Time|Ratio|ms|Benchmarking tool (JMeter/K6)|Indikator utama performa real-time|
|Throughtput| DV   |Kapasistas distem|Requests Per Second|Ratio|RPS|Benchmarking tool|Indikator skalabilitas dan beban kerja|
|Skala Data| CV   |Volume data|Jumlah Record|Ratio|data point|Penambahan entri dataset|Menjaga konsistensi beban kerja|

Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  [x] Setiap langkah terdokumentasi
  [x] Tidak ada "lompatan logis"
  [x] Metrik mengukur apa yang dimaksud (construct validity)
```

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** __________________________________________________

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
| Jenis DBMS | *IV* | Paradigma basis data |MySQL vs MongoDB| Nominal | - |
| Waktu respon | DV | Kecepatan akses data |Mean Response Time|Ratio|Ms|
| Jumlah transaksi | DV | Kapasitas olah data |Throughput (RPS)|Ratio|RPS|
| Spesifikasi server | CV | Insfrastruktur fisik |CPU, RAM, Network|Ratio |GHz, GB|

**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [x] Tidak
> Jika ya, di mana? ____________________________________

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | 5 |Latency dan throughput adalah standar industri untuk performa DBMS|
| Sensitive | 4 |Metrik ini mampu menangkap perubahan kecil saat beban data meningkat|
| Feasible | 5 |Data mudah dikumpulkan otomatis menggunakan tool benchmarking seperti K6|

**Apakah perlu secondary metric?** [x] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? Secondary metric: Error Rate (%). Mengapa: Untuk memastikan bahwa performa cepat tidak didapatkan karena kueri yang gagal/error.

**Contoh kasus ceiling effect untuk metrik ini:**
> Ketika latency mencapai batas minimal hardware (misal < 0.1ms), peningkatan efisiensi kueri tidak akan terlihat lagi karena dibatasi oleh latensi jaringan (network overhead).

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | *Apakah semua data point terkumpul?* |Ya, semua log tersimpan| Automated logging ke database terpisah |
| Consistency | *Apakah ada kontradiksi internal?* |Mungkin terjadi jitter| Menggunakan median dan outlier removal |
| Validity | *Apakah benar-benar mengukur yang dimaksud?* |Ya, latency adalah awaktu murni| Isolasi environment dari proses background |
| Representativeness | *Apakah sampel mewakili populasi target?* |Ya, dataset simulasi e-cmemerce| Menggunakan dataset yang bervariasi (read/write mix) |

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Memilih metrik setelah melihat data (p-hacking) adalah praktik tidak etis karena peneliti secara sengaja mencari "signifikansi" atau hasil yang bagus dengan mengubah metrik yang dipakai, bukan menguji hipotesis awal. Eksplorasi data yang sah dilakukan untuk memahami karakteristik data sebelum pengujian, sedangkan p-hacking dilakukan untuk memaksa hasil agar sesuai dengan keinginan peneliti. Dalam riset yang ketat, metrik utama wajib didaftarkan sebelum eksperimen dimulai (pre-registration).
