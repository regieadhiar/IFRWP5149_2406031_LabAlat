# Skenario, Aktor, dan Keputusan Pemodelan — Kasus LAB (Pertemuan 4)

Sistem Informasi Peminjaman dan Pengembalian Peralatan Laboratorium Kampus.

## Skenario

Skenario berikut merupakan bahan latihan yang ditetapkan untuk jobsheet, bukan hasil pengumpulan kebutuhan laboratorium nyata. Skenario ini melanjutkan potongan model Pertemuan 3.

Selain mahasiswa, dosen juga meminjam peralatan laboratorium untuk kegiatan praktikum dan penelitian. Mahasiswa dan dosen sama-sama dapat melihat ketersediaan peralatan dan mengajukan peminjaman. Petugas laboratorium mengelola data peralatan: menambah peralatan baru, mengubah data peralatan, dan menghapus data peralatan yang tidak lagi dipakai. Setelah peminjaman disetujui dan alat diambil, petugas mencatat pengembalian peralatan. Pada saat mencatat pengembalian, petugas memeriksa dan mencatat kondisi peralatan. Dua use case utama pada potongan model ini, Ajukan Peminjaman dan Catat Pengembalian Peralatan, ditunjukkan realisasinya oleh collaboration yang bersesuaian.

Seluruh fungsi Pertemuan 3 tetap berlaku dan tetap digambar: pemeriksaan ketersediaan di dalam pengajuan, pencetakan bukti pengajuan oleh mahasiswa, proses keputusan peminjaman oleh petugas, dan laporan peminjaman untuk kepala laboratorium. Diagram Pertemuan 4 adalah diagram Pertemuan 3 yang ditambah, bukan diagram baru yang menggantikannya.

## Aktor

| Aktor | Status | Tujuan terhadap Sistem |
|---|---|---|
| Peminjam | Umum (general), baru pada Pertemuan 4 | Peran umum peminjam; mewariskan fungsi melihat ketersediaan dan mengajukan peminjaman kepada Mahasiswa dan Dosen. |
| Mahasiswa | Khusus dari Peminjam, tetap dari Pertemuan 3 | Mewarisi fungsi Peminjam; memiliki asosiasi sendiri ke Cetak Bukti Pengajuan. |
| Dosen | Khusus dari Peminjam, baru pada Pertemuan 4 | Mewarisi fungsi Peminjam untuk kegiatan praktikum dan penelitian. |
| Petugas Laboratorium | Tetap dari Pertemuan 3 | Mengelola data peralatan, memproses keputusan peminjaman, dan mencatat pengembalian. |
| Kepala Laboratorium | Tetap dari Pertemuan 3 | Melihat laporan peminjaman. |

## Keputusan Pemodelan dan Alasannya

1. **Mahasiswa dan Dosen digeneralisasi menjadi Peminjam.**
   Alasan: keduanya memiliki fungsi yang sama, yaitu melihat ketersediaan peralatan dan mengajukan peminjaman (LAB-R07). Peminjam adalah nama peran, bukan orang baru, sehingga generalisasi ini menjelaskan kesamaan fungsi, bukan sekadar mengelompokkan gambar.

2. **Asosiasi ke LAB-UC01 dan LAB-UC03 digambar satu kali dari Peminjam.**
   Alasan: asosiasi adalah hak akses peran. Karena Mahasiswa dan Dosen mewarisi fungsi Peminjam, menggambar garis yang sama dari kedua aktor khusus akan menggandakan hubungan yang sebenarnya satu. Garis dari aktor khusus hanya dipakai untuk fungsi yang memang hanya dimiliki aktor itu.

3. **Asosiasi Mahasiswa ke LAB-UC05 tetap langsung.**
   Alasan: hanya mahasiswa yang mencetak bukti pengajuan (LAB-R04). Fungsi ini bukan fungsi Peminjam, sehingga tidak boleh dinaikkan ke aktor umum dan tidak diwariskan ke Dosen.

4. **Segitiga kosong generalisasi menempel pada Peminjam.**
   Alasan: panah generalisasi selalu menunjuk dari aktor khusus ke aktor umum. Pada diagram, Mahasiswa berada di atas Peminjam (panah mengarah ke bawah) dan Dosen berada di bawah Peminjam (panah mengarah ke atas).

