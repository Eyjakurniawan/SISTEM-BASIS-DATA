# Sistem Manajemen Arsip Surat dan Dokumen Digital
### Proyek implementasi basis data relasional untuk Sistem Manajemen Arsip Surat dan Dokumen Digital guna mengotomatisasi pencatatan surat, digitalisasi berkas akademik, serta pelacakan verifikasi dan disposisi.

# NAMA ANGGOTA KELOMPOK 7
## Eyja Kurniawan (2501020094)
## Yazira Sartika (2501020103)
## Raihan Parsa Ahza Hamizan (2501200104)
## Naufal Putra Azjril (2501020108)

# STUDI KASUS
Sistem Manajemen Arsip Surat dan Dokumen Digital merupakan sistem berbasis basis data yang dirancang untuk mengubah cara pengelolaan surat dan dokumen di Prodi Teknik Informatika yang tadinya serba manual/kertas menjadi serba digital dan otomatis menggunakan basis data (database). Jadi, mulai dari mahasiswa yang mau upload berkas, staf TU yang meriksa dan kasih nomor surat, dosen yang ngecek, sampai Kaprodi atau Dekan yang ngasih instruksi disposisi, semuanya tercatat langsung di dalam sistem secara real-time. Dengan sistem ini, berkas jadi lebih rapi, aman dari risiko hilang, dan kalau mau cari dokumen lama tinggal ketik aja tanpa perlu bongkar-bongkar lemari arsip lagi.

# LATAR BELAKANG DAN TUJUAN SISTEM
## Latar Belakang
Setiap harinya, Program Studi Teknik Informatika menerima dan mengeluarkan berbagai macam surat serta dokumen akademik, seperti Surat Keputusan (SK) Dosen, surat pengantar penelitian mahasiswa, berkas proposal, hingga draf skripsi final. Namun, saat ini proses pencatatan dan pengarsipan dokumen-dokumen tersebut masih dilakukan secara manual menggunakan buku besar atau disimpan secara terpisah di Google Drive pribadi milik staf. 
Sistem penyimpanan yang belum terpusat ini menimbulkan beberapa masalah utama: 
* Pencarian data lambat: Staf Tata Usaha (TU) membutuhkan waktu lama untuk mencari kembali dokumen fisik atau file digital yang terselip. 
* Risiko data hilang: Surat fisik rawan rusak atau hilang, dan file digital di drive pribadi berisiko terhapus. 
* Proses disposisi terhambat: Alur instruksi dari Ketua Prodi ke dosen terkait surat masuk seringkali lambat karena harus dilakukan secara manual atau melalui pesan teks biasa yang mudah tertumpuk. 
Oleh karena itu, diperlukan perancangan basis data yang terstruktur untuk membangun sistem manajemen arsip yang mampu mengintegrasikan seluruh data, mempermudah pencarian, serta menjaga keamanan dokumen penting di lingkungan program studi.

## Tujuan Sistem
Membuat rancangan basis data yang mampu mengintegrasikan data aktor utama (Mahasiswa, Staf TU, Dosen, dan Dekan/Kaprodi) beserta hak aksesnya masing-masing dalam sistem manajemen dokumen.
Mengotomatisasi Pencatatan Siklus Hidup Dokumen Membangun struktur tabel yang dapat merekam setiap perubahan status dokumen secara kronologis, mulai dari dokumen pertama kali diunggah (upload), diverifikasi oleh TU, diperiksa oleh Dosen, hingga diberi disposisi oleh Dekan/Kaprodi.
Mendukung Alur Kerja Pemeriksaan dan Disposisi Berjenjang Merancang relasi antar-tabel yang mampu mencatat data hasil pemeriksaan oleh Dosen serta lembar disposisi dari Dekan/Kaprodi, sehingga rekam jejak keputusan pimpinan terhadap dokumen tersebut tersimpan dengan baik.
Menghasilkan Query untuk Pelaporan dan Pemantauan Status (Tracking) Membuat perintah SQL (Query) spesifik untuk menghasilkan laporan operasional yang dibutuhkan pihak kampus, seperti:
•	Menampilkan daftar dokumen mahasiswa yang masih tertunda (pending) di meja Staf TU.
•	Menampilkan rekapitulasi dokumen yang sedang diperiksa atau didisposisikan oleh Dosen/Dekan.
•	Menyajikan laporan akhir mengenai jumlah dokumen yang berhasil diselesaikan (status: Selesai) dalam periode tertentu.

