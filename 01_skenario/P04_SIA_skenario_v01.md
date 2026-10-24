# Skenario, Aktor, dan Keputusan Pemodelan — Kasus SIA (Pertemuan 4)

Sistem Informasi Akademik, Layanan Hasil Studi.

## Skenario

Sistem Informasi Akademik melayani pengajuan KRS mahasiswa, validasi KRS, unduh bukti pengajuan, dan proses keputusan oleh dosen wali. Potongan model Pertemuan 3 tersebut tetap berlaku dan tetap digambar.

Pada Pertemuan 4, layanan diperluas. Mahasiswa dan dosen, sebagai civitas akademika, dapat melihat kalender akademik. Dosen dapat menginput nilai mata kuliah yang diampu. Mahasiswa dapat melihat KHS untuk semester yang nilainya sudah dipublikasikan. Admin akademik mengelola data mahasiswa dalam tiga bentuk: tambah, ubah, dan hapus data mahasiswa. Dua use case utama pada potongan model ini, Input Nilai Mata Kuliah dan Lihat KHS, ditunjukkan realisasinya oleh collaboration yang bersesuaian.

Model Pertemuan 4 bersifat kumulatif: diagram Pertemuan 3 disalin, seluruh elemennya dipertahankan, lalu elemen baru ditambahkan.

## Aktor

| Aktor | Status | Tujuan terhadap Sistem |
|---|---|---|
| Civitas Akademika | Umum, baru | Peran umum yang mewariskan fungsi melihat kalender akademik kepada Mahasiswa dan Dosen. |
| Mahasiswa | Khusus, tetap dari P3 | Mewarisi fungsi Civitas Akademika; mengajukan KRS, mengunduh bukti, melihat jadwal kuliah, dan melihat KHS. |
| Dosen | Khusus, baru | Mewarisi fungsi Civitas Akademika; menginput nilai mata kuliah yang diampu. |
| Admin Akademik | Tetap dari P2 | Mengelola jadwal kuliah dan mengelola data mahasiswa. |
| Dosen Wali | Tetap dari P3 | Memproses persetujuan atau penolakan KRS. |

## Keputusan Pemodelan dan Alasannya

1. **Civitas Akademika menjadi aktor umum bagi Mahasiswa dan Dosen.**
   Alasan: SIA-R07 memberi fungsi yang sama kepada keduanya, yaitu melihat kalender akademik. Civitas Akademika adalah nama peran, bukan orang baru, sehingga generalisasi menjelaskan kesamaan hak akses.

2. **Asosiasi ke SIA-UC07 digambar satu kali dari Civitas Akademika.**
   Alasan: Mahasiswa dan Dosen mewarisi fungsi tersebut. Menggambar garis dari keduanya akan menggandakan asosiasi yang sama dan melanggar aturan "gambar sekali dari aktor umum".

3. **Mahasiswa tetap memiliki garis langsung ke SIA-UC01, SIA-UC03, SIA-UC05, dan SIA-UC09.**
   Alasan: fungsi-fungsi itu memang hanya dimiliki Mahasiswa, bukan fungsi umum Civitas Akademika. SIA-UC01 berasal dari Pertemuan 2; SIA-UC03 dan SIA-UC05 dari Pertemuan 3; SIA-UC09 baru pada Pertemuan 4.

4. **Dosen memiliki garis langsung ke SIA-UC08.**
   Alasan: hanya dosen yang menginput nilai, dan hanya untuk mata kuliah yang diampu (SIA-R08). Fungsi ini tidak diwariskan dari Civitas Akademika.

5. **SIA-UC10 Kelola Data Mahasiswa menjadi use case umum bagi SIA-UC11, SIA-UC12, dan SIA-UC13.**
   Alasan: SIA-R11 menyebut tiga bentuk khusus dengan perilaku berbeda (menambah, mengubah, menghapus). Ketiganya adalah jenis nyata dari pengelolaan data mahasiswa.

6. **Admin Akademik dihubungkan ke SIA-UC10, bukan ke ketiga use case khusus.**
   Alasan: admin memakai fungsi umum pengelolaan data mahasiswa. Menghubungkan aktor ke setiap elips khusus akan membuat asosiasi berlebihan.

7. **Relasi Pertemuan 3 disalin tanpa perubahan.**
   Alasan: `«include»` SIA-UC03→SIA-UC04 dan `«extend»` SIA-UC05→SIA-UC03 beserta condition dan extension point adalah elemen P3 yang harus tetap ada. Keduanya tidak boleh diganti dengan generalisasi.

8. **Dosen Wali tetap dihubungkan ke SIA-UC06.**
   Alasan: hubungan ini diambil dari diagram P3, bukan ditebak. Dosen Wali tidak memperoleh fungsi baru pada P4.

9. **Collaboration hanya dibuat untuk SIA-UC08 dan SIA-UC09.**
   Alasan: keduanya adalah dua use case utama pada potongan model ini (SIA-R12). Collaboration memakai ID `SIA-CO01`/`SIA-CO02` dan nama yang sama persis dengan use case yang direalisasikannya.

