# Rancangan Database Sistem Informasi Akademik (E-Learning)

[Beranda](../README.md) · [Analisis](../01_analisis) · [Rancangan Sistem](rancangan_sistem.md) · [Panduan](../03_panduan)

## 1. Gambaran Umum

Database dirancang untuk menyimpan dan mengelola informasi pengguna, kelas, materi, tugas, kuis, nilai, presensi, serta pengumuman. Setiap pengguna memiliki akun dengan peran administrator, dosen, atau mahasiswa. Dosen dapat membuat kelas, sedangkan mahasiswa dapat bergabung menggunakan kode kelas. Administrator bertugas mengelola akun dan memantau aktivitas sistem.

## 2. Tabel Pengguna

### pengguna

| Kolom            | Tipe Data    | Keterangan                                 |
| ---------------- | ------------ | ------------------------------------------ |
| id_pengguna (PK) | BIGINT       | ID unik pengguna                           |
| nama_lengkap     | VARCHAR(150) | Nama lengkap pengguna                      |
| email            | VARCHAR(150) | Email untuk login, unik                    |
| password_hash    | VARCHAR(255) | Hash kata sandi                            |
| peran            | VARCHAR(20)  | Administrator, dosen, atau mahasiswa       |
| nomor_identitas  | VARCHAR(30)  | NIM atau NIP, opsional untuk administrator |
| foto_profil      | VARCHAR(255) | Referensi foto profil, opsional            |
| status_akun      | BOOLEAN      | Status aktif atau nonaktif                 |

Seluruh pengguna disimpan dalam satu tabel. Administrator tidak memerlukan tabel khusus karena hak akses ditentukan berdasarkan peran.

## 3. Tabel Kelas

### kelas

| Kolom         | Tipe Data    | Keterangan                |
| ------------- | ------------ | ------------------------- |
| id_kelas (PK) | BIGINT       | ID unik kelas             |
| id_dosen (FK) | BIGINT       | Dosen pembuat kelas       |
| nama_kelas    | VARCHAR(100) | Nama kelas                |
| mata_kuliah   | VARCHAR(150) | Nama mata kuliah          |
| kode_kelas    | VARCHAR(20)  | Kode unik untuk bergabung |
| deskripsi     | TEXT         | Deskripsi kelas, opsional |
| dibuat_pada   | TIMESTAMP    | Waktu pembuatan kelas     |

Kelas dibuat dan dikelola oleh dosen. Mahasiswa dapat bergabung menggunakan kode kelas yang diberikan dosen.

### anggota_kelas

| Kolom             | Tipe Data | Keterangan               |
| ----------------- | --------- | ------------------------ |
| id_anggota (PK)   | BIGINT    | ID unik keanggotaan      |
| id_kelas (FK)     | BIGINT    | Kelas yang diikuti       |
| id_mahasiswa (FK) | BIGINT    | Mahasiswa yang bergabung |
| bergabung_pada    | TIMESTAMP | Waktu bergabung          |

Kombinasi `id_kelas` dan `id_mahasiswa` harus UNIQUE agar mahasiswa tidak terdaftar dua kali pada kelas yang sama.

## 4. Tabel Materi

### materi

| Kolom          | Tipe Data    | Keterangan                    |
| -------------- | ------------ | ----------------------------- |
| id_materi (PK) | BIGINT       | ID unik materi                |
| id_kelas (FK)  | BIGINT       | Kelas tempat materi diberikan |
| judul          | VARCHAR(150) | Judul materi                  |
| deskripsi      | TEXT         | Penjelasan materi, opsional   |
| file_key       | VARCHAR(255) | Referensi berkas materi       |
| diunggah_pada  | TIMESTAMP    | Waktu unggah materi           |

Materi diunggah oleh dosen dan dapat diakses oleh mahasiswa yang tergabung dalam kelas.

## 5. Tabel Tugas dan Kuis

### tugas_kuis