5. **LAB-UC02 Kelola Data Peralatan menjadi use case umum bagi LAB-UC08, LAB-UC09, dan LAB-UC10.**
   Alasan: LAB-R08 menyebut tiga bentuk khusus yang berbeda perilakunya (menambah, mengubah, menghapus). Ketiganya adalah jenis nyata dari pengelolaan data peralatan, bukan sekadar penggantian nama.

6. **Petugas Laboratorium dihubungkan ke LAB-UC02, bukan ke ketiga use case khusus.**
   Alasan: petugas memakai fungsi umum "kelola data peralatan"; ketiga bentuk khusus adalah pilihan perilaku di dalamnya. Menghubungkan petugas ke setiap elips akan membuat asosiasi berlebihan.

7. **LAB-UC11 Catat Pengembalian Peralatan memasukkan LAB-UC12 Periksa Kondisi Peralatan.**
   Alasan: LAB-R10 menetapkan pemeriksaan kondisi sebagai bagian wajib dari pencatatan pengembalian, sehingga hubungannya `«include»` (selalu dijalankan), bukan `«extend»` (opsional).

8. **Collaboration hanya dibuat untuk LAB-UC03 dan LAB-UC11.**
   Alasan: keduanya adalah dua use case utama pada potongan model ini (LAB-R11). Collaboration diberi nama persis sama dengan use case yang direalisasikannya dan memakai ID `LAB-CO01`/`LAB-CO02`, bukan ID use case.

9. **Kepala Laboratorium hanya dihubungkan ke LAB-UC07.**
   Alasan: LAB-R06 hanya memberi fungsi melihat laporan peminjaman. LAB-UC07 tidak memiliki relasi lain, sehingga tidak ada garis tambahan yang perlu digambar.

## Tabel 4.4 Perbandingan Model Pertemuan 3 dan Pertemuan 4

| Kelompok | Isi |
|---|---|
| Tetap sama dari Pertemuan 3 | Aktor Mahasiswa, Petugas Laboratorium, dan Kepala Laboratorium; use case LAB-UC01 sampai LAB-UC07; relasi `«include»` LAB-UC03 ke LAB-UC04; relasi `«extend»` LAB-UC05 ke LAB-UC03 lengkap dengan condition `[mahasiswa memilih cetak]` dan extension point `Bukti pengajuan tersedia`; asosiasi Petugas Laboratorium ke LAB-UC02 dan LAB-UC06; asosiasi Kepala Laboratorium ke LAB-UC07; asosiasi Mahasiswa ke LAB-UC05. |
| Berubah karena generalization aktor | Asosiasi ke LAB-UC01 dan LAB-UC03 yang pada Pertemuan 3 digambar dari Mahasiswa kini digambar satu kali dari Peminjam. Fungsi mahasiswa tidak hilang: mahasiswa mewarisinya dari Peminjam. Inilah satu-satunya perubahan garis pada diagram lama, dan alasannya adalah aturan generalization, bukan penghapusan fungsi. |
| Ditambah pada Pertemuan 4 | Aktor Peminjam dan Dosen; dua generalization aktor; use case LAB-UC08, LAB-UC09, LAB-UC10 beserta tiga generalization use case ke LAB-UC02; use case LAB-UC11 dan LAB-UC12 beserta relasi `«include»` di antara keduanya dan asosiasi Petugas Laboratorium ke LAB-UC11; collaboration LAB-CO01 dan LAB-CO02 beserta dua relasi realization. |

## Katalog Use Case (Gabungan)