# IDENTIFIKASI AKTOR
1. Mahasiswa: Pengguna yang memiliki hak akses untuk mengunggah berkas pengajuan baru serta mengunduh dokumen akademik hasil validasi.
2. Staf TU: Verifikator awal yang bertugas memproses registrasi berkas masuk, menghapus dokumen yang salah input, memverifikasi kelayakan berkas, dan menginput nomor surat resmi jika berkas disetujui.
3. Dosen: Pemeriksa berkas akademis yang menerima notifikasi dokumen dari staf TU serta memberikan pembaruan status hasil pemeriksaan berkas.
4. Dekan / Kaprodi: Pimpinan tertinggi yang bertugas meninjau dokumen akhir serta memberikan catatan instruksi atau lembar disposisi resmi di dalam sistem.

# KEBUTUHAN FUNGSIONAL
1. Sistem harus dapat menyimpan data autentikasi login (username dan password) untuk Mahasiswa, Staf TU, Dosen, dan Dekan/Kaprodi.
2. Sistem harus dapat mencatat riwayat pengajuan dokumen yang diunggah oleh Mahasiswa beserta waktu unggahnya.
3. Sistem harus dapat memfasilitasi Staf TU untuk melakukan pencatatan nomor dokumen resmi pada berkas yang telah dinyatakan valid.
4. Sistem harus dapat menyimpan alasan penolakan berkas di dalam database apabila Staf TU mengubah status dokumen menjadi "Ditolak".
5. Sistem harus dapat memperbarui status dokumen secara dinamis (Pending, Diterima, Ditolak, Disetujui) di dalam tabel terkait.
6. Sistem harus dapat mencatat pengiriman notifikasi berkas masuk secara otomatis dari Staf TU ke Dosen Pemeriksa.
7. Sistem harus dapat menyimpan data hasil penilaian, komentar, atau catatan pemeriksaan dokumen yang dilakukan oleh Dosen.
8. Sistem harus dapat mencatat lembar disposisi dari Dekan/Kaprodi yang berisi instruksi kelanjutan berkas.
9. Sistem harus dapat menampilkan laporan operasional berupa jumlah berkas selesai dan berkas tertunda berdasarkan filter rentang tanggal tertentu melalui query SQL.
10. Sistem harus dapat membatasi hak akses unduh berkas agar dokumen internal prodi hanya bisa diakses oleh aktor yang berwenang.

# KEBUTUHAN DATA
### Tabel User
* `id_user` INT
* `nama` VARCHAR (50)
* `email` VARCHAR (50)
* `password` VARCHAR (50)
* `role` VARCHAR (20)

### Tabel Mahasiswa
* `nim` VARCHAR (15)
* `nama_mahasiswa` VARCHAR (50)
* `program_studi` VARCHAR (30)
* `id_user` INT

### Tabel Dosen
* `nidn` VARCHAR (15)
* `nama_dosen` VARCHAR (50)
* `jabatan` VARCHAR (40)
* `id_user` INT

### Tabel Staf TU
* `id_pegawai` VARCHAR (15)
* `nama_pegawai` VARCHAR (50)
* `id_user` INT

### Tabel Dokumen
* `id_dokumen` INT
* `nama_berkas` VARCHAR (100)
* `nomor_dokumen` VARCHAR (40)
* `tanggal_unggah` DATETIME
* `status_dokumen` VARCHAR (20)
* `catatan_penolakan` VARCHAR (200)
* `file_path` VARCHAR (200)
* `nim` VARCHAR(15)
* `id_pegawai` VARCHAR(15)

