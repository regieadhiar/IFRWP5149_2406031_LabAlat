# Deskripsi Use Case — Kasus LAB (Pertemuan 4)

Sistem Informasi Peminjaman dan Pengembalian Peralatan Laboratorium Kampus.

Dokumen ini melengkapi katalog Pertemuan 4. Use case Pertemuan 3 yang tidak berubah tetap memakai deskripsi P3.

---

## LAB-UC11: Catat Pengembalian Peralatan

| Bagian | Isi |
|---|---|
| **ID dan nama** | LAB-UC11 — Catat Pengembalian Peralatan |
| **Sumber kebutuhan** | LAB-R09, LAB-R10 |
| **Tujuan** | Pengembalian tercatat; status peminjaman dan kondisi peralatan diperbarui |
| **Aktor utama** | Petugas Laboratorium |
| **Aktor pendukung** | — |
| **Pemicu** | Petugas memilih fungsi pengembalian dan memilih peminjaman yang dikembalikan |
| **Prasyarat** | Petugas telah terautentikasi; peminjaman yang dipilih berstatus **Dipinjam** |
| **Alur utama** | melihat tabel di bawah |
| **Alur alternatif/pengecualian** | A1, A2, A3 (lihat di bawah) |
| **Pascakondisi berhasil** | Pengembalian tercatat dengan tanggal kembali dan kondisi peralatan; status peminjaman menjadi **Selesai** |
| **Pascakondisi gagal** | Tidak ada pengembalian baru yang tercatat; status peminjaman tidak berubah |
| **Aturan bisnis/asumsi** | Pengembalian hanya untuk peminjaman berstatus **Dipinjam**. Kondisi peralatan bernilai **Baik**, **Rusak Ringan**, atau **Rusak Berat**. Keterlambatan dan denda belum dimodelkan (lihat Pertanyaan Terbuka). |
| **Include** | LAB-UC12 Periksa Kondisi Peralatan — dijalankan pada langkah 4 |
| **Generalisasi** | — (LAB-UC11 bukan use case khusus maupun use case umum; tidak ada relasi generalisasi) |
| **Collaboration** | LAB-CO02 Catat Pengembalian Peralatan — merealisasikan LAB-UC11 |

### Tabel Alur Utama

| Langkah | Tindakan Petugas Laboratorium | Respons Sistem |
|---|---|---|
| 1 | Memilih peminjaman yang akan dikembalikan | Menampilkan data peminjaman dan statusnya |
| 2 | Mengonfirmasi peralatan dan jumlah yang dikembalikan | Menerima konfirmasi |
| 3 | — | Memeriksa bahwa status peminjaman adalah **Dipinjam** |
| 4 | — | Menjalankan **LAB-UC12 (Periksa Kondisi Peralatan)**: memeriksa dan mencatat kondisi peralatan |
| 5 | Menyimpan catatan pengembalian | Menyimpan tanggal kembali dan kondisi; mengubah status peminjaman menjadi **Selesai** |
| 6 | Melihat konfirmasi | Menampilkan ringkasan pengembalian |

### Alur Alternatif / Pengecualian

- **A1 (langkah 3): status bukan Dipinjam.** Jika status peminjaman adalah **Menunggu Keputusan** atau **Ditolak**, sistem menolak pencatatan dan menampilkan status saat ini. Pascakondisi gagal berlaku: tidak ada pengembalian baru yang tercatat dan status peminjaman tidak berubah.
- **A2 (langkah 4): kondisi Rusak Ringan atau Rusak Berat.** Sistem tetap menyimpan pengembalian, menandai kondisi tersebut pada data peralatan, dan pengembalian tetap tercatat. Tidak ada denda otomatis.
- **A3 (langkah 2): jumlah peralatan tidak sesuai.** Sistem meminta petugas memeriksa ulang jumlah. Tidak ada data yang disimpan sampai jumlah dikoreksi.

### Uji Konsistensi Diagram dan Deskripsi

| Situasi | Yang diharapkan | Status |
|---|---|---|
| Peminjaman berstatus Dipinjam, kondisi Baik | LAB-UC11 dan LAB-UC12 berjalan; status menjadi Selesai | Konsisten |
| Peminjaman berstatus Menunggu Keputusan atau Ditolak | LAB-UC11 ditolak pada langkah 3; LAB-UC12 tidak berjalan; status tidak berubah | Konsisten |
| Peminjaman berstatus Dipinjam, kondisi Rusak Ringan/Berat | LAB-UC11 dan LAB-UC12 tetap berjalan; kondisi tercatat; status menjadi Selesai | Konsisten |
| Jumlah peralatan tidak sesuai | Sistem meminta koreksi; tidak ada data tersimpan | Konsisten |

### Catatan Pemodelan

- **Generalisasi** tidak dipakai pada LAB-UC11. Use case ini adalah fungsi utama petugas, bukan bentuk khusus dari use case lain, sehingga baris Generalization sengaja diisi "—". Memaksakan generalisasi di sini akan melanggar aturan bahwa use case khusus harus merupakan jenis nyata dari use case umum.
- **Collaboration** LAB-CO02 diberi nama sama persis dengan use case yang direalisasikannya. Realisasi digambar sebagai garis putus-putus berujung segitiga kosong dari collaboration menuju LAB-UC11. Tidak ada aktor yang dihubungkan ke collaboration.
- **Include** LAB-UC12 bersifat wajib karena pemeriksaan kondisi adalah bagian dari pencatatan pengembalian (LAB-R10), bukan perilaku opsional.
