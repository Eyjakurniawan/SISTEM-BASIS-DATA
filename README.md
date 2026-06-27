# Sistem Manajemen Arsip Surat dan Dokumen Digital
### Proyek implementasi basis data relasional untuk Sistem Manajemen Arsip Surat dan Dokumen Digital guna mengotomatisasi pencatatan surat, digitalisasi berkas akademik, serta pelacakan verifikasi dan disposisi.

# NAMA ANGGOTA KELOMPOK 7
## Eyja Kurniawan (2501020094)
## Yazira Sartika (2501020103)
## Raihan Parsa Ahza Hamizan (2501020104)
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
5. Sistem harus dapat memperbarui status dokumen secara dinamis (Pending, Diterima, Ditolak, Diperiksa, Disetujui, Selesai) di dalam tabel terkait.
6. Sistem harus dapat mencatat pengiriman notifikasi berkas masuk secara otomatis dari Staf TU ke Dosen Pemeriksa.
7. Sistem harus dapat menyimpan data hasil penilaian, komentar, atau catatan pemeriksaan dokumen yang dilakukan oleh Dosen.
8. Sistem harus dapat mencatat lembar disposisi dari Dekan/Kaprodi yang berisi instruksi kelanjutan berkas.
9. Sistem harus dapat menampilkan laporan operasional berupa jumlah berkas selesai dan berkas tertunda berdasarkan filter rentang tanggal tertentu melalui query SQL.
10. Sistem harus dapat membatasi hak akses unduh berkas agar dokumen internal prodi hanya bisa diakses oleh aktor yang berwenang.

# KEBUTUHAN DATA
### Tabel USER
* `id_user` INT
* `nama` VARCHAR (100)
* `email` VARCHAR (100)
* `password` VARCHAR (255)
* `role` VARCHAR (20)

### Tabel MAHASISWA
* `nim` VARCHAR (15)
* `nama_mahasiswa` VARCHAR (100)
* `prodi` VARCHAR (50)
* `id_user` INT

### Tabel DOSEN
* `nidn` VARCHAR (20)
* `nama_dosen` VARCHAR (100)
* `jabatan` VARCHAR (50)
* `id_user` INT

### Tabel STAF_TU
* `id_pegawai` VARCHAR (15)
* `nama_pegawai` VARCHAR (100)
* `id_user` INT

### Tabel DOKUMEN
* `id_dokumen` INT
* `nama_berkas` VARCHAR (255)
* `no_dokumen` VARCHAR (50)
* `tgl_unggah` DATETIME
* `status_dokumen` VARCHAR (20)
* `catatan_penolakan` VARCHAR (200)
* `file_path` VARCHAR (255)
* `id_pegawai` VARCHAR (15)
* `nim` VARCHAR (15)

### Tabel PEMERIKSAAN
* `id_periksa` INT
* `id_dokumen` INT
* `nidn` VARCHAR (20)
* `tgl_periksa` DATETIME
* `catatan_pemeriksaan` VARCHAR (200)

### Tabel DISPOSISI
* `id_disposisi` INT
* `id_dokumen` INT
* `id_user` INT
* `tgl_disposisi` DATETIME
* `instruksi` VARCHAR (200)

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
* **User (Aktor Utama)** Menyimpan data akun autentikasi yang terbagi menjadi tiga peran (role), yaitu Mahasiswa, Staf TU, dan Dosen. Untuk pimpinan seperti Dekan atau Kaprodi, data menggunakan basis entitas Dosen dengan hak akses khusus.
* **Dokumen / Surat (Objek Data):** Berkas digital yang diunggah oleh mahasiswa dan mengalami perubahan status secara berkala selama proses validasi, pemeriksaan, hingga disposisi.
* **Pemeriksaan:** Entitas transaksional untuk mencatat hasil evaluasi dan rekam jejak pemeriksaan berkas oleh Dosen
* **Disposisi:** Entitas transaksional untuk mencatat instruksi dan lembar perintah lanjutan dari Dekan/Kaprodi terhadap dokumen surat masuk.

2. Hubungan Relasi Berdasarkan Alur Aktivitas Flowchart
Hubungan keterkaitan data antar-aktor dimodelkan melalui urutan aktivitas berikut:

##### A. Fase Pengajuan (Mahasiswa)
* **User dengan Mahasiswa (Relasi 1:1):** Satu akun user hanya memiliki satu data profil mahasiswa yang sah.
* **Mahasiswa dengan Dokumen (Relasi 1:N):** Seorang mahasiswa dapat mengunggah banyak dokumen pengajuan berkas ke dalam database. Proses unggah ini otomatis memicu status awal menjadi 'Pending'.