### Tabel Pemeriksaan
* `id_periksa` INT
* `id_dokumen` INT
* `nidn` VARCHAR (15)
* `tanggal_periksa` DATETIME
* `catatan_hasil_pemeriksaan` VARCHAR (200)

### Tabel Disposisi
* `id_disposisi` INT
* `id_dokumen` INT
* `id_user` INT
* `tanggal_disposisi` DATETIME
* `isi_instruksi_disposisi` VARCHAR (200)

# DIAGRAM PROSES (FLOWCHART)
<img width="825" height="1600" alt="WhatsApp Image 2026-06-13 at 9 02 38 PM" src="https://github.com/user-attachments/assets/71a90e42-c836-4589-9b91-3288ae45f876" />


# PEMBAGIAN TUGAS SETIAP ANGGOTA
1. Naufal (2501020108) = Bertugas dalam membuat studi kasus, latar belakang, serta tujuan sistem.
2. Yazira Sartika (2501020103) = Bertugas dalam membuat identifikasi aktor dan kebutuhan fungsional.
3. Raihan (2501020104) = Bertugas dalam membuat rancangan kebutuhan data.
4. Eyja Kurniawan (2501020094) = Bertugas dalam membuat diagram proses atau flowchart.

# LINK REPOSITORY GITHUB
https://github.com/Eyjakurniawan/SISTEM-BASIS-DATA.git

---

# PROGRESS 2: PERANCANGAN BASIS DATA
## ERD
<img width="921" height="1071" alt="ERD_SBD_REVISI drawio" src="https://github.com/user-attachments/assets/26c77a59-8c57-446e-b308-a938661b45d4" />

## Penjelasan Entitas dan Relasi
1. Entitas Sistem
* **User (Aktor Utama):** Terbagi menjadi Mahasiswa, Staf TU, dan Dosen (di mana akun Pimpinan seperti Dekan/Kaprodi menggunakan basis data aktor Dosen/User dengan hak akses khusus).
* **Dokumen / Surat (Objek Data):** Berkas digital yang mengalami perubahan status secara berkala di dalam sistem pengarsipan.

2. Hubungan Relasi Berdasarkan Alur Aktivitas Flowchart
Hubungan keterkaitan data antar-aktor dimodelkan melalui urutan aktivitas berikut:

##### A. Fase Pengajuan (Mahasiswa)
* **Mahasiswa → Dokumen:** Mahasiswa melakukan otentikasi login untuk mengakses sistem. Mahasiswa memiliki dua opsi relasi terhadap dokumen:
    * Mengunduh dokumen yang telah tersedia hingga selesai.
    * Mengunggah berkas pengajuan baru ke database yang otomatis memicu relasi data berupa **Notifikasi Pengajuan Dokumen** ke pihak Staf TU.

#### B. Fase Validasi & Registrasi (Staf TU)
* **Staf TU → Dokumen:** Staf TU menerima notifikasi berkas masuk lalu melakukan tindakan **Verifikasi Dokumen**.
    * *Jika Valid (Ya):* Staf TU melakukan registrasi dengan **Memberikan Nomor Pada Dokumen**, sehingga status objek data berubah menjadi **Dokumen Diterima**.
    * *Jika Tidak Valid:* Sistem menolak dokumen dan mengembalikan alur data ke Mahasiswa untuk direvisi.

#### C. Fase Distribusi, Pemeriksaan & Disposisi
Setelah status berubah menjadi "Dokumen Diterima", basis data membagi relasi menjadi dua alur pemrosesan:
1.  **Sistem → Dosen:** Menghasilkan **Notifikasi Pada Dosen** untuk melakukan tindakan **Periksa Dokumen**.
2.  **Sistem → Filter Evaluasi:** Dokumen masuk ke menu keputusan untuk menentukan metode penyelesaian berkas:
    * *Jalur Pemeriksaan Dokumen Oleh Dosen:* Berkas dialihkan ke status **Dokumen Diperiksa** setelah dosen menginput catatan evaluasi.
    * *Jalur Disposisi Oleh Dekan/Kaprodi:* Berkas dialihkan ke pimpinan untuk dilakukan **Review Surat Masuk**, kemudian pimpinan menginput data **Memberikan Disposisi pada Dokumen**.