| Kolom         | Tipe Data    | Keterangan                   |
| ------------- | ------------ | ---------------------------- |
| id_tugas (PK) | BIGINT       | ID unik tugas atau kuis      |
| id_kelas (FK) | BIGINT       | Kelas tempat tugas diberikan |
| jenis         | VARCHAR(10)  | Tugas atau kuis              |
| judul         | VARCHAR(150) | Judul tugas atau kuis        |
| instruksi     | TEXT         | Petunjuk pengerjaan          |
| tenggat       | TIMESTAMP    | Batas waktu pengumpulan      |
| dibuat_pada   | TIMESTAMP    | Waktu pembuatan              |

Tugas dan kuis menggunakan tabel yang sama karena memiliki proses pengerjaan dan pengumpulan yang serupa. Kolom `jenis` digunakan untuk membedakan keduanya.

### pengumpulan

| Kolom               | Tipe Data    | Keterangan                       |
| ------------------- | ------------ | -------------------------------- |
| id_pengumpulan (PK) | BIGINT       | ID unik pengumpulan              |
| id_tugas (FK)       | BIGINT       | Tugas atau kuis yang dikumpulkan |
| id_mahasiswa (FK)   | BIGINT       | Mahasiswa yang mengumpulkan      |
| file_key            | VARCHAR(255) | Referensi berkas jawaban         |
| dikumpulkan_pada    | TIMESTAMP    | Waktu pengumpulan                |
| nilai               | DECIMAL(5,2) | Nilai 0–100, opsional            |
| umpan_balik         | TEXT         | Komentar dosen, opsional         |

Setiap mahasiswa dapat mengumpulkan jawaban untuk tugas atau kuis pada kelas yang diikuti. Kombinasi `id_tugas` dan `id_mahasiswa` harus UNIQUE agar setiap mahasiswa memiliki satu pengumpulan aktif untuk setiap tugas atau kuis.

## 6. Tabel Presensi

### pertemuan

| Kolom             | Tipe Data    | Keterangan             |
| ----------------- | ------------ | ---------------------- |
| id_pertemuan (PK) | BIGINT       | ID unik pertemuan      |
| id_kelas (FK)     | BIGINT       | Kelas tempat pertemuan |
| tanggal           | DATE         | Tanggal pertemuan      |
| topik             | VARCHAR(150) | Topik pembelajaran     |

### presensi

| Kolom             | Tipe Data   | Keterangan                         |
| ----------------- | ----------- | ---------------------------------- |
| id_presensi (PK)  | BIGINT      | ID unik presensi                   |
| id_pertemuan (FK) | BIGINT      | Pertemuan yang dicatat             |
| id_mahasiswa (FK) | BIGINT      | Mahasiswa yang mengikuti pertemuan |
| status            | VARCHAR(10) | Hadir, izin, sakit, atau alpa      |

Dosen mencatat kehadiran mahasiswa pada setiap pertemuan. Kombinasi `id_pertemuan` dan `id_mahasiswa` harus UNIQUE agar tidak terjadi pencatatan ganda.

## 7. Tabel Pengumuman

### pengumuman

| Kolom              | Tipe Data    | Keterangan                |
| ------------------ | ------------ | ------------------------- |
| id_pengumuman (PK) | BIGINT       | ID unik pengumuman        |
| id_kelas (FK)      | BIGINT       | Kelas penerima pengumuman |
| judul              | VARCHAR(150) | Judul pengumuman          |
| isi                | TEXT         | Isi pengumuman            |
| dibuat_pada        | TIMESTAMP    | Waktu publikasi           |

Pengumuman dibuat oleh dosen dan dapat dibaca oleh mahasiswa yang tergabung dalam kelas.

## 8. Tabel Log Aktivitas

### log_aktivitas

| Kolom            | Tipe Data    | Keterangan                        |
| ---------------- | ------------ | --------------------------------- |
| id_log (PK)      | BIGINT       | ID unik log aktivitas             |
| id_pengguna (FK) | BIGINT       | Pengguna yang melakukan aktivitas |
| aktivitas        | VARCHAR(255) | Deskripsi aktivitas               |
| waktu            | TIMESTAMP    | Waktu aktivitas                   |

Log aktivitas digunakan untuk mencatat aktivitas penting pengguna dan membantu administrator memantau sistem.
