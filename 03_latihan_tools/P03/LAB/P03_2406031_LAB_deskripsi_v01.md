# Deskripsi Use Case: Sistem Informasi Peminjaman dan Pengembalian Peralatan Laboratorium Kampus

---

## LAB-UC03: Ajukan peminjaman

| Bagian | Isi |
|--------|-----|
| **ID dan nama** | LAB-UC03 — Ajukan peminjaman |
| **Sumber kebutuhan** | LAB-R03, LAB-R04 |
| **Tujuan** | Menghasilkan pengajuan peminjaman yang tersimpan dengan status Menunggu keputusan |
| **Aktor utama** | Mahasiswa |
| **Aktor pendukung** | — |
| **Pemicu** | Mahasiswa memilih fungsi pengajuan peminjaman |
| **Prasyarat** | Mahasiswa telah terautentikasi; data peralatan tersedia |
| **Alur utama** | melihat tabel di bawah |
| **Alur alternatif/pengecualian** | 3a, 5a, 6a (lihat di bawah) |
| **Pascakondisi berhasil** | Pengajuan tersimpan dengan nomor pengajuan dan status Menunggu keputusan |
| **Pascakondisi gagal** | Tidak ada pengajuan baru yang berhasil tersimpan |
| **Aturan bisnis/asumsi** | Pengajuan yang diterima sistem berstatus Menunggu keputusan, bukan otomatis Disetujui. Pencetakan bukti bukan syarat keberhasilan pengajuan. |

### Tabel Alur Utama

| Langkah | Tindakan mahasiswa | Respons sistem |
|---------|-------------------|----------------|
| 1 | Membuka halaman pengajuan | Menampilkan formulir pengajuan peminjaman |
| 2 | Memilih alat, jumlah, rentang waktu, dan tujuan peminjaman | Menampung isian yang dimasukkan |
| 3 | Mengirim pengajuan | Memeriksa kelengkapan data |
| 4 | — | Menjalankan **LAB-UC04 (Periksa ketersediaan)** |
| 5 | — | Jika ketersediaan terpenuhi, menyimpan pengajuan dan menampilkan nomor pengajuan |
| 6 | Melihat halaman konfirmasi | Menampilkan nomor pengajuan dan status; mencapai *extension point* **Bukti pengajuan tersedia** |
| 7 | Mengakhiri pengajuan | Menutup proses pengajuan |

### Alur Alternatif / Pengecualian

- **3a. Data tidak lengkap.** Jika pada langkah 3 data yang dimasukkan tidak lengkap, sistem menolak pengiriman dan menampilkan pesan kelengkapan yang harus diperbaiki. Pengajuan tidak sampai ke tahap penyimpanan.
- **5a. Alat tidak tersedia.** Jika pada langkah 5 hasil LAB-UC04 menunjukkan alat tidak tersedia untuk rentang waktu yang diminta, sistem tidak menyimpan pengajuan. Mahasiswa dapat mengubah pilihan atau membatalkan.
- **6a. Mahasiswa memilih mencetak bukti.** Jika pada langkah 6 mahasiswa memilih mencetak bukti, sistem menjalankan **LAB-UC05 (Cetak bukti pengajuan)** lalu kembali ke langkah 7.

### Include, Extension Point, Extend

- **Include:** LAB-UC04 (Periksa ketersediaan) — dipanggil pada langkah 4.
- **Extension point:** **Bukti pengajuan tersedia**, terletak pada langkah 6 (halaman konfirmasi).
- **Extend:** LAB-UC05 (Cetak bukti pengajuan) jika kondisi **[mahasiswa memilih mencetak]** terpenuhi pada extension point.

---

## LAB-UC04: Periksa ketersediaan

| Bagian | Isi |
|--------|-----|
| **ID dan nama** | LAB-UC04 — Periksa ketersediaan |
| **Sumber kebutuhan** | LAB-R03 |
| **Tujuan** | Memvalidasi ketersediaan alat, jumlah, dan rentang waktu yang diminta dalam pengajuan |
| **Aktor utama** | Sistem (dieksekusi sebagai bagian dari LAB-UC03) |
| **Aktor pendukung** | — |
| **Pemicu** | Mahasiswa mengirim pengajuan (langkah 3 LAB-UC03) |
| **Prasyarat** | Data peralatan tersedia di sistem |
| **Alur utama** | Sistem memeriksa ketersediaan alat, jumlah, dan rentang waktu yang diminta |
| **Alur alternatif/pengecualian** | Jika alat tidak tersedia untuk rentang waktu yang diminta |
| **Pascakondisi berhasil** | Ketersediaan alat terkonfirmasi; pengajuan dapat diteruskan ke penyimpanan |
| **Pascakondisi gagal** | Ketersediaan tidak terpenuhi; pengajuan tidak disimpan |
| **Aturan bisnis/asumsi** | Pengajuan dengan peralatan tidak tersedia tidak disimpan sebagai pengajuan berhasil. |

### Tabel Alur Utama

| Langkah | Tindakan sistem | Hasil |
|---------|----------------|-------|
| 1 | Menerima permintaan pemeriksaan: alat, jumlah, rentang waktu | — |
| 2 | Memeriksa ketersediaan alat pada rentang waktu yang diminta | Tersedia / tidak tersedia |
| 3 | Mengembalikan hasil pemeriksaan | Layak dipinjam / tidak layak |

### Alur Alternatif

- **2a. Alat tidak tersedia.** Jika alat tidak tersedia untuk jumlah atau rentang waktu yang diminta, sistem mengembalikan hasil "tidak tersedia". Pengajuan tidak disimpan (lihat LAB-UC03 langkah 5a).

---

## LAB-UC05: Cetak bukti pengajuan

| Bagian | Isi |
|--------|-----|
| **ID dan nama** | LAB-UC05 — Cetak bukti pengajuan |
| **Sumber kebutuhan** | LAB-R04 |
| **Tujuan** | Mahasiswa memperoleh bukti cetakan atas pengajuan yang telah tersimpan |
| **Aktor utama** | Mahasiswa |
| **Aktor pendukung** | — |
| **Pemicu** | Mahasiswa memilih mencetak bukti pada halaman konfirmasi pengajuan (extension point LAB-UC03) |
| **Prasyarat** | Pengajuan telah tersimpan; halaman konfirmasi pengajuan tampil |
| **Alur utama** | Mahasiswa memilih cetak → sistem mencetak/menampilkan bukti pengajuan |
| **Alur alternatif/pengecualian** | Pencetakan gagal |
| **Pascakondisi berhasil** | Bukti pengajuan berhasil dicetak/ditampilkan |
| **Pascakondisi gagal** | Bukti tidak tercetak, namun pengajuan tetap tersimpan dengan status Menunggu keputusan |
| **Aturan bisnis/asumsi** | Pencetakan bukti bukan syarat keberhasilan pengajuan. Pengajuan tetap berhasil tanpa pencetakan. |

### Tabel Alur Utama

| Langkah | Tindakan mahasiswa | Respons sistem |
|---------|-------------------|----------------|
| 1 | Memilih opsi cetak bukti pada halaman konfirmasi | Memproses permintaan pencetakan |
| 2 | — | Mencetak atau menampilkan bukti pengajuan |

### Alur Alternatif

- **1a. Pencetakan gagal.** Jika sistem gagal mencetak bukti (mis. masalah perangkat keras printer), sistem menampilkan pesan kesalahan. Pengajuan tetap tersimpan; mahasiswa dapat mencoba lagi atau mengabaikan.