#### D. Fase Finalisasi Status
* **Sistem → Dokumen Final:** Kedua jalur di atas (Pemeriksaan biasa maupun Disposisi) akan bertemu kembali di satu titik akhir yang sama, yaitu mengubah status data menjadi **Dokumen Disetujui**.
* **Perubahan Akhir:** Sistem melakukan eksekusi perintah terakhir berupa **Ubah Status Selesai / Pending** untuk memperbarui rekam jejak arsip digital sebelum alur proses resmi dinyatakan berakhir (Selesai).

## Kamus Data (Data Dictionary)
Kamus data ini menjelaskan secara detail mengenai tipe data, panjang karakter, serta fungsi dari setiap kolom yang digunakan pada rancangan basis data:

### 1. Tabel User (Pengguna)
* `id_user` (INT): Kunci utama (Primary Key) untuk mengidentifikasi setiap akun pengguna secara unik.
* `nama` (VARCHAR, 50): Menyimpan nama lengkap pengguna saat mendaftarkan akun (maksimal 50 karakter).
* `email` (VARCHAR, 50): Menyimpan alamat email pengguna sebagai identitas unik untuk login.
* `password` (VARCHAR, 50): Menyimpan kata sandi akun pengguna untuk keamanan login.
* `role` (VARCHAR, 20): Menentukan peran atau hak akses pengguna di dalam sistem (Mahasiswa / Staf TU / Dosen / Dekan atau Kaprodi).

### 2. Tabel Mahasiswa
* `nim` (VARCHAR, 15): Kunci utama (Primary Key) berupa Nomor Induk Mahasiswa.
* `nama_mahasiswa` (VARCHAR, 50): Menyimpan nama lengkap mahasiswa (maksimal 50 karakter).
* `program_studi` (VARCHAR, 30): Menyimpan nama program studi atau jurusan mahasiswa.
* `id_user` (INT): Kunci tamu (Foreign Key) yang menghubungkan profil mahasiswa ke akun loginnya di tabel User.

### 3. Tabel Dosen
* `nidn` (VARCHAR, 15): Kunci utama (Primary Key) berupa Nomor Induk Dosen Nasional atau kode pengenal dosen.
* `nama_dosen` (VARCHAR, 50): Menyimpan nama lengkap dosen beserta gelar (maksimal 50 karakter).
* `jabatan` (VARCHAR, 40): Menyimpan jabatan struktural atau fungsional dosen (misal: Dosen Pembimbing, Kaprodi, Dekan).
* `id_user` (INT): Kunci tamu (Foreign Key) yang menghubungkan profil dosen ke akun loginnya di tabel User.

### 4. Tabel Staf TU
* `id_pegawai` (VARCHAR, 15): Kunci utama (Primary Key) berupa nomor induk atau kode pegawai staf TU.
* `nama_pegawai` (VARCHAR, 50): Menyimpan nama lengkap staf TU (maksimal 50 karakter).
* `id_user` (INT): Kunci tamu (Foreign Key) yang menghubungkan profil staf ke akun loginnya di tabel User.

### 5. Tabel Dokumen
* `id_dokumen` (INT): Kunci utama (Primary Key) untuk mengidentifikasi setiap berkas dokumen secara unik.
* `nama_berkas` (VARCHAR, 100): Menyimpan nama atau judul berkas digital yang diunggah ke dalam sistem.
* `nomor_dokumen` (VARCHAR, 40): Menyimpan nomor surat resmi yang diberikan oleh staf TU setelah berkas valid.
* `tanggal_unggah` (DATETIME): Mencatat waktu berupa tanggal dan jam ketika berkas pertama kali diunggah mahasiswa.
* `status_dokumen` (VARCHAR, 20): Menyimpan status proses terkini dari berkas (Pending / Diterima / Ditolak / Selesai).
* `catatan_penolakan` (VARCHAR, 200): Menyimpan alasan atau catatan dari staf TU jika dokumen ditolak.
* `file_path` (VARCHAR, 200): Menyimpan jalur direktori atau lokasi penyimpanan file fisik dokumen di server.
* `nim` (VARCHAR, 15): Kunci tamu (Foreign Key) yang menghubungkan dokumen dengan mahasiswa pengunggahnya.
* `id_pegawai` (VARCHAR, 15): Kunci tamu (Foreign Key) yang menghubungkan dokumen dengan staf TU yang memprosesnya.