#### B. Fase Validasi & Registrasi (Staf TU)
* **User dengan Staf TU (Relasi 1:1):** Satu akun user hanya terikat pada satu profil pegawai tata usaha.
* **Staf TU dengan Dokumen (Relasi 1:N):** Seorang staf TU dapat memverifikasi banyak dokumen masuk.
    * *Jika Tidak Valid:* Staf TU mengubah status dokumen menjadi 'Ditolak' dan wajib menginput alasan pada kolom catatan penolakan.
    * Jika Valid:* Staf TU mengubah status menjadi 'Diterima' dan melakukan registrasi penomoran resmi pada kolom nomor dokumen.

#### C. Fase Distribusi, Pemeriksaan & Disposisi
* **User dengan Dosen (Relasi 1:1):** Satu akun user hanya terikat pada satu profil dosen.
* **Dokumen dengan Pemeriksaan (Relasi 1:N) & Dosen dengan Pemeriksaan (Relasi 1:N):** Setelah berstatus 'Diterima', berkas didistribusikan ke Dosen terkait. Dosen dapat memeriksa banyak dokumen dan mencatat evaluasinya di tabel Pemeriksaan, yang mengubah status berkas menjadi 'Diperiksa'.
* **Dokumen dengan Disposisi (Relasi 1:N) & User dengan Disposisi (Relasi 1:N):** Khusus berkas surat masuk pimpinan, Dekan/Kaprodi (menggunakan akun User pimpinan) memberikan lembar instruksi resmi yang datanya disimpan di dalam tabel Disposisi.

#### D. Fase Finalisasi Status
Setelah melalui jalur Pemeriksaan Dosen atau Disposisi Pimpinan, status akhir objek data pada tabel dokumen akan diperbarui secara dinamis menjadi 'Disetujui' atau 'Selesai', menandakan seluruh rangkaian proses bisnis pengarsipan telah berakhir.

## Kamus Data (Data Dictionary)
Kamus data ini menjelaskan secara detail mengenai tipe data, panjang karakter, serta fungsi dari setiap kolom yang digunakan pada rancangan basis data:

### 1. Tabel USER (Pengguna)
* `id_user` (INT): Kunci utama (Primary Key) untuk mengidentifikasi setiap akun pengguna secara unik.
* `nama` (VARCHAR, 100): Menyimpan nama lengkap pengguna saat mendaftarkan akun (maksimal 100 karakter).
* `email` (VARCHAR, 100): Menyimpan alamat email pengguna sebagai identitas unik untuk login.
* `password` (VARCHAR, 255): Menyimpan kata sandi akun pengguna untuk keamanan login.
* `role` (VARCHAR, 20): Menentukan peran atau hak akses pengguna di dalam sistem (Mahasiswa / Staf TU / Dosen / Dekan).

### 2. Tabel MAHASISWA
* `nim` (VARCHAR, 15): Kunci utama (Primary Key) berupa Nomor Induk Mahasiswa.
* `nama_mahasiswa` (VARCHAR, 100): Menyimpan nama lengkap mahasiswa (maksimal 100 karakter).
* `prodi` (VARCHAR, 50): Menyimpan nama program studi mahasiswa.
* `id_user` (INT): Kunci tamu (Foreign Key) yang menghubungkan profil mahasiswa ke akun loginnya di tabel USER.

### 3. Tabel DOSEN
* `nidn` (VARCHAR, 20): Kunci utama (Primary Key) berupa Nomor Induk Dosen Nasional atau kode pengenal dosen.
* `nama_dosen` (VARCHAR, 100): Menyimpan nama lengkap dosen beserta gelar (maksimal 100 karakter).
* `jabatan` (VARCHAR, 50): Menyimpan jabatan struktural atau fungsional dosen (misal: Dosen, Kaprodi, Dekan).
* `id_user` (INT): Kunci tamu (Foreign Key) yang menghubungkan profil dosen ke akun loginnya di tabel USER.

### 4. Tabel STAF_TU
* `id_pegawai` (VARCHAR, 15): Kunci utama (Primary Key) berupa nomor induk atau kode pegawai staf TU.
* `nama_pegawai` (VARCHAR, 100): Menyimpan nama lengkap staf TU (maksimal 100 karakter).
* `id_user` (INT): Kunci tamu (Foreign Key) yang menghubungkan profil staf ke akun loginnya di tabel USER.

