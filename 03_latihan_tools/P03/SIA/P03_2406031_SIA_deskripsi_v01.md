# Deskripsi Use Case: Sistem Informasi Akademik

---

## SIA-UC01: Ajukan KRS

| Bagian | Isi |
|--------|-----|
| **ID dan nama** | SIA-UC01 — Ajukan KRS |
| **Sumber kebutuhan** | SIA-R03 |
| **Tujuan** | Menghasilkan KRS yang tersimpan dengan status Menunggu persetujuan dosen wali |
| **Aktor utama** | Mahasiswa |
| **Aktor pendukung** | — |
| **Pemicu** | Mahasiswa memilih fungsi pengajuan KRS |
| **Prasyarat** | Mahasiswa telah terautentikasi; data mata kuliah, prasyarat, dan jadwal tersedia |
| **Alur utama** | melihat tabel di bawah |
| **Alur alternatif/pengecualian** | 3a (data tidak lengkap), 4a/5a (validasi gagal), 6a (unduh bukti) |
| **Pascakondisi berhasil** | KRS tersimpan dengan status Menunggu persetujuan dosen wali |
| **Pascakondisi gagal** | KRS tidak tersimpan |
| **Aturan bisnis/asumsi** | Validasi gagal menyebabkan pengajuan belum berhasil tersimpan. Unduh bukti bukan syarat keberhasilan pengajuan. KRS tersimpan belum berarti disetujui. |

### Tabel Alur Utama

| Langkah | Tindakan mahasiswa | Respons sistem |
|---------|-------------------|----------------|
| 1 | Membuka halaman pengajuan KRS | Menampilkan formulir pengajuan KRS |
| 2 | Memilih mata kuliah yang akan diambil | Menampung pemilihan mata kuliah |
| 3 | Mengirim KRS | Memeriksa kelengkapan data |
| 4 | — | Menjalankan **SIA-UC02 (Validasi KRS)** |
| 5 | — | Jika validasi berhasil, menyimpan KRS dengan status **Menunggu persetujuan dosen wali** dan menampilkan nomor/detail KRS |
| 6 | Melihat halaman konfirmasi | Menampilkan konfirmasi KRS tersimpan; mencapai *extension point* **Bukti pengajuan tersedia** |
| 7 | Mengakhiri pengajuan | Menutup proses pengajuan |

### Alur Alternatif / Pengecualian

- **3a. Data tidak lengkap.** Jika pada langkah 3 data yang dimasukkan tidak lengkap (mis. tidak ada mata kuliah yang dipilih), sistem menolak pengiriman dan meminta mahasiswa melengkapi data.
- **4a/5a. Validasi gagal.** Jika pada langkah 4–5 SIA-UC02 menghasilkan **tidak valid** (karena kelengkapan, prasyarat, atau benturan jadwal), sistem tidak menyimpan KRS. Mahasiswa dapat memperbaiki pilihan mata kuliah atau membatalkan pengajuan. Halaman konfirmasi tidak tampil, sehingga extension point untuk unduh bukti tidak tercapai.
- **6a. Mahasiswa memilih mengunduh bukti.** Jika pada langkah 6 mahasiswa memilih mengunduh bukti, sistem menjalankan **SIA-UC03 (Unduh bukti pengajuan KRS)** lalu kembali ke langkah 7.

### Include, Extension Point, Extend

- **Include:** SIA-UC02 (Validasi KRS) — dipanggil pada langkah 4.
- **Extension point:** **Bukti pengajuan tersedia**, terletak pada langkah 6 (halaman konfirmasi setelah KRS tersimpan).
- **Extend:** SIA-UC03 (Unduh bukti pengajuan KRS) jika kondisi **[mahasiswa memilih mengunduh bukti]** terpenuhi pada extension point.

---

## SIA-UC02: Validasi KRS

