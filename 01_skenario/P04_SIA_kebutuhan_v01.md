# Kebutuhan Pertemuan 4 — Kasus SIA

Sistem Informasi Akademik, Layanan Hasil Studi.

## Skenario

Sistem Informasi Akademik melayani pengajuan KRS mahasiswa, validasi KRS, unduh bukti pengajuan, dan proses keputusan oleh dosen wali. Potongan model Pertemuan 3 tersebut tetap berlaku dan tetap digambar.

Pada Pertemuan 4, layanan diperluas. Mahasiswa dan dosen, sebagai civitas akademika, dapat melihat kalender akademik. Dosen dapat menginput nilai mata kuliah yang diampu. Mahasiswa dapat melihat Kartu Hasil Studi (KHS) untuk semester yang nilainya sudah dipublikasikan. Admin akademik mengelola data mahasiswa dalam tiga bentuk: tambah, ubah, dan hapus data mahasiswa. Dua use case utama pada potongan model ini, Input Nilai Mata Kuliah dan Lihat KHS, ditunjukkan realisasinya oleh collaboration yang bersesuaian.

Model Pertemuan 4 bersifat kumulatif: diagram Pertemuan 3 disalin, seluruh elemennya dipertahankan, lalu elemen baru ditambahkan.

## Tabel Kebutuhan

| ID | Kebutuhan |
|---|---|
| SIA-R01 s.d. SIA-R06 | Kebutuhan pertemuan sebelumnya tetap berlaku dan tidak berubah arti. Kode baru dimulai dari R07 agar identitas R01–R06 tidak bergeser. |
| SIA-R07 | Mahasiswa dan Dosen, sebagai Civitas Akademika, dapat melihat kalender akademik. |
| SIA-R08 | Dosen dapat menginput nilai mata kuliah yang diampu. |
| SIA-R09 | Mahasiswa dapat melihat KHS untuk semester yang nilainya sudah dipublikasikan. |
| SIA-R10 | Admin Akademik dapat mengelola data mahasiswa. |
| SIA-R11 | Pengelolaan data mahasiswa memiliki tiga bentuk khusus: tambah, ubah, dan hapus data mahasiswa. |
| SIA-R12 | Model menunjukkan collaboration yang merealisasikan Input Nilai Mata Kuliah dan Lihat KHS. |

## Asumsi dan Batas Sistem

- Pengguna telah terautentikasi dan memiliki hak akses sesuai peran.
- Kalender akademik adalah agenda resmi institusi, bukan jadwal kuliah yang sudah dimodelkan pada Pertemuan 2.
- Nilai hanya dapat diinput oleh dosen yang mengampu mata kuliah tersebut.
- KHS hanya menampilkan nilai yang sudah dipublikasikan.
- Hapus Data Mahasiswa hanya berlaku untuk mahasiswa yang tidak memiliki data akademik aktif (aturan fiktif untuk latihan).
- KRS tetap berada di dalam diagram; relasi `«include»` dan `«extend»` dari Pertemuan 3 disalin.
- Pembayaran dan perancangan basis data berada di luar ruang lingkup.

## Uji Konsistensi

| Uji | Situasi | Hasil yang Diharapkan | Status |
|---|---|---|---|
| A | Mahasiswa membuka kalender akademik | Mahasiswa tidak memiliki garis langsung ke SIA-UC07, tetapi tetap dapat menjalankannya karena mewarisi asosiasi Civitas Akademika→SIA-UC07. Pada diagram tidak ada garis Mahasiswa→SIA-UC07. | Konsisten |
| B | Dosen yang bukan pengampu mencoba menginput nilai | Prasyarat gagal: dosen bukan pengampu mata kuliah. Sistem menolak, tidak ada nilai yang disimpan, dan pascakondisi gagal berlaku. Batasan ini dinyatakan pada prasyarat deskripsi SIA-UC08, bukan sebagai garis tambahan pada diagram. | Konsisten |
| C | Admin Akademik menghapus mahasiswa yang masih memiliki data akademik aktif | Aturan menolak penghapusan; tidak ada data yang dihapus. Batasan ini dinyatakan pada aturan bisnis SIA-UC13. | Konsisten |

## Catatan Sumber

- Berkas P3 SIA yang ada memuat potongan KRS saja: SIA-UC03 s.d. SIA-UC06 dan aktor Mahasiswa serta Dosen Wali. Elemen SIA-UC01 dan SIA-UC02 beserta aktor Admin Akademik berasal dari Pertemuan 2 dan dilibatkan kembali pada katalog kumulatif P4.
- Penomoran pada berkas deskripsi P3 masih memakai urutan lama (Ajukan KRS = UC01 dan seterusnya). Katalog P4 memakai penomoran jobsheet P4: UC01–UC02 dari P2, UC03–UC06 dari P3. Tidak ada use case yang dihapus atau diubah artinya; yang berubah hanya nomor urut katalog.
