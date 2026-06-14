# Sistem Manajemen Arsip Surat dan Dokumen Digital
### Proyek implementasi basis data relasional untuk Sistem Manajemen Arsip Surat dan Dokumen Digital guna mengotomatisasi pencatatan surat, digitalisasi berkas akademik, serta pelacakan verifikasi dan disposisi.

# NAMA ANGGOTA KELOMPOK 7
## Eyja Kurniawan (2501020094)
## Yazira Sartika (2501020103)
## Raihan Parsa Ahza Hamizan (2501200104)
## Naufal Putra Azjril (2501020108)

# STUDI KASUS
Sistem Manajemen Arsip Surat dan Dokumen Digital merupakan sistem berbasis basis data yang dirancang untuk membantu pengelolaan tata kelola persuratan serta arsip dokumen akademik di lingkungan Program Studi Teknik Informatika secara digital dan otomatis. Sistem ini digunakan untuk mencatat aktivitas sirkulasi dokumen mulai dari pengajuan berkas, proses verifikasi, pemeriksaan, hingga disposisi pimpinan secara real-time. Sistem ini melibatkan beberapa pengguna seperti mahasiswa, staf tata usaha (TU), dosen, dan dekan/kaprodi. Setiap dokumen yang masuk ke dalam sistem akan dicatat ke dalam basis data sehingga informasi status berkas dapat dikelola dengan lebih teratur dan mudah dilacak. Dengan adanya sistem ini, proses disposisi dan pencarian arsip menjadi lebih cepat, akurat, aman, dan mengurangi ketergantungan terhadap pencatatan fisik secara manual.

# LATAR BELAKANG DAN TUJUAN SISTEM
## Latar Belakang
Program Studi Teknik Informatika setiap harinya menerima dan mengeluarkan berbagai macam surat serta dokumen akademik, seperti Surat Keputusan (SK) Dosen, surat pengantar penelitian mahasiswa, berkas proposal, hingga draf skripsi final. Namun, saat ini proses pencatatan dan pengarsipan dokumen-dokumen tersebut masih dilakukan secara manual menggunakan buku besar atau disimpan secara terpisah-pisah di Google Drive pribadi milik staf. 
Sistem penyimpanan yang belum terpusat ini menimbulkan beberapa masalah utama: 
•	Pencarian data lambat: Staf Tata Usaha (TU) membutuhkan waktu lama untuk mencari kembali dokumen fisik atau file digital yang terselip. 
•	Risiko data hilang: Surat fisik rawan rusak atau hilang, dan file digital di drive pribadi berisiko terhapus. 
•	Proses disposisi terhambat: Alur instruksi dari Ketua Prodi ke dosen terkait surat masuk seringkali lambat karena harus dilakukan secara manual atau lewat pesan teks biasa yang tertumpuk. 
Oleh karena itu, diperlukan sebuah perancangan basis data yang terstruktur untuk membangun Sistem Manajemen Arsip Surat dan Dokumen Digital. Sistem ini diharapkan mampu mengintegrasikan seluruh data arsip, mempermudah pencarian, serta menjaga keamanan data dokumen penting di lingkungan program studi.

## Tujuan Sistem
Membuat rancangan basis data yang mampu mengintegrasikan data aktor utama (Mahasiswa, Staf TU, Dosen, dan Dekan/Kaprodi) beserta hak aksesnya masing-masing dalam sistem manajemen dokumen.
Mengotomatisasi Pencatatan Siklus Hidup Dokumen Membangun struktur tabel yang dapat merekam setiap perubahan status dokumen secara kronologis, mulai dari dokumen pertama kali diunggah (upload), diverifikasi oleh TU, diperiksa oleh Dosen, hingga diberi disposisi oleh Dekan/Kaprodi.
Mendukung Alur Kerja Pemeriksaan dan Disposisi Berjenjang Merancang relasi antar-tabel yang mampu mencatat data hasil pemeriksaan oleh Dosen serta lembar disposisi dari Dekan/Kaprodi, sehingga rekam jejak keputusan pimpinan terhadap dokumen tersebut tersimpan dengan baik.
Menghasilkan Query untuk Pelaporan dan Pemantauan Status (Tracking) Membuat perintah SQL (Query) spesifik untuk menghasilkan laporan operasional yang dibutuhkan pihak kampus, seperti:
•	Menampilkan daftar dokumen mahasiswa yang masih tertunda (pending) di meja Staf TU.
•	Menampilkan rekapitulasi dokumen yang sedang diperiksa atau didisposisikan oleh Dosen/Dekan.
•	Menyajikan laporan akhir mengenai jumlah dokumen yang berhasil diselesaikan (status: Selesai) dalam periode tertentu.