### 5. Tabel DOKUMEN
* `id_dokumen` (INT): Kunci utama (Primary Key) untuk mengidentifikasi setiap berkas dokumen secara unik.
* `nama_berkas` (VARCHAR, 255): Menyimpan nama atau judul berkas digital yang diunggah ke dalam sistem.
* `no_dokumen` (VARCHAR, 50): Menyimpan nomor surat resmi yang diberikan oleh staf TU setelah berkas valid.
* `tgl_unggah` (DATETIME): Mencatat waktu berupa tanggal dan jam ketika berkas pertama kali diunggah mahasiswa.
* `status_dokumen` (VARCHAR, 20): Menyimpan status proses terkini dari berkas (Pending / Diterima / Ditolak / Selesai / Diperiksa / Disetujui).
* `catatan_penolakan` (VARCHAR, 200): Menyimpan alasan atau catatan dari staf TU jika dokumen ditolak.
* `file_path` (VARCHAR, 255): Menyimpan jalur direktori atau lokasi penyimpanan file fisik dokumen di server.
* `id_pegawai` (VARCHAR, 15): Kunci tamu (Foreign Key) yang menghubungkan dokumen dengan staf TU yang memproses atau memverifikasinya.
* `nim` (VARCHAR, 15): Kunci tamu (Foreign Key) yang menghubungkan dokumen dengan mahasiswa pengunggahnya.

### 6. Tabel PEMERIKSAAN
* `id_periksa` (INT): Kunci utama (Primary Key) untuk mengidentifikasi setiap log riwayat pemeriksaan berkas secara unik.
* `id_dokumen` (INT): Kunci tamu (Foreign Key) yang merujuk pada berkas dokumen yang sedang diperiksa.
* `nidn` (VARCHAR, 20): Kunci tamu (Foreign Key) yang merujuk pada dosen yang melakukan pemeriksaan.
* `tgl_periksa` (DATETIME): Mencatat waktu berupa tanggal dan jam pelaksanaan pemeriksaan berkas oleh dosen.
* `catatan_pemeriksaan` (VARCHAR, 200): Menyimpan ulasan, komentar, hasil penilaian, atau catatan evaluasi dari dosen.

### 7. Tabel DISPOSISI
* `id_disposisi` (INT): Kunci utama (Primary Key) untuk mengidentifikasi setiap lembar instruksi disposisi secara unik.
* `id_dokumen` (INT): Kunci tamu (Foreign Key) yang merujuk pada dokumen berkas surat masuk yang membutuhkan disposisi.
* `id_user` (INT): Kunci tamu (Foreign Key) yang merujuk pada pimpinan (Kaprodi/Dekan) yang memberikan instruksi disposisi melalui tabel USER.
* `tgl_disposisi` (DATETIME): Mencatat waktu berupa tanggal dan jam pemberian instruksi disposisi oleh pimpinan.
* `instruksi` (VARCHAR, 200): Menyimpan pesan perintah atau teks instruksi lanjutan terkait penanganan berkas oleh pimpinan.

## Normalisasi UNF → 1NF → 2NF → 3NF
Normalisasi adalah teknik perancangan basis data yang digunakan untuk menyusun tabel-tabel secara logis guna mengurangi **redudansi** (pengulangan data) dan mencegah **anomali** (kesalahan saat menambah, mengubah, atau menghapus data). Proses ini diibaratkan seperti merapikan lemari pakaian; kita memisahkan kemeja, celana, dan jaket ke dalam laci yang berbeda agar lebih mudah dicari dan tidak memakan tempat secara percuma.

### 1. UNF (Unnormalized Form / Bentuk Tidak Normal)
Pada tahap UNF, data dikumpulkan apa adanya dari catatan/rekap manual. Data masih memiliki *repeating group* (satu sel berisi banyak nilai), sel yang digabung (merging), dan format pencatatan yang bertumpuk antara data mahasiswa, dokumen, staf TU yang melayani, hingga dosen pemeriksa.

