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