| ID | Nama | Peran dalam Model | Sumber |
|---|---|---|---|
| LAB-UC01 | Lihat Ketersediaan Peralatan | Tetap; fungsi aktor umum Peminjam | LAB-R01, LAB-R07 |
| LAB-UC02 | Kelola Data Peralatan | Tetap; use case UMUM bagi UC08, UC09, UC10 | LAB-R02, LAB-R08 |
| LAB-UC03 | Ajukan Peminjaman | Tetap; fungsi Peminjam; includes UC04; direalisasikan LAB-CO01 | LAB-R03, LAB-R07 |
| LAB-UC04 | Periksa Ketersediaan | Tetap; included oleh UC03 | LAB-R03 |
| LAB-UC05 | Cetak Bukti Pengajuan | Tetap; extension bersyarat dari UC03 | LAB-R04 |
| LAB-UC06 | Proses Keputusan Peminjaman | Tetap; fungsi utama petugas | LAB-R05 |
| LAB-UC07 | Lihat Laporan Peminjaman | Tetap; fungsi utama kepala laboratorium | LAB-R06 |
| LAB-UC08 | Tambah Data Peralatan | Baru; KHUSUS dari UC02 | LAB-R08 |
| LAB-UC09 | Ubah Data Peralatan | Baru; KHUSUS dari UC02 | LAB-R08 |
| LAB-UC10 | Hapus Data Peralatan | Baru; KHUSUS dari UC02 | LAB-R08 |
| LAB-UC11 | Catat Pengembalian Peralatan | Baru; fungsi utama petugas; direalisasikan LAB-CO02; includes UC12 | LAB-R09 |
| LAB-UC12 | Periksa Kondisi Peralatan | Baru; included oleh UC11 | LAB-R10 |

### Perbedaan Perilaku Use Case Khusus

- **Tambah Data Peralatan** menghasilkan data peralatan baru.
- **Ubah Data Peralatan** menghasilkan data peralatan yang berubah.
- **Hapus Data Peralatan** menghasilkan data peralatan yang dihapus, hanya jika peralatan tidak sedang dipinjam dan tidak memiliki pengajuan aktif.

## Collaboration

| ID | Nama (sama persis dengan use case) | Merealisasikan |
|---|---|---|
| LAB-CO01 | Ajukan Peminjaman | LAB-UC03 |
| LAB-CO02 | Catat Pengembalian Peralatan | LAB-UC11 |

Alasan: keduanya adalah dua use case utama pada potongan model ini. Collaboration lain tidak digambar.

## Tabel 4.5 Verifikasi Relasi Diagram LAB

Diagram harus memuat **tepat 17 relasi** berikut, tidak lebih dan tidak kurang.

| No | Sumber | Jenis Relasi | Target |
|---:|---|---|---|
| 1 | Peminjam | Asosiasi | LAB-UC01 |
| 2 | Peminjam | Asosiasi | LAB-UC03 |
| 3 | Mahasiswa | Asosiasi | LAB-UC05 |
| 4 | Mahasiswa | Generalisasi | Peminjam |
| 5 | Dosen | Generalisasi | Peminjam |
| 6 | Petugas Laboratorium | Asosiasi | LAB-UC02 |
| 7 | Petugas Laboratorium | Asosiasi | LAB-UC06 |
| 8 | Petugas Laboratorium | Asosiasi | LAB-UC11 |
| 9 | Kepala Laboratorium | Asosiasi | LAB-UC07 |
| 10 | LAB-UC03 | `«include»` | LAB-UC04 |
| 11 | LAB-UC05 | `«extend»` | LAB-UC03 |
| 12 | LAB-UC08 | Generalisasi | LAB-UC02 |
| 13 | LAB-UC09 | Generalisasi | LAB-UC02 |
| 14 | LAB-UC10 | Generalisasi | LAB-UC02 |
| 15 | LAB-UC11 | `«include»` | LAB-UC12 |
| 16 | LAB-CO01 | Realisasi | LAB-UC03 |
| 17 | LAB-CO02 | Realisasi | LAB-UC11 |

Pemeriksaan tambahan:

- [x] Kepala Laboratorium hanya terhubung ke LAB-UC07, dan LAB-UC07 tidak memiliki relasi lain.
- [x] Tidak ada asosiasi warisan yang digambar ulang dari Mahasiswa atau Dosen ke LAB-UC01/LAB-UC03.
- [x] Tidak ada garis dari aktor mana pun ke collaboration.
- [x] Semua aktor berada di luar batas sistem; semua use case dan collaboration berada di dalamnya.
- [x] Nama collaboration sama persis dengan nama use case yang direalisasikannya.
- [x] Tidak ada pasangan use case yang memakai dua jenis relasi sekaligus.