#### Tabel Rekap Pengajuan Dokumen (Raw Data)
| nim | Info Mahasiswa | Info Dokumen (Berkas, No, Tgl, Path) | Status & Catatan Penolakan | Staf TU (ID - Nama) | Dosen Pemeriksa | Catatan Pemeriksaan | Disposisi Pimpinan |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2501020103 | Yazira Sartika (Teknik Informatika) | Surat_Izin_Observasi.pdf, SIO-001, 2026-06-18 09:00, /docs/sio1.pdf | Pending (-) | P01 - Mbak Rini | 0022028903-Ferdi Chahyadi, 9990631627-Nolan Efranda | Tambahkan tujuan, Format sudah oke | 9-Martaleli Bettiza (Setujui segera) |
| 2501020094 | Eyja Kurniawan (Teknik Informatika) | Proposal_Badminton.pdf, -, 2026-06-19 14:30, /docs/prop2.pdf | Ditolak (Revisi RAB) | P02 - Mas Joko | - | - | - |
| 2501020104 | Raihan Parsa (Teknik Informatika) | Surat_Permohonan_Cuti.pdf, SC-045, 2026-06-20 10:15, /docs/cuti3.pdf | Selesai (-) | P01 - Mbak Rini | 0117099601-Feri Irawan | Sesuai aturan | 9-Martaleli Bettiza (Disetujui) |
| 2501020108 | Naufal Putra (Teknik Informatika) | Keringanan_UKT.pdf, UKT-012, 2026-06-21 08:00, /docs/ukt4.pdf | Diperiksa (-) | P02 - Mas Joko | 7141775676130173-Rifaldi Herikson | Sedang diverifikasi | - |

---

### 2. 1NF (First Normal Form / Bentuk Normal Kesatu)
Syarat 1NF adalah setiap atribut harus bernilai **atomik** (tidak ada multi-value atau grup berulang dalam satu sel) dan tidak ada baris yang duplikat. Data pada baris pertama (dokumen observasi Yazira Sartika) yang diperiksa oleh lebih dari satu dosen, dipecah menjadi baris terpisah.

#### Tabel Dokumen 1NF
| nim | nama_mahasiswa | prodi | nama_berkas | no_dokumen | tgl_unggah | file_path | status_dokumen | catatan_penolakan | id_pegawai | nama_pegawai | nidn | nama_dosen | catatan_pemeriksaan | id_user | instruksi |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2501020103 | Yazira Sartika | Teknik Informatika | Surat_Izin_Observasi.pdf | SIO-001 | 2026-06-18 09:00 | /docs/sio1.pdf | Pending | - | P01 | Mbak Rini | 0022028903 | Ferdi Chahyadi | Tambahkan tujuan | 9 | Setujui segera |
| 2501020103 | Yazira Sartika | Teknik Informatika | Surat_Izin_Observasi.pdf | SIO-001 | 2026-06-18 09:00 | /docs/sio1.pdf | Pending | - | P01 | Mbak Rini | 9990631627 | Nolan Efranda | Format sudah oke | 9 | Setujui segera |
| 2501020094 | Eyja Kurniawan | Teknik Informatika | Proposal_Badminton.pdf | NULL | 2026-06-19 14:30 | /docs/prop2.pdf | Ditolak | Revisi RAB | P02 | Mas Joko | NULL | NULL | NULL | NULL | NULL |
| 2501020104 | Raihan Parsa | Teknik Informatika | Surat_Permohonan_Cuti.pdf | SC-045 | 2026-06-20 10:15 | /docs/cuti3.pdf | Selesai | - | P01 | Mbak Rini | 0117099601 | Feri Irawan | Sesuai aturan | 9 | Disetujui |
| 2501020108 | Naufal Putra | Teknik Informatika | Keringanan_UKT.pdf | UKT-012 | 2026-06-21 08:00 | /docs/ukt4.pdf | Diperiksa | - | P02 | Mas Joko | 7141775676130173 | Rifaldi Herikson | Sedang diverifikasi | NULL | NULL |

---

### 3. 2NF (Second Normal Form / Bentuk Normal Kedua)
Syarat 2NF adalah data memenuhi 1NF dan menghilangkan **Partial Dependency** (ketergantungan parsial). Tabel raksasa di 1NF dipisahkan menjadi tabel struktur entitas (Master) dan tabel kegiatan (Transaksi). Atribut login (`email`, `password`) masih melekat sementara pada tabel profil masing-masing sebelum dibersihkan di tahap berikutnya.

#### A. Tabel Mahasiswa (Struktur 2NF)
| nim (PK) | nama_mahasiswa | prodi | email | password |
| :--- | :--- | :--- | :--- | :--- |
| 2501020103 | Yazira Sartika | Teknik Informatika | yazira@mhs.com | pass123 |
| 2501020094 | Eyja Kurniawan | Teknik Informatika | eyja@mhs.com | pass456 |
| 2501020104 | Raihan Parsa | Teknik Informatika | raihan@mhs.com | pass789 |
| 2501020108 | Naufal Putra | Teknik Informatika | naufal@mhs.com | pass000 |

