# Deskripsi Use Case — Kasus SIA (Pertemuan 4)

Sistem Informasi Akademik, Layanan Hasil Studi.

Dokumen ini melengkapi katalog Pertemuan 4. Use case Pertemuan 3 yang tidak berubah tetap memakai deskripsi P3.

---

## SIA-UC08: Input Nilai Mata Kuliah

| Bagian | Isi |
|---|---|
| **ID dan nama** | SIA-UC08 — Input Nilai Mata Kuliah |
| **Sumber kebutuhan** | SIA-R08 |
| **Tujuan** | Nilai mata kuliah yang diampu tersimpan dan siap ditampilkan pada KHS setelah dipublikasikan |
| **Aktor utama** | Dosen |
| **Aktor pendukung** | — |
| **Pemicu** | Dosen membuka fungsi input nilai untuk mata kuliah yang diampu |
| **Prasyarat** | Dosen telah terautentikasi dan merupakan dosen pengampu mata kuliah tersebut |
| **Alur utama** | melihat tabel di bawah |
| **Alur alternatif/pengecualian** | A1 (bukan dosen pengampu), A2 (nilai di luar rentang), A3 (data belum lengkap) |
| **Pascakondisi berhasil** | Nilai per mahasiswa tersimpan untuk mata kuliah yang diampu; nilai dapat ditampilkan pada KHS setelah dipublikasikan |
| **Pascakondisi gagal** | Tidak ada nilai baru yang tersimpan; nilai sebelumnya tidak berubah |
| **Aturan bisnis/asumsi** | Nilai hanya diinput oleh dosen pengampu. KHS hanya menampilkan nilai yang sudah dipublikasikan. Rentang nilai yang sah mengikuti aturan akademik yang berlaku. |
| **Generalisasi** | — (SIA-UC08 bukan use case khusus maupun use case umum; tidak ada relasi generalisasi) |
| **Collaboration** | SIA-CO01 Input Nilai Mata Kuliah — merealisasikan SIA-UC08 |

### Tabel Alur Utama

| Langkah | Tindakan Dosen | Respons Sistem |
|---|---|---|
| 1 | Memilih mata kuliah yang diampu | Menampilkan data mata kuliah dan daftar mahasiswa |
| 2 | Mengisi nilai setiap mahasiswa | Menerima isian nilai |
| 3 | Mengirim data nilai | Memeriksa kelengkapan dan rentang nilai |
| 4 | — | Menyimpan nilai untuk mata kuliah tersebut |
| 5 | Melihat konfirmasi | Menampilkan ringkasan nilai yang tersimpan |

### Alur Alternatif / Pengecualian

- **A1 (prasyarat): dosen bukan pengampu.** Jika dosen yang membuka fungsi bukan pengampu mata kuliah tersebut, prasyarat gagal. Sistem menolak akses, tidak ada nilai yang tersimpan, dan pascakondisi gagal berlaku.
- **A2 (langkah 3): nilai di luar rentang yang sah.** Sistem menolak nilai tersebut dan meminta dosen memperbaiki. Nilai yang tidak sah tidak disimpan; nilai lain yang sudah benar tetap dapat disimpan setelah diperbaiki.
- **A3 (langkah 3): data belum lengkap.** Jika masih ada mahasiswa yang belum memiliki nilai, sistem menolak pengiriman dan menampilkan daftar yang belum lengkap. Tidak ada nilai yang disimpan sampai data dilengkapi.

### Uji Konsistensi Diagram dan Deskripsi

| Situasi | Yang diharapkan | Status |
|---|---|---|
| Dosen pengampu menginput nilai yang sah | SIA-UC08 berjalan; nilai tersimpan; pascakondisi berhasil | Konsisten |
| Dosen bukan pengampu | Prasyarat gagal; akses ditolak; tidak ada nilai tersimpan | Konsisten |
| Nilai di luar rentang | Nilai ditolak; tidak tersimpan; dosen diminta memperbaiki | Konsisten |
| Data nilai belum lengkap | Pengiriman ditolak; tidak ada nilai tersimpan | Konsisten |

---

## SIA-UC09: Lihat KHS

| Bagian | Isi |
|---|---|
| **ID dan nama** | SIA-UC09 — Lihat KHS |
| **Sumber kebutuhan** | SIA-R09 |
| **Aktor utama** | Mahasiswa |
| **Prasyarat** | Mahasiswa telah terautentikasi |
| **Alur utama** | Mahasiswa memilih semester → sistem menampilkan KHS semester tersebut |
| **Pascakondisi berhasil** | KHS semester yang dipilih ditampilkan |
| **Pascakondisi gagal** | KHS tidak ditampilkan; tidak ada data yang berubah |
| **Aturan bisnis/asumsi** | KHS hanya menampilkan nilai yang sudah dipublikasikan. Nilai yang belum dipublikasikan tidak ditampilkan. |
| **Generalisasi** | — (SIA-UC09 bukan use case khusus maupun use case umum; tidak ada relasi generalisasi) |
| **Collaboration** | SIA-CO02 Lihat KHS — merealisasikan SIA-UC09 |

Deskripsi ringkas: mahasiswa memilih semester, sistem menampilkan KHS yang hanya berisi nilai terpublikasi. Jika nilai semester tersebut belum dipublikasikan, sistem menampilkan pesan bahwa KHS belum tersedia. Use case ini tidak mengubah data.

---

## Catatan Penomoran

Berkas deskripsi P3 memakai nomor lama (Ajukan KRS = SIA-UC01, Validasi KRS = SIA-UC02, Unduh Bukti = SIA-UC03, Proses Keputusan = SIA-UC04). Katalog P4 mengikuti penomoran jobsheet P4: SIA-UC01 dan SIA-UC02 berasal dari Pertemuan 2, sedangkan Ajukan KRS dan seterusnya menjadi SIA-UC03–SIA-UC06. Tidak ada use case yang dihapus atau diubah artinya.
