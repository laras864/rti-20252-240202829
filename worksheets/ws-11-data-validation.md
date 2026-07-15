# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [x] Semua 5 jurnal telah dianalisis sesuai kriteria
  [x] Matriks ekstraksi data terisi lengkap untuk semua parameter (Latency, Throughput, Load).\
  [x] Tidak ada jurnal yang hilang dalam pemetaan
  Missing: 0 dari 5 data paper

Format Consistency:
  [x] Semua data diekstraksi ke dalam format matriks yang seragam (Excel/CSV)
  [x] Definisi metrik konsisten (misal: semua satuan latency dikonversi ke milidetik)
  [x] Skala pengukuran (misal: "tinggi/rendah" atau numerik) diseragamkan

Range & Logic:
  [x] Rentang tahun literatur sesuai (2022-2026).
  [x] Tidak ada temuan yang secara logika bertentangan dengan arsitektur dasar DBMS tanpa penjelasan.
  [x] Metrik yang diambil masuk akal dalam konteks cloud-native.
  Anomali ditemukan: Variasi hasil pada P3 karena environment pengujian yang sangat spesifik (skala kecil)

Cross-Validation:
  [x] Temuan P1 didukung oleh P4 mengenai write-heavy throughput.
  [x] Konsistensi trend antar paper terjaga sesuai teori arsitektur basis data.

Keputusan:
  [x] Data siap analisis (Sintesis siap dibuat).
```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| paper id | juernal  | status ekstrasi | Missing | Alasan |
|----------|-----------------|-------------|---------|--------|
| P1 | Putra et al. | lengkap | - | - |
| P2 | Hilman et al. | lengkap | - | - |
| P3 | Ilham et al. | lengkap | - | - |
| P4 | Saputra et al. | lengkap | - | - |
| P5 | Avrylya et al. | lengkap | - | - |

**Total expected:** 5 | **Total actual:** 5 | **Missing:** 0

---

## Latihan 2 — Anomaly Investigation

Dalam SLR, anomali adalah paper yang memberikan hasil "berlawanan" atau "tidak biasa" dibanding paper lainnya.
| paper | hasil temuan | Kemungkinan penyebab | Keputuan |
|-----|-------------|-------------|-------------|
| P3 | MongoDB performa rendah | Environment (skala kecil/hanya 1 node) | Dokumentasikan sebagai limitasi single-node. | 

**Investigasi:**
> Mengapa P3 berbeda? Setelah dianalisis, P3 menggunakan environment yang berbeda (lokal/non-cloud), sementara paper lain (P1, P2, P4) menggunakan cloud-native. Ini bukan anomali buruk, melainkan temuan tentang sensitivitas skala infrastruktur.
---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 100% data terkumpul
**2. Format:** [x] Konsisten / [ ] Ada inkonsistensi: ____
**3. Range check :** semua paper berada di rentang 2022-2026 sesuai kriteria
**4. Logic check:** [x] Parameter sesuai plan / [ ] Ada ketidaksesuaian: ____

**Kesimpulan:** [x] Data siap analisis / [ ] Perlu tindakan: ____

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> Data yang "benar" adalah apa yang tertulis di paper. Data yang "dipercaya" adalah data yang setelah divalidasi memiliki konteks metodologi yang jelas dan tidak bias. Jurnal peer-reviewed menjamin kualitas riset, namun tidak menjamin bahwa hasilnya berlaku untuk semua skenario. Validasi formal diperlukan agar kita tidak salah melakukan generalisasi hasil. Contoh: Kita tidak boleh mengklaim "MongoDB selalu lebih cepat" hanya karena 1 paper menyebutkan demikian, tanpa melihat apakah environment yang digunakan sama atau tidak dengan konteks riset kita.