#### B. Tabel Staf TU (Struktur 2NF)
| id_pegawai (PK) | nama_pegawai | email | password |
| :--- | :--- | :--- | :--- |
| P01 | Mbak Rini | rini@tu.com | tu123 |
| P02 | Mas Joko | joko@tu.com | tu456 |

#### C. Tabel Dosen (Struktur 2NF)
| nidn (PK) | nama_dosen | jabatan | email | password |
| :--- | :--- | :--- | :--- | :--- |
| 0022028903 | Ferdi Chahyadi | Dosen | ferdi@dsn.com | dsn002 |
| 9990631627 | Nolan Efranda | Dosen | nolan@dsn.com | dsn999 |
| 7141775676130173 | Rifaldi Herikson | Dosen | rifaldi@dsn.com | dsn714 |
| 0117099601 | Feri Irawan | Dosen | feri@dsn.com | dsn011 |
| 1028087501 | Martaleli Bettiza | Dekan | martaleli@dsn.com | dsn102 |

#### D. Tabel DOKUMEN
| id_dokumen (PK) | nama_berkas | no_dokumen | tgl_unggah | status_dokumen | catatan_penolakan | file_path | id_pegawai (FK) | nim (FK) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Surat_Izin_Observasi.pdf | SIO-001 | 2026-06-18 09:00 | Pending | - | /docs/sio1.pdf | P01 | 2501020103 |
| 2 | Proposal_Badminton.pdf | NULL | 2026-06-19 14:30 | Ditolak | Revisi RAB | /docs/prop2.pdf | P02 | 2501020094 |
| 3 | Surat_Permohonan_Cuti.pdf | SC-045 | 2026-06-20 10:15 | Selesai | - | /docs/cuti3.pdf | P01 | 2501020104 |
| 4 | Keringanan_UKT.pdf | UKT-012 | 2026-06-21 08:00 | Diperiksa | - | /docs/ukt4.pdf | P02 | 2501020108 |

#### E. Tabel Transaksi Gabungan Pemeriksaan & Disposisi
| id_trans (PK) | id_dokumen (FK) | nidn (FK) | catatan_pemeriksaan | id_user (FK) | instruksi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TRX-1 | 1 | 0022028903 | Tambahkan tujuan | 9 | Setujui segera |
| TRX-2 | 1 | 9990631627 | Format sudah oke | 9 | Setujui segera |
| TRX-3 | 3 | 0117099601 | Sesuai aturan | 9 | Disetujui |
| TRX-4 | 4 | 7141775676130173 | Sedang diverifikasi | NULL | NULL |

---

### 4. 3NF (Third Normal Form / Bentuk Normal Ketiga)
Syarat 3NF adalah memenuhi 2NF dan menghilangkan **Transitive Dependency** (ketergantungan transitif). Informasi kredensial login ditarik keluar menjadi satu **Tabel USER** terpusat. Alur proses setelah dokumen diterima dipisah secara tegas menjadi **Tabel PEMERIKSAAN** dan **Tabel DISPOSISI** sesuai rancangan ERD final kelompok.

#### 1. Tabel USER (Sentralisasi Autentikasi)
| id_user (PK) | nama | email | password | role |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Yazira Sartika | yazira@mhs.com | pass123 | Mahasiswa |
| 2 | Eyja Kurniawan | eyja@mhs.com | pass456 | Mahasiswa |
| 3 | Raihan Parsa | raihan@mhs.com | pass789 | Mahasiswa |
| 4 | Naufal Putra | naufal@mhs.com | pass000 | Mahasiswa |
| 5 | Mbak Rini | rini@tu.com | tu123 | Staf TU |
| 6 | Mas Joko | joko@tu.com | tu456 | Staf TU |
| 7 | Ferdi Chahyadi | ferdi@dsn.com | dsn002 | Dosen |
| 8 | Nolan Efranda | nolan@dsn.com | dsn999 | Dosen |
| 9 | Martaleli Bettiza | martaleli@dsn.com | dsn102 | Dekan |
| 10 | Feri Irawan | feri@dsn.com | dsn011 | Dosen |
| 11 | Rifaldi Herikson | rifaldi@dsn.com | dsn714 | Dosen |

#### 2. Tabel MAHASISWA
| nim (PK) | nama_mahasiswa | prodi | id_user (FK) |
| :--- | :--- | :--- | :--- |
| 2501020103 | Yazira Sartika | Teknik Informatika | 1 |
| 2501020094 | Eyja Kurniawan | Teknik Informatika | 2 |
| 2501020104 | Raihan Parsa | Teknik Informatika | 3 |
| 2501020108 | Naufal Putra | Teknik Informatika | 4 |