| Bagian | Isi |
|--------|-----|
| **ID dan nama** | SIA-UC02 — Validasi KRS |
| **Sumber kebutuhan** | SIA-R04 |
| **Tujuan** | Memvalidasi KRS sebelum penyimpanan; memastikan kelengkapan, prasyarat, dan tidak ada benturan jadwal |
| **Aktor utama** | Sistem (dieksekusi sebagai bagian dari SIA-UC01) |
| **Aktor pendukung** | — |
| **Pemicu** | Mahasiswa mengirim KRS (langkah 3 SIA-UC01) |
| **Prasyarat** | Data mata kuliah, prasyarat mata kuliah, dan jadwal kuliah tersedia di sistem |
| **Alur utama** | Sistem memeriksa kelengkapan, prasyarat mata kuliah, dan benturan jadwal; menghasilkan hasil valid atau tidak valid |
| **Alur alternatif/pengecualian** | Kegagalan pada tiap pemeriksaan menghasilkan tidak valid |
| **Pascakondisi berhasil** | KRS dinyatakan valid; pengajuan dapat diteruskan ke penyimpanan |
| **Pascakondisi gagal** | KRS dinyatakan tidak valid; pengajuan tidak tersimpan |
| **Aturan bisnis/asumsi** | Validasi gagal menyebabkan pengajuan belum berhasil tersimpan. Validasi adalah perilaku yang wajib disertakan dalam setiap pengajuan (bukan opsional). |

### Tabel Alur Utama

| Langkah | Tindakan sistem | Hasil |
|---------|----------------|-------|
| 1 | Memeriksa kelengkapan data KRS (apakah ada mata kuliah yang dipilih, form lengkap) | Lengkap / tidak lengkap |
| 2 | Memeriksa prasyarat mata kuliah untuk setiap kuliah yang dipilih | Prasyarat terpenuhi / tidak terpenuhi |
| 3 | Memeriksa benturan jadwal antar mata kuliah yang dipilih | Tidak ada benturan / ada benturan |
| 4 | Mengembalikan hasil keseluruhan | **Valid** (lanjut ke penyimpanan) atau **Tidak valid** (pengajuan gagal) |

### Alur Alternatif

- **1a. Kelengkapan tidak terpenuhi.** Jika data tidak lengkap (mis. tidak ada mata kuliah yang dipilih), sistem mengembalikan **tidak valid** dengan pesan kelengkapan. KRS tidak tersimpan.
- **2a. Prasyarat tidak terpenuhi.** Jika mahasiswa belum memenuhi prasyarat suatu mata kuliah, sistem mengembalikan **tidak valid** dengan pesan prasyarat. KRS tidak tersimpan.
- **3a. Benturan jadwal terdeteksi.** Jika terdapat mata kuliah dengan jadwal bertabrakan, sistem mengembalikan **tidak valid** dengan pesan benturan. KRS tidak tersimpan.

---

## SIA-UC03: Unduh bukti pengajuan KRS

| Bagian | Isi |
|--------|-----|
| **ID dan nama** | SIA-UC03 — Unduh bukti pengajuan KRS |
| **Sumber kebutuhan** | SIA-R05 |
| **Tujuan** | Mahasiswa memperoleh bukti pengajuan KRS dalam bentuk berkas yang dapat diunduh |
| **Aktor utama** | Mahasiswa |
| **Aktor pendukung** | — |
| **Pemicu** | Mahasiswa memilih mengunduh bukti pada halaman konfirmasi pengajuan (extension point SIA-UC01) |
| **Prasyarat** | KRS sudah tersimpan; halaman konfirmasi pengajuan tampil |
| **Alur utama** | Mahasiswa memilih unduh → sistem mengirim/menyediakan berkas bukti pengajuan |
| **Alur alternatif/pengecualian** | Unduhan gagal |
| **Pascakondisi berhasil** | Bukti pengajuan berhasil diunduh oleh mahasiswa |
| **Pascakondisi gagal** | Unduhan gagal, namun KRS tetap tersimpan dengan status Menunggu persetujuan dosen wali |
| **Aturan bisnis/asumsi** | Unduh bukti bukan syarat keberhasilan pengajuan. KRS tetap tersimpan meskipun unduhan gagal. |

### Tabel Alur Utama