## Katalog Use Case (Gabungan)

| ID | Nama | Aktor Terkait | Sumber | Status |
|---|---|---|---|---|
| SIA-UC01 | Lihat Jadwal Kuliah | Mahasiswa | Pertemuan 2 | Tetap |
| SIA-UC02 | Kelola Jadwal Kuliah | Admin Akademik | Pertemuan 2 | Tetap |
| SIA-UC03 | Ajukan KRS | Mahasiswa | SIA-R03 | Tetap; includes SIA-UC04 |
| SIA-UC04 | Validasi KRS | Sistem (dipanggil SIA-UC03) | SIA-R04 | Tetap; included oleh SIA-UC03 |
| SIA-UC05 | Unduh Bukti Pengajuan KRS | Mahasiswa | SIA-R05 | Tetap; extend dari SIA-UC03 |
| SIA-UC06 | Proses Keputusan KRS | Dosen Wali | SIA-R06 | Tetap |
| SIA-UC07 | Lihat Kalender Akademik | Civitas Akademika | SIA-R07 | Baru |
| SIA-UC08 | Input Nilai Mata Kuliah | Dosen | SIA-R08 | Baru; direalisasikan SIA-CO01 |
| SIA-UC09 | Lihat KHS | Mahasiswa | SIA-R09 | Baru; direalisasikan SIA-CO02 |
| SIA-UC10 | Kelola Data Mahasiswa | Admin Akademik | SIA-R10, SIA-R11 | Baru; UMUM bagi UC11–UC13 |
| SIA-UC11 | Tambah Data Mahasiswa | Admin Akademik (melalui SIA-UC10) | SIA-R11 | Baru; KHUSUS dari SIA-UC10 |
| SIA-UC12 | Ubah Data Mahasiswa | Admin Akademik (melalui SIA-UC10) | SIA-R11 | Baru; KHUSUS dari SIA-UC10 |
| SIA-UC13 | Hapus Data Mahasiswa | Admin Akademik (melalui SIA-UC10) | SIA-R11 | Baru; KHUSUS dari SIA-UC10 |

### Perbedaan Perilaku Use Case Khusus

- **Tambah Data Mahasiswa** menghasilkan data mahasiswa baru.
- **Ubah Data Mahasiswa** menghasilkan data mahasiswa yang berubah.
- **Hapus Data Mahasiswa** menghasilkan data mahasiswa yang dihapus, hanya jika mahasiswa tidak memiliki data akademik aktif.

## Collaboration

| ID | Nama (sama persis dengan use case) | Merealisasikan |
|---|---|---|
| SIA-CO01 | Input Nilai Mata Kuliah | SIA-UC08 |
| SIA-CO02 | Lihat KHS | SIA-UC09 |

Alasan: keduanya adalah dua use case utama pada potongan model ini. Collaboration lain tidak digambar.

## Verifikasi Relasi Diagram SIA

| No | Sumber | Jenis Relasi | Target |
|---:|---|---|---|
| 1 | Civitas Akademika | Asosiasi | SIA-UC07 |
| 2 | Mahasiswa | Asosiasi | SIA-UC01 |
| 3 | Mahasiswa | Asosiasi | SIA-UC03 |
| 4 | Mahasiswa | Asosiasi | SIA-UC05 |
| 5 | Mahasiswa | Asosiasi | SIA-UC09 |
| 6 | Admin Akademik | Asosiasi | SIA-UC02 |
| 7 | Admin Akademik | Asosiasi | SIA-UC10 |
| 8 | Dosen | Asosiasi | SIA-UC08 |
| 9 | Dosen Wali | Asosiasi | SIA-UC06 |
| 10 | Mahasiswa | Generalisasi | Civitas Akademika |
| 11 | Dosen | Generalisasi | Civitas Akademika |
| 12 | SIA-UC11 | Generalisasi | SIA-UC10 |
| 13 | SIA-UC12 | Generalisasi | SIA-UC10 |
| 14 | SIA-UC13 | Generalisasi | SIA-UC10 |
| 15 | SIA-UC03 | `«include»` | SIA-UC04 |
| 16 | SIA-UC05 | `«extend»` | SIA-UC03 |
| 17 | SIA-CO01 | Realisasi | SIA-UC08 |
| 18 | SIA-CO02 | Realisasi | SIA-UC09 |

Pemeriksaan tambahan:

- [x] Tidak ada garis Mahasiswa→SIA-UC07; fungsi kalender diwarisi dari Civitas Akademika.
- [x] Tidak ada asosiasi Admin Akademik ke SIA-UC11/SIA-UC12/SIA-UC13.
- [x] Semua aktor berada di luar batas sistem; semua use case dan collaboration berada di dalamnya.
- [x] Nama collaboration sama persis dengan nama use case yang direalisasikannya.
- [x] Tidak ada garis dari aktor ke collaboration.
- [x] Tidak ada pasangan use case yang memakai dua jenis relasi sekaligus.
