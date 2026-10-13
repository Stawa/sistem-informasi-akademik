# Analisis Kebutuhan Sistem Informasi Akademik (E-Learning)

[Beranda](../README.md) · [Perancangan](../02_perancangan) · [Panduan](../03_panduan)

## 1. Latar Belakang

Materi perkuliahan, tugas, nilai, dan informasi kelas yang disampaikan melalui berbagai media dapat menyulitkan dosen dan mahasiswa dalam mengakses serta mengelola informasi. Oleh karena itu, Sistem Informasi Akademik berbasis E-Learning dirancang sebagai platform terpusat untuk mendukung kegiatan pembelajaran agar lebih terstruktur, efisien, dan mudah diakses.

## 2. Tujuan Sistem

| No. | Tujuan                                                                 |
| :-: | ---------------------------------------------------------------------- |
|  1  | Mempermudah pengelolaan materi pembelajaran, tugas, kuis, dan nilai.   |
|  2  | Memudahkan mahasiswa mengakses informasi kelas dan mengumpulkan tugas. |
|  3  | Mendukung komunikasi melalui pengumuman kelas.                         |
|  4  | Membantu dosen mencatat kehadiran dan mengevaluasi hasil pembelajaran. |

## 3. Ruang Lingkup

Sistem Informasi Akademik berbasis E-Learning mencakup pengelolaan akun pengguna, mata kuliah, kelas, materi perkuliahan, tugas, kuis, nilai, presensi, dan pengumuman. Sistem digunakan oleh administrator, dosen, dan mahasiswa melalui aplikasi berbasis web.

## 4. Pengguna dan Hak Akses

| Pengguna      | Kebutuhan dan Hak Akses                                                                                          |
| ------------- | ---------------------------------------------------------------------------------------------------------------- |
| Administrator | Mengelola akun, mata kuliah, kelas, penugasan dosen, dan keanggotaan mahasiswa.                                  |
| Dosen         | Mengelola materi, tugas, kuis, presensi, pengumuman, dan nilai pada kelas yang diampu.                           |
| Mahasiswa     | Mengakses kelas yang diikuti, mengunduh materi, mengumpulkan tugas, mengerjakan kuis, dan melihat nilai sendiri. |

## 5. Informasi yang Diperlukan

| Pengguna      | Informasi                                                          |
| ------------- | ------------------------------------------------------------------ |
| Mahasiswa     | NIM, nama lengkap, email, kata sandi, dan foto profil (opsional).  |
| Dosen         | NIDN, nama lengkap, email, kata sandi, dan foto profil (opsional). |
| Administrator | Username, email, kata sandi, dan data akun pengguna yang dikelola. |

### Data Pendukung Pembelajaran

| Informasi             | Data yang Diperlukan                                         |
| --------------------- | ------------------------------------------------------------ |
| Mata Kuliah dan Kelas | Nama mata kuliah, kode, dosen pengampu, dan anggota kelas.   |
| Materi dan Tugas      | Judul, deskripsi, berkas, dan batas waktu pengumpulan tugas. |
| Nilai                 | Nilai tugas atau kuis mahasiswa.                             |
| Presensi              | Tanggal pertemuan dan status kehadiran mahasiswa.            |
| Pengumuman            | Judul, isi, dan tanggal pengumuman.                          |

## 6. Kebutuhan Fungsional

| No. | Kebutuhan                                                          |
| --- | ------------------------------------------------------------------ |
| 01  | Pengguna dapat login dan logout sesuai hak akses.                  |
| 02  | Administrator dapat mengelola akun pengguna dan kelas.             |
| 03  | Dosen dapat mengunggah dan mengelola materi perkuliahan.           |
| 04  | Mahasiswa dapat mengakses materi perkuliahan.                      |
| 05  | Dosen dapat memberikan tugas dan menentukan batas pengumpulan.     |
| 06  | Mahasiswa dapat mengumpulkan tugas secara online.                  |
| 07  | Dosen dapat memberikan nilai dan mahasiswa dapat melihat hasilnya. |
| 08  | Dosen dapat mengelola presensi dan pengumuman kelas.               |
| 09  | Pengguna dapat melihat informasi pembelajaran sesuai hak aksesnya. |

## 7. Kebutuhan Nonfungsional

| Aspek                | Kebutuhan                                                             |
| -------------------- | --------------------------------------------------------------------- |
| Keamanan             | Sistem melindungi data pengguna dan membatasi akses sesuai hak akses. |
| Kemudahan Penggunaan | Sistem memiliki tampilan yang sederhana dan mudah dipahami.           |
| Kinerja              | Sistem dapat memproses dan menampilkan informasi dengan baik.         |
| Aksesibilitas        | Sistem dapat diakses melalui komputer maupun ponsel.                  |

## 8. Kebutuhan terhadap Layanan Cloud

| Kebutuhan            | Layanan Cloud        | Penggunaan                                           |
| -------------------- | -------------------- | ---------------------------------------------------- |
| Menjalankan Aplikasi | Cloud Hosting / PaaS | Menjalankan aplikasi E-Learning secara online.       |
| Penyimpanan Data     | Managed Database     | Menyimpan data pengguna, kelas, tugas, dan nilai.    |
| Penyimpanan Berkas   | Object Storage       | Menyimpan materi, berkas tugas, dan foto profil.     |
| Pencadangan Data     | Cloud Backup         | Mencadangkan data untuk menghindari kehilangan data. |
| Pemantauan Sistem    | Cloud Monitoring     | Memantau kinerja dan kondisi aplikasi.               |
