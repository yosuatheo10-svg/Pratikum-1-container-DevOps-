# Laporan Praktikum Modul 1: Kontainerisasi Docker & Orkestrasi Multi-Tier

- **Nama Mahasiswa**: Yosua Theo
- **NIM**: 42430006
- **Prodi**: S1 Teknologi Informasi UNDIKNAS Denpasar
- **Branch Kerja**: lab1-2/yosua

---

## 1. Tabel Komparasi Eksperimen (Tahap 1 vs. Tahap 2 vs. Tahap 3)

| Parameter Pembanding | Tahap 1: Tanpa Docker | Tahap 2: Single-Stage | Tahap 3: Multi-Stage |
|---|---|---|---|
| **Kebutuhan Go di Host** | Wajib | Tidak wajib | Tidak wajib |
| **Ukuran Image** | - | ~840 MB | **26.1 MB** (< 100 MB) |
| **User Eksekusi** | User Laptop | root (uid=0) | appuser (uid=10001) |

---

## 2. Bukti Screenshot & Analisis

### Tahap 3: Optimasi Dockerfile Multi-Stage Build
![Ukuran Image Multi-Stage](docs/screenshots/sc03-tahap3-multistage.png)
![Log Ber-NIM](docs/screenshots/sc03-tahap3-multistage%20%282%29.png)

**Penjelasan Analisis Tahap 3**:
Pada tahap ini dilakukan optimasi Dockerfile menggunakan teknik Multi-Stage Build. Stage builder menggunakan `golang:alpine` untuk mengompilasi biner, sedangkan stage production hanya mengambil file biner tersebut ke dalam base image `alpine:3.20`. Hal ini memangkas ukuran image secara signifikan menjadi **26.1 MB** (berhasil memenuhi syarat < 100 MB). Keamanan juga ditingkatkan dengan menjalankan aplikasi menggunakan user non-root (`appuser` dengan UID 10001).