#### 3. Tabel STAF_TU
| id_pegawai (PK) | nama_pegawai | id_user (FK) |
| :--- | :--- | :--- |
| P01 | Mbak Rini | 5 |
| P02 | Mas Joko | 6 |

#### 4. Tabel DOSEN
| nidn (PK) | nama_dosen | jabatan | id_user (FK) |
| :--- | :--- | :--- | :--- |
| 0022028903 | Ferdi Chahyadi | Dosen | 7 |
| 9990631627 | Nolan Efranda | Dosen | 8 |
| 1028087501 | Martaleli Bettiza | Dekan | 9 |
| 0117099601 | Feri Irawan | Dosen | 10 |
| 7141775676130173 | Rifaldi Herikson | Dosen | 11 |

#### 5. Tabel DOKUMEN (Tabel Utama Objek Berkas)
| id_dokumen (PK) | nama_berkas | no_dokumen | tgl_unggah | status_dokumen | catatan_penolakan | file_path | id_pegawai (FK) | nim (FK) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Surat_Izin_Observasi.pdf | SIO-001 | 2026-06-18 09:00 | Pending | - | /docs/sio1.pdf | P01 | 2501020103 |
| 2 | Proposal_Badminton.pdf | NULL | 2026-06-19 14:30 | Ditolak | Revisi RAB | /docs/prop2.pdf | P02 | 2501020094 |
| 3 | Surat_Permohonan_Cuti.pdf | SC-045 | 2026-06-20 10:15 | Selesai | - | /docs/cuti3.pdf | P01 | 2501020104 |
| 4 | Keringanan_UKT.pdf | UKT-012 | 2026-06-21 08:00 | Diperiksa | - | /docs/ukt4.pdf | P02 | 2501020108 |

#### 6. Tabel PEMERIKSAAN
| id_periksa (PK) | id_dokumen (FK) | nidn (FK) | tgl_periksa | catatan_pemeriksaan |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 0022028903 | 2026-06-18 10:00 | Tambahkan tujuan |
| 2 | 1 | 9990631627 | 2026-06-18 11:30 | Format sudah oke |
| 3 | 3 | 0117099601 | 2026-06-20 13:00 | Sesuai aturan |
| 4 | 4 | 7141775676130173 | 2026-06-21 10:30 | Sedang diverifikasi |

#### 7. Tabel DISPOSISI
| id_disposisi (PK) | id_dokumen (FK) | id_user (FK) | tgl_disposisi | instruksi |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 9 | 2026-06-19 14:30 | Setujui segera |
| 2 | 3 | 9 | 2026-06-21 14:00 | Disetujui |

**Catatan Penting Perubahan Relasi Pimpinan (2NF ke 3NF):**
Jika diperhatikan, sejak pemisahan tabel transaksi, relasi penstrukturan pimpinan pada Disposisi diarahkan langsung menuju id_user dan bukan NIDN fisik dosen.

**Alasan Perubahan Struktur:**
1. **Penerapan Aturan Ketat 3NF:** Untuk menghilangkan *Transitive Dependency*, seluruh data kredensial login (`email`, `password`, `role`) mahasiswa, staf TU, maupun dosen ditarik keluar dari tabel profil masing-masing dan disatukan secara terpusat ke dalam **Tabel User**.
2. **Otorisasi Aksi pada Aplikasi:** Tindakan *"Memberikan Disposisi"* di dalam sistem digital merupakan sebuah aksi otorisasi yang melekat pada **Akun Login (User)** yang sedang aktif di aplikasi (siapa yang menekan tombol setuju), bukan melekat pada identitas fisik akademik dosen (`NIDN`). Oleh karena itu, Tabel Disposisi dihubungkan langsung ke `id_user` pada Tabel User untuk memastikan bahwa aktor yang mengeksekusi perintah tersebut memiliki hak akses (*role*) yang sah sebagai Dekan/Pimpinan.
---

