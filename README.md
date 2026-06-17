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
* `id_user` INT

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
<img width="1041" height="2018" alt="Mentahan Flowchart SBD Revisi" src="https://github.com/user-attachments/assets/99dc035f-e762-47a3-a646-67eba210f7bf" />


# PEMBAGIAN TUGAS SETIAP ANGGOTA
1. Naufal (2501020108) = Bertugas dalam membuat studi kasus, latar belakang, serta tujuan sistem.
2. Yazira Sartika (2501020103) = Bertugas dalam membuat identifikasi aktor dan kebutuhan fungsional.
3. Raihan (2501020104) = Bertugas dalam membuat rancangan kebutuhan data.
4. Eyja Kurniawan (2501020094) = Bertugas dalam membuat diagram proses atau flowchart.

# LINK REPOSITORY GITHUB
https://github.com/Eyjakurniawan/SISTEM-BASIS-DATA.git

---

# PROGRESS 2: PERANCANGAN BASIS DATA

## Penjelasan Entitas dan Relasi 

### 1. Entitas (Entities)
Dalam konteks sistem ini, entitas dapat dibagi menjadi Aktor (User) dan Objek (Data/Dokumen):

Mahasiswa: Pengguna sistem yang bertindak sebagai pemohon (yang mengunggah dokumen) atau konsumen (yang mengunduh dokumen).

Staf TU (Tata Usaha): Pengguna sistem yang berfungsi sebagai validator awal, administrator dokumen (registrasi/penomoran), dan pengelola arsip (hapus dokumen).

Dosen (termasuk Dekan/Kaprodi): Pengguna sistem tingkat atas yang bertanggung jawab memeriksa, memberikan disposisi, dan memberikan persetujuan (approval) akhir terhadap dokumen.

Dokumen / Surat: Objek utama yang mengalir di dalam sistem. Dokumen ini memiliki siklus hidup yang berubah statusnya (diunggah, diverifikasi, diberi nomor, diperiksa, didisposisi, disetujui, hingga selesai/pending).

### 2. Relasi dan Alur Proses (Relations & Process Flow)
Relasi di dalam flowchart ini digambarkan melalui garis alur aktivitas yang menghubungkan para aktor dengan dokumen. Berikut adalah rincian relasinya berdasarkan peran:

A. Alur Relasi Mahasiswa
Mahasiswa → Dokumen (Download): Mahasiswa memilih dokumen yang tersedia di sistem untuk diunduh langsung hingga selesai.
Mahasiswa → Dokumen (Upload): Mahasiswa membuat/mengunggah dokumen baru ke dalam sistem, yang kemudian memicu notifikasi ke pihak Staf TU.

B. Alur Relasi Staf TU (Verifikasi & Administrasi)
Staf TU → Dokumen (Pengelolaan): Staf TU dapat melakukan hapus dokumen atau registrasi baru secara mandiri.
Staf TU → Dokumen Mahasiswa: Staf TU menerima notifikasi pengajuan, melakukan Verifikasi Dokumen, dan mengambil keputusan:
Jika TIDAK diterima: Relasi kembali ke Mahasiswa untuk perbaikan.
Jika YA (diterima): Staf TU Memberikan Nomor Pada Dokumen.
Staf TU → Dosen: Setelah dokumen resmi diterima dan diberi nomor, sistem mengirimkan Notifikasi Pada Dosen.

C. Alur Relasi Dosen & Pimpinan (Pemeriksaan & Disposisi)
Setelah Dosen menerima notifikasi dan memeriksa dokumen, alur terbagi menjadi dua jalur evaluasi (Decision):
Jalur Pemeriksaan Biasa (Oleh Dosen): Dokumen diperiksa → Dokumen Disetujui.
Jalur Disposisi (Oleh Dekan/Kaprodi): Pimpinan melakukan Review Surat Masuk → Memberikan Disposisi pada Dokumen → Dokumen Disetujui.

D. Tahap Akhir Dokumen
Dosen/Sistem → Dokumen: Setelah dokumen disetujui (baik lewat jalur pemeriksaan biasa maupun disposisi), sistem akan Mengubah Status dokumen menjadi Selesai atau Pending, lalu proses berakhir (Selesai).

## Kamus Data (Data Dictionary)
Kamus data ini menjelaskan secara detail mengenai tipe data, panjang karakter, serta fungsi dari setiap kolom yang digunakan pada rancangan basis data:

### 1. Tabel User
* `id_user` (INT): Kunci utama (Primary Key) untuk mengidentifikasi setiap akun pengguna secara unik.
* `nama` (VARCHAR, 50): Menyimpan nama lengkap pengguna saat mendaftaran akun (maksimal 50 karakter).
* `email` (VARCHAR, 50): Menyimpan alamat email pengguna sebagai identitas unik untuk login.
* `password` (VARCHAR, 50): Menyimpan kata sandi akun pengguna untuk keamanan login.
* `role` (VARCHAR, 20): Menentukan peran atau hak akses pengguna di dalam sistem (Mahasiswa / Staf TU / Dosen / Dekan atau Kaprodi).

### 2. Tabel Mahasiswa
* `nim` (VARCHAR, 15): Kunci utama (Primary Key) berupa Nomor Induk Mahasiswa.
* `nama_mahasiswa` (VARCHAR, 50): Menyimpan nama lengkap mahasiswa (maksimal 50 karakter).
* `program_studi` (VARCHAR, 30): Menyimpan nama program studi atau jurusan mahasiswa.
* `id_user` (INT): Kunci tamu (Foreign Key) yang menghubungkan profil mahasiswa ke akun loginnya di tabel User.

### 3. Tabel Dosen
* `nidn` (VARCHAR, 15): Kunci utama (Primary Key) berupa Nomor Induk Dosen Nasional.
* `nama_dosen` (VARCHAR, 50): Menyimpan nama lengkap dosen beserta gelar (maksimal 50 karakter).
* `jabatan` (VARCHAR, 40): Menyimpan jabatan struktural atau fungsional dosen (misal: Dosen, Kaprodi, Dekan).
* `id_user` (INT): Kunci tamu (Foreign Key) yang menghubungkan profil dosen ke akun loginnya di tabel User.

### 4. Tabel Staf TU
* `id_pegawai` (VARCHAR, 15): Kunci utama (Primary Key) berupa nomor induk pegawai staf TU.
* `nama_pegawai` (VARCHAR, 50): Menyimpan nama lengkap staf TU (maksimal 50 karakter).
* `id_user` (INT): Kunci tamu (Foreign Key) yang menghubungkan profil staf ke akun loginnya di tabel User.

### 5. Tabel Dokumen
* `id_dokumen` (INT): Kunci utama (Primary Key) untuk mengidentifikasi setiap berkas dokumen secara unik.
* `nama_berkas` (VARCHAR, 100): Menyimpan nama asli file yang diunggah ke dalam sistem. 
* `nomor_dokumen` (VARCHAR, 40): Menyimpan nomor surat resmi yang diterbitkan dan diinput oleh prodi/staf TU.
* `tanggal_unggah` (DATETIME): Mencatat waktu dan tanggal tepat saat dokumen diunggah oleh mahasiswa.
* `status_dokumen` (VARCHAR, 20): Melacak status berkas secara dinamis (Pending / Diterima / Ditolak / Selesai).
* `catatan_penolakan` (VARCHAR, 200): Menyimpan teks alasan penolakan jika berkas tidak lolos verifikasi awal oleh staf TU.
* `file_path` (VARCHAR, 200): Menyimpan teks alamat tautan atau link lokasi folder penyimpanan file digital.
* `id_user` (INT): Kunci tamu (Foreign Key) untuk mencatat akun pengguna mana yang mengunggah dokumen tersebut.

### 6. Tabel Pemeriksaan
* `id_periksa` (INT): Kunci utama (Primary Key) untuk setiap baris aktivitas peninjauan berkas.
* `id_dokumen` (INT): Kunci tamu (Foreign Key) untuk merujuk ke dokumen mana yang sedang diperiksa.
* `nidn` (VARCHAR, 15): Kunci tamu (Foreign Key) untuk mencatat dosen mana yang melakukan pemeriksaan berkas.
* `tanggal_periksa` (DATETIME): Mencatat waktu pelaksanaan pemeriksaan berkas oleh dosen.
* `catatan_hasil_pemeriksaan` (VARCHAR, 200): Menyimpan teks hasil evaluasi, masukan, atau koreksi dari dosen pemeriksa.

### 7. Tabel Disposisi
* `id_disposisi` (INT): Kunci utama (Primary Key) untuk setiap lembar instruksi resmi pimpinan.
* `id_dokumen` (INT): Kunci tamu (Foreign Key) untuk merujuk pada surat masuk yang membutuhkan disposisi.
* `id_user` (INT): Kunci tamu (Foreign Key) untuk mencatat akun pimpinan (Dekan/Kaprodi) yang mengeluarkan perintah disposisi.
* `tanggal_disposisi` (DATETIME): Mencatat tanggal ketika instruksi disposisi resmi dikeluarkan.
* `isi_instruksi_disposisi` (VARCHAR, 200): Menyimpan teks detail perintah atau disposisi dari pimpinan untuk ditindaklanjuti.

