## A. Kasus LAB — Peminjaman Peralatan Laboratorium

### A.1 Uji Konsistensi

| Situasi | Hasil |
|---|---|
| Alat tersedia dan tidak mencetak | Konsisten. `LAB-UC03` menjalankan `LAB-UC04`, dan `<<extend>>` tidak aktif. Pengajuan disimpan dengan status *Menunggu keputusan*. |
| Alat tidak tersedia | Konsisten. `LAB-UC04` tetap berjalan, dan *extension point* tidak tercapai. Data tidak disimpan. |
| Alat tersedia dan mahasiswa memilih mencetak | Konsisten. `LAB-UC05` memperluas `LAB-UC03` saat kondisi `[mahasiswa memilih cetak]`. Status pengajuan tetap sama. |

### A.2 Matriks Keterlacakan

| ID | Use Case | Status |
|---|---|---|
| `LAB-R01` | `LAB-UC01` | Diagram ada, deskripsi belum dibuat |
| `LAB-R02` | `LAB-UC02` | Diagram ada, deskripsi belum dibuat |
| `LAB-R03` | `LAB-UC03`, `LAB-UC04` | Terlacak lengkap |
| `LAB-R04` | `LAB-UC05` | Terlacak lengkap |
| `LAB-R05` | `LAB-UC06` | Terlacak lengkap |
| `LAB-R06` | `LAB-UC07` | Diagram ada, deskripsi belum dibuat |

## B. Kasus SIA — Pengajuan KRS

### B.1 Uji Konsistensi

| Situasi | Hasil |
|---|---|
| Validasi berhasil dan tidak mengunduh bukti | Konsisten. `SIA-UC01` menjalankan `SIA-UC02`, dan `SIA-UC03` tidak aktif. Data tersimpan dengan status *Menunggu persetujuan dosen wali*. |
| Validasi gagal | Konsisten. `SIA-UC02` tetap dipanggil, dan *extension point* tidak tercapai. Data tidak disimpan. |
| Validasi berhasil dan mahasiswa mengunduh bukti | Konsisten. `SIA-UC03` memperluas `SIA-UC01` saat kondisi `[mahasiswa memilih unduh]`. Status pengajuan tetap sama. |

### B.2 Matriks Keterlacakan

| ID | Use Case | Status |
|---|---|---|
| `SIA-R03` | `SIA-UC01` | Terlacak lengkap |
| `SIA-R04` | `SIA-UC02` | Terlacak lengkap |
| `SIA-R05` | `SIA-UC03` | Terlacak lengkap |
| `SIA-R06` | `SIA-UC04` | Terlacak lengkap |

## C. Checklist Evaluasi Model

| Indikator | LAB | SIA | Hasil |
|---|---:|---:|---|
| Aktor jelas | ✓ | ✓ | Terpenuhi |
| Use case sesuai kebutuhan | ✓ | ✓ | Terpenuhi |
| `<<include>>` sesuai | ✓ | ✓ | Terpenuhi |
| `<<extend>>` sesuai | ✓ | ✓ | Terpenuhi |
| *Extension point* jelas | ✓ | ✓ | Terpenuhi |
| Kondisi extend jelas | ✓ | ✓ | Terpenuhi |
| Pengajuan tetap tersimpan | ✓ | ✓ | Terpenuhi |
| Prasyarat dibedakan | ✓ | ✓ | Terpenuhi |
| Alur gagal dijelaskan | ✓ | ✓ | Terpenuhi |
| ID dan nama konsisten | ✓ | ✓ | Terpenuhi |
| File diagram bisa diedit | ✓ | ✓ | Terpenuhi |
| File gambar sesuai versi | ✓ | ✓ | Terpenuhi |
| Kebutuhan yang belum ada ditandai | ✓ | ✓ | Terpenuhi |

## D. Log Review

| No | Kasus | Temuan | Perbaikan |
|---:|---|---|---|
| 1 | SIA | Panah `<<extend>>` berlawanan arah pada draf awal | Arah panah diperbaiki ke `SIA-UC03` → `SIA-UC01` |
| 2 | LAB | Kondisi `extend` belum ditulis pada diagram | Ditambahkan `condition: [mahasiswa memilih cetak]` |