# PROGRESS 3: IMPLEMENTASI DATABASE DAN PENGUJIAN
## Ketentuan 1 dan 2: Script SQL DDL & Constraint
<img width="527" height="88" alt="1" src="https://github.com/user-attachments/assets/55f678e5-e8da-4708-a518-9c42dde9d8c0" />
<img width="492" height="148" alt="2" src="https://github.com/user-attachments/assets/42e5a147-fa96-4a7d-add9-3a31c5c9b4af" />
<img width="838" height="149" alt="3" src="https://github.com/user-attachments/assets/274ddeb0-9a1b-4c5c-84a2-b4779d1cfdf6" />
<img width="821" height="136" alt="4" src="https://github.com/user-attachments/assets/4405812e-192d-4a24-8be2-a8c1e1d61de1" />
<img width="805" height="156" alt="5" src="https://github.com/user-attachments/assets/ca4f78d7-1fb2-4ff9-a78d-3dc6825b8a3f" />
<img width="856" height="229" alt="6" src="https://github.com/user-attachments/assets/82729f06-3c77-4a5e-8553-22bd1b620762" />
<img width="946" height="162" alt="7" src="https://github.com/user-attachments/assets/56df88f1-6f98-4bd7-9df4-ad75e96e79e7" />
<img width="943" height="168" alt="8" src="https://github.com/user-attachments/assets/f042d9d1-f864-4580-a8c4-0ffc2a6bdcf0" />

## Ketentuan 3: Data uji
<img width="840" height="230" alt="9" src="https://github.com/user-attachments/assets/98669f81-bd44-4fce-8e2f-2186bdddf11d" />
<img width="869" height="120" alt="10" src="https://github.com/user-attachments/assets/404e5adc-97e4-429b-b350-d9a4afe78da3" />
<img width="840" height="83" alt="11" src="https://github.com/user-attachments/assets/b7f217c7-8923-45fe-8931-fd04b79d21fd" />
<img width="827" height="136" alt="12" src="https://github.com/user-attachments/assets/9fdb3cb0-520e-4c4d-a163-7e02b942e37d" />
<img width="1348" height="136" alt="13" src="https://github.com/user-attachments/assets/91145fc2-cd94-4dae-8a24-1fe5d82d9726" />
<img width="1106" height="120" alt="14" src="https://github.com/user-attachments/assets/0ed1a76f-a6c6-4624-a53f-fe3c26f767fd" />
<img width="1061" height="90" alt="15" src="https://github.com/user-attachments/assets/6d38abc1-b405-43fc-8224-fb97cf5d2e9d" />

## Ketentuan 4: 10 Query SQL
Query 1: Menampilkan Seluruh Dokumen yang Berstatus 'Pending'
Fungsi: Membantu Staf TU memantau antrean berkas mahasiswa baru yang masuk ke sistem untuk segera divalidasi.
<img width="808" height="150" alt="16" src="https://github.com/user-attachments/assets/63cb008c-5119-4a51-93b9-b0f85867a494" />

Query 2: Menampilkan Daftar Pengajuan Dokumen Lengkap dengan Nama Mahasiswa (INNER JOIN)
Fungsi: Menggabungkan tabel dokumen dan mahasiswa agar memunculkan nama terang pemilik dokumen.
<img width="900" height="200" alt="17" src="https://github.com/user-attachments/assets/3e4c9691-db8e-49dc-8701-2029db83dc2d" />

Query 3: Menghitung Jumlah Dokumen Berdasarkan Setiap Status (COUNT & GROUP BY)
Fungsi: Menyajikan ringkasan statistik total berkas selesai, tertunda, atau ditolak sebagai bahan rekapitulasi berkas.
<img width="732" height="199" alt="18" src="https://github.com/user-attachments/assets/d9b8737c-f796-4bea-983d-b6eece295b74" />

Query 4: Menampilkan Dokumen yang Ditolak Beserta Alasan Penolakannya
Fungsi: Memudahkan pengembang sistem memunculkan umpan balik alasan penolakan dokumen di dashboard mahasiswa.
<img width="861" height="153" alt="19" src="https://github.com/user-attachments/assets/ab7c1017-4b96-440b-8d56-06f87bb49392" />

Query 5: Menampilkan Riwayat Catatan Pemeriksaan Dosen terhadap Berkas Tertentu (Multi-join)
Fungsi: Melacak rekam jejak penilaian dosen, berkas apa yang diperiksa, dan siapa nama dosen pemeriksanya.
<img width="1038" height="212" alt="20" src="https://github.com/user-attachments/assets/6e762f6b-1511-4ea5-8003-2e4e57b84732" />

Query 6: Menampilkan Lembar Instruksi Disposisi dari Dekan / Pimpinan
Fungsi: Menampilkan isi pesan arahan atau lembar instruksi resmi yang dikeluarkan oleh pimpinan fakultas.
<img width="1095" height="192" alt="21" src="https://github.com/user-attachments/assets/78fc0db5-a896-4ebc-980e-c6d8b2f1a1df" />