### 6. Tabel Pemeriksaan
* `id_periksa` (INT): Kunci utama (Primary Key) untuk mengidentifikasi setiap log riwayat pemeriksaan berkas secara unik.
* `id_dokumen` (INT): Kunci tamu (Foreign Key) yang merujuk pada berkas dokumen yang sedang diperiksa.
* `nidn` (VARCHAR, 15): Kunci tamu (Foreign Key) yang merujuk pada dosen yang melakukan pemeriksaan.
* `tanggal_periksa` (DATETIME): Mencatat waktu berupa tanggal dan jam pelaksanaan pemeriksaan berkas oleh dosen.
* `catatan_hasil_pemeriksaan` (VARCHAR, 200): Menyimpan komentar, hasil penilaian, atau catatan evaluasi dari dosen.

### 7. Tabel Disposisi
* `id_disposisi` (INT): Kunci utama (Primary Key) untuk mengidentifikasi setiap lembar instruksi disposisi secara unik.
* `id_dokumen` (INT): Kunci tamu (Foreign Key) yang merujuk pada dokumen surat masuk yang membutuhkan disposisi.
* `id_user` (INT): Kunci tamu (Foreign Key) yang merujuk pada pimpinan (Kaprodi/Dekan) yang memberikan instruksi.
* `tanggal_disposisi` (DATETIME): Mencatat waktu berupa tanggal dan jam pemberian instruksi disposisi oleh pimpinan.
* `isi_instruksi_disposisi` (VARCHAR, 200): Menyimpan pesan perintah atau teks instruksi lanjutan terkait penanganan berkas.

## Normalisasi UNF → 1NF → 2NF → 3NF
Normalisasi adalah teknik perancangan basis data yang digunakan untuk menyusun tabel-tabel secara logis guna mengurangi **redudansi** (pengulangan data) dan mencegah **anomali** (kesalahan saat menambah, mengubah, atau menghapus data). Proses ini diibaratkan seperti merapikan lemari pakaian; kita memisahkan kemeja, celana, dan jaket ke dalam laci yang berbeda agar lebih mudah dicari dan tidak memakan tempat secara percuma.

### 1. UNF (Unnormalized Form / Bentuk Tidak Normal)
Pada tahap UNF, data dikumpulkan apa adanya dari catatan/rekap manual. Data masih memiliki *repeating group* (satu sel berisi banyak nilai), sel yang digabung (merging), dan format pencatatan yang bertumpuk antara data mahasiswa, dokumen, staf TU yang melayani, hingga dosen pemeriksa.

#### Tabel Rekap Pengajuan Dokumen (Raw Data)
| NIM | Info Mahasiswa | Info Dokumen (Berkas, No, Tgl, Path) | Status & Catatan Penolakan | Staf TU (ID - Nama) | Dosen Pemeriksa | Catatan Periksa | Disposisi Pimpinan |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 12345 | Budi (Informatika) | Surat Magang.pdf, SM-001, 2026-06-20 10:00, /docs/magang.pdf | Pending (-) | P01 - Mbak Rini | 111-Pak Andi, 222-Bu Sari | Tolong revisi ttd, Format oke | 333-Pak Dekan (Setujui) |
| 67890 | Siti (Sistem Informasi) | Cuti Kuliah.pdf, -, 2026-06-21 08:30, /docs/cuti.pdf | Ditolak (Berkas tidak lengkap) | P02 - Mas Joko | - | - | - |

---