| Langkah | Tindakan mahasiswa | Respons sistem |
|---------|-------------------|----------------|
| 1 | Memilih opsi unduh bukti pada halaman konfirmasi | Memproses permintaan unduhan |
| 2 | — | Menyediakan/mengirim berkas bukti pengajuan KRS |

### Alur Alternatif

- **1a. Unduhan gagal.** Jika sistem gagal menyediakan berkas unduhan (mis. masalah koneksi atau server), sistem menampilkan pesan kesalahan. KRS tetap tersimpan; mahasiswa dapat mencoba lagi.

---

## Uji Konsistensi Diagram dan Deskripsi SIA

| Situasi | Yang diharapkan | Status Konsistensi |
|---------|----------------|-------------------|
| a. Validasi berhasil, mahasiswa tidak mengunduh bukti | UC01 dan UC02 berjalan; KRS tersimpan (menunggu persetujuan); UC03 tidak berjalan | ✅ Konsisten |
| b. Validasi gagal | UC02 menghasilkan tidak valid; KRS tidak tersimpan; tidak sampai konfirmasi sehingga UC03 tidak tersedia | ✅ Konsisten |
| c. Validasi berhasil, mahasiswa memilih mengunduh bukti | Seperti (a), ditambah UC03 berjalan di extension point | ✅ Konsisten |

---

## SIA-UC04: Proses keputusan KRS

| Bagian | Isi |
|--------|-----|
| **ID dan nama** | SIA-UC04 — Proses keputusan KRS |
| **Sumber kebutuhan** | SIA-R06 |
| **Tujuan** | Menetapkan persetujuan atau penolakan terhadap KRS yang menunggu persetujuan, disertai catatan keputusan |
| **Aktor utama** | Dosen wali |
| **Aktor pendukung** | — |
| **Pemicu** | Dosen wali membuka KRS yang berstatus Menunggu persetujuan dosen wali |
| **Prasyarat** | KRS berstatus **Menunggu persetujuan dosen wali** |
| **Alur utama** | Dosen wali membuka KRS → meninjau → menetapkan persetujuan atau penolakan + catatan → sistem menyimpan keputusan |
| **Alur alternatif/pengecualian** | Penolakan (status Ditolak + catatan); kegagalan penyimpanan keputusan |
| **Pascakondisi berhasil (persetujuan)** | KRS berstatus **Disetujui** dengan catatan keputusan dari dosen wali |
| **Pascakondisi berhasil (penolakan)** | KRS berstatus **Ditolak** dengan catatan penolakan dari dosen wali |
| **Pascakondisi gagal** | Keputusan tidak tersimpan; status KRS tetap Menunggu persetujuan |
| **Aturan bisnis/asumsi** | KRS tersimpan belum berarti disetujui. Dosen wali memberikan catatan pada kedua hasil (persetujuan maupun penolakan). |

### Tabel Alur Utama

| Langkah | Tindakan dosen wali | Respons sistem |
|---------|--------------------|----------------|
| 1 | Membuka daftar KRS yang menunggu persetujuan | Menampilkan daftar KRS dengan status Menunggu persetujuan |
| 2 | Memilih dan membuka KRS tertentu | Menampilkan detail KRS (mata kuliah, kelengkapan, dll.) |
| 3 | Meninjau KRS | — |
| 4 | Menetapkan keputusan: **Setujui** atau **Tolak**, disertai catatan | Menyimpan keputusan dan catatan |
| 5 | — | Mengupdate status KRS menjadi **Disetujui** atau **Ditolak** sesuai keputusan |

### Alur Alternatif

- **4a. Penolakan.** Jika dosen wali memilih **Tolak**, sistem menyimpan status **Ditolak** bersama catatan penolakan. KRS tidak dapat diproses lebih lanjut tanpa pengajuan ulang (di luar ruang lingkup model ini).
- **4b. Gagal menyimpan keputusan.** Jika sistem gagal menyimpan keputusan (mis. masalah penyimpanan), sistem menampilkan pesan kesalahan. Status KRS tetap **Menunggu persetujuan dosen wali**; dosen wali dapat mencoba lagi.