Query 7: Rekap Data Mahasiswa yang Akun Loginnya Memiliki Role 'Mahasiswa'
Fungsi: Memastikan keabsahan hak akses sistem (role autentikasi) terhubung secara akurat dengan data master NIM mahasiswa.
<img width="718" height="199" alt="22" src="https://github.com/user-attachments/assets/122961a0-e04a-4303-90c4-1d569f48e66c" />

Query 8: Filter Dokumen yang Diunggah pada Rentang Tanggal Tertentu (Tracking Periode)
Fungsi: Menghasilkan laporan arsip dokumen masuk berdasarkan filter periode (misal: mingguan atau bulanan).
<img width="679" height="182" alt="23" src="https://github.com/user-attachments/assets/887f2da3-a22a-49e7-aa1a-62e260c6b82d" />

Query 9: Menampilkan Staf TU yang Paling Banyak Memverifikasi Berkas (Kombinasi Aggregate)
Fungsi: Mengukur beban kerja serta produktivitas kinerja dari masing-masing staf TU dalam mengurus berkas digital prodi.
<img width="938" height="183" alt="24" src="https://github.com/user-attachments/assets/8454d684-9866-4487-a085-5582d667cdb1" />

Query 10: Mengupdate Status Dokumen Menjadi 'Selesai' Berdasarkan ID Tertentu
Mensimulasikan pembaruan status data secara riil saat dokumen telah menuntaskan seluruh tahapan disposisi.
<img width="458" height="89" alt="25" src="https://github.com/user-attachments/assets/bc11aa3c-adc3-4ec5-a314-2cfef2ffc487" />

# Ketentuan 5: Skenario pengujian (UAT - User Acceptance Testing)
Skenario pengujian ini dirancang untuk mensimulasikan alur kerja nyata pada sistem dan membuktikan bahwa batasan relasi (*constraint*) serta fungsionalitas basis data berjalan dengan sukses tanpa terjadi eror sintaks.

| ID Uji | Fitur / Skenario Pengujian | Langkah Pengujian (Query SQL Penguji) | Hasil yang Diharapkan | Status |
| :--- | :--- | :--- | :--- | :--- |
| **UAT-01** | **Autentikasi Relasional Akun** | `SELECT m.nim, m.nama_mahasiswa, u.email, u.role FROM MAHASISWA m INNER JOIN USER u ON m.id_user = u.id_user;` | Sistem menyajikan kecocokan relasi kunci asing (`id_user`) antara data profil mahasiswa dan akun login dengan benar. | Sukses |
| **UAT-02** | **Pengunggahan Berkas Baru oleh Mahasiswa** | `INSERT INTO DOKUMEN (nama_berkas, no_dokumen, tgl_unggah, status_dokumen, catatan_penolakan, file_path, id_pegawai, nim) VALUES ('Proposal_Skripsi_Yas.pdf', NULL, NOW(), DEFAULT, '-', '/docs/skripsi_yas.pdf', 'P01', '2501020103');` | Data dokumen baru berhasil masuk ke database dengan status default otomatis **'Pending'** dan nomor surat resmi bernilai **`NULL`**. | Sukses |
| **UAT-03** | **Validasi & Penolakan Berkas oleh Staf TU** | `UPDATE DOKUMEN SET status_dokumen = 'Ditolak', catatan_penolakan = 'Format proposal belum sesuai template prodi' WHERE id_dokumen = 2;` | Status dokumen dengan ID 2 berubah secara dinamis menjadi **'Ditolak'** dan teks alasan penolakan terekam permanen di database. | Sukses |
| **UAT-04** | **Pemeriksaan & Evaluasi Berkas oleh Dosen** | `INSERT INTO PEMERIKSAAN (id_dokumen, nidn, tgl_periksa, catatan_pemeriksaan) VALUES (1, '0022028903', NOW(), 'Bab 1 perlu diperjelas di bagian metode');` | Catatan evaluasi dosen berhasil ditambahkan ke tabel `PEMERIKSAAN` dan terikat kuat ke identitas fisik dosen (`NIDN`). | Sukses |
| **UAT-05** | **Lembar Instruksi Disposisi Pimpinan (Dekan)** | `INSERT INTO DISPOSISI (id_dokumen, id_user, tgl_disposisi, instruksi) VALUES (1, 9, NOW(), 'Teruskan ke prodi untuk dijadwalkan seminar');` | Lembar perintah disposisi dari Dekan (`id_user = 9`) berhasil tercatat secara kronologis dalam sistem untuk kelanjutan berkas terkait. | Sukses |



# PROGRESS 4: LAPORAN AKHIR






