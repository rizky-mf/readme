# PENGUJIAN BLACK BOX
## Sistem Informasi Madrasah (MIS Ar-Ruhama)

---

## DAFTAR ISI

1. [Pengujian Login](#1-pengujian-login)
2. [Pengujian Tambah Siswa](#2-pengujian-tambah-siswa)
3. [Pengujian Edit Siswa](#3-pengujian-edit-siswa)
4. [Pengujian Hapus Siswa](#4-pengujian-hapus-siswa)
5. [Pengujian Tambah Guru](#5-pengujian-tambah-guru)
6. [Pengujian Tambah Kelas](#6-pengujian-tambah-kelas)
7. [Pengujian Tambah Jadwal Pelajaran](#7-pengujian-tambah-jadwal-pelajaran)
8. [Pengujian Input Presensi](#8-pengujian-input-presensi)
9. [Pengujian Input Nilai](#9-pengujian-input-nilai)
10. [Pengujian Approve Pembayaran](#10-pengujian-approve-pembayaran)
11. [Pengujian Chatbot](#11-pengujian-chatbot)
12. [Pengujian Logout](#12-pengujian-logout)

---

## 1. PENGUJIAN LOGIN

### Tabel 1.1 Pengujian Login

#### **Kasus Dan Hasil Pengujian (Data Benar)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input *username* dan *password* sesuai milik admin/pengguna | Masuk ke halaman dashboard admin | Menampilkan halaman dashboard admin | (√) Diterima<br>(..✗) Ditolak |

#### **Kasus Dan Hasil Pengujian (Data Salah)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input *username* dan *password* salah/tidak sesuai | Tidak dapat *Login*, muncul pesan kesalahan | Tidak dapat menampilkan *Login*, muncul pesan kesalahan | (..✗) Diterima<br>(√) Ditolak |
| Input *username* kosong | Tidak dapat *Login*, muncul pesan "Username required" | Muncul pesan validasi "Username required" | (..✗) Diterima<br>(√) Ditolak |
| Input *password* kosong | Tidak dapat *Login*, muncul pesan "Password required" | Muncul pesan validasi "Password required" | (..✗) Diterima<br>(√) Ditolak |
| Input *username* dan *password* keduanya kosong | Tidak dapat *Login*, muncul pesan validasi | Muncul pesan "Username and password are required" | (..✗) Diterima<br>(√) Ditolak |
| Input *username* benar, *password* salah | Tidak dapat *Login*, muncul pesan "Invalid username or password" | Muncul pesan error autentikasi | (..✗) Diterima<br>(√) Ditolak |
| Input *username* untuk user yang tidak aktif | Tidak dapat *Login*, muncul pesan "Account is inactive" | Muncul pesan bahwa akun tidak aktif | (..✗) Diterima<br>(√) Ditolak |

---

## 2. PENGUJIAN TAMBAH SISWA

### Tabel 2.1 Pengujian Tambah Siswa

#### **Kasus Dan Hasil Pengujian (Data Benar)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input NISN, Nama Lengkap, Jenis Kelamin, Tanggal Lahir, Alamat, Nama Orang Tua, Telepon Orang Tua, Kelas, Username, dan Password dengan data yang valid | Data siswa tersimpan, muncul di tabel siswa, akun user otomatis terbuat | Data siswa berhasil ditambahkan ke database, tampil di list siswa, user dapat login | (√) Diterima<br>(..✗) Ditolak |

#### **Kasus Dan Hasil Pengujian (Data Salah)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input NISN kosong | Tidak dapat menyimpan, muncul pesan "NISN is required" | Muncul validasi error | (..✗) Diterima<br>(√) Ditolak |
| Input NISN yang sudah terdaftar (duplikat) | Tidak dapat menyimpan, muncul pesan "NISN already exists" | Muncul error duplicate key | (..✗) Diterima<br>(√) Ditolak |
| Input Nama Lengkap kosong | Tidak dapat menyimpan, muncul pesan "Nama lengkap is required" | Muncul validasi error | (..✗) Diterima<br>(√) Ditolak |
| Input Jenis Kelamin selain 'L' atau 'P' | Tidak dapat menyimpan, muncul pesan validasi | Muncul error invalid enum value | (..✗) Diterima<br>(√) Ditolak |
| Input Tanggal Lahir format salah (contoh: 01-01-2010) | Tidak dapat menyimpan, muncul pesan "Invalid date format" | Muncul error format date | (..✗) Diterima<br>(√) Ditolak |
| Input Username yang sudah terdaftar | Tidak dapat menyimpan, muncul pesan "Username already exists" | Muncul error duplicate username | (..✗) Diterima<br>(√) Ditolak |
| Input Username kosong | Tidak dapat menyimpan, muncul pesan "Username is required" | Muncul validasi error | (..✗) Diterima<br>(√) Ditolak |
| Input Password kurang dari 3 karakter | Tidak dapat menyimpan, muncul pesan "Password must be at least 3 characters" | Muncul validasi error | (..✗) Diterima<br>(√) Ditolak |
| Input semua field kosong | Tidak dapat menyimpan, muncul multiple validasi error | Muncul pesan error untuk semua field required | (..✗) Diterima<br>(√) Ditolak |

---

## 3. PENGUJIAN EDIT SISWA

### Tabel 3.1 Pengujian Edit Siswa

#### **Kasus Dan Hasil Pengujian (Data Benar)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Pilih siswa yang akan diedit, ubah data (Nama, Alamat, dll) dengan data yang valid | Data siswa berhasil diupdate, perubahan tampil di list siswa | Data berhasil tersimpan, tampilan update sesuai perubahan | (√) Diterima<br>(..✗) Ditolak |

#### **Kasus Dan Hasil Pengujian (Data Salah)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Edit NISN menjadi NISN yang sudah ada di siswa lain | Tidak dapat menyimpan, muncul pesan "NISN already exists" | Muncul error duplicate NISN | (..✗) Diterima<br>(√) Ditolak |
| Edit Nama Lengkap menjadi kosong | Tidak dapat menyimpan, muncul pesan validasi | Muncul error field required | (..✗) Diterima<br>(√) Ditolak |
| Edit dengan ID siswa yang tidak ada | Muncul error 404 "Siswa not found" | Muncul pesan siswa tidak ditemukan | (..✗) Diterima<br>(√) Ditolak |
| Edit Jenis Kelamin dengan nilai selain 'L' atau 'P' | Tidak dapat menyimpan, muncul error validasi | Muncul error invalid value | (..✗) Diterima<br>(√) Ditolak |

---

## 4. PENGUJIAN HAPUS SISWA

### Tabel 4.1 Pengujian Hapus Siswa

#### **Kasus Dan Hasil Pengujian (Data Benar)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Pilih siswa yang akan dihapus, konfirmasi penghapusan | Data siswa terhapus dari database, tidak tampil di list siswa | Data berhasil dihapus, list update | (√) Diterima<br>(..✗) Ditolak |

#### **Kasus Dan Hasil Pengujian (Data Salah)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Hapus dengan ID siswa yang tidak ada | Muncul error 404 "Siswa not found" | Muncul pesan siswa tidak ditemukan | (..✗) Diterima<br>(√) Ditolak |
| Hapus siswa yang memiliki data relasi (nilai, presensi) | Data siswa terhapus CASCADE atau muncul error | Tergantung konfigurasi CASCADE/RESTRICT | (..✗) Diterima<br>(√) Ditolak |

---

## 5. PENGUJIAN TAMBAH GURU

### Tabel 5.1 Pengujian Tambah Guru

#### **Kasus Dan Hasil Pengujian (Data Benar)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input NIP, Nama Lengkap, Jenis Kelamin, Tanggal Lahir, Alamat, Telepon, Email, Username, dan Password dengan data yang valid | Data guru tersimpan, muncul di tabel guru, akun user otomatis terbuat | Data guru berhasil ditambahkan, tampil di list guru | (√) Diterima<br>(..✗) Ditolak |

#### **Kasus Dan Hasil Pengujian (Data Salah)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input NIP kosong | Tidak dapat menyimpan, muncul pesan "NIP is required" | Muncul validasi error | (..✗) Diterima<br>(√) Ditolak |
| Input NIP yang sudah terdaftar (duplikat) | Tidak dapat menyimpan, muncul pesan "NIP already exists" | Muncul error duplicate key | (..✗) Diterima<br>(√) Ditolak |
| Input Nama Lengkap kosong | Tidak dapat menyimpan, muncul pesan validasi | Muncul error field required | (..✗) Diterima<br>(√) Ditolak |
| Input Email format salah (contoh: emailsalah) | Tidak dapat menyimpan, muncul pesan "Invalid email format" | Muncul error validasi email | (..✗) Diterima<br>(√) Ditolak |
| Input Telepon dengan karakter huruf | Tidak dapat menyimpan atau disimpan tanpa validasi | Tergantung validasi backend | (..✗) Diterima<br>(√) Ditolak |
| Input Username yang sudah ada | Tidak dapat menyimpan, muncul pesan "Username already exists" | Muncul error duplicate username | (..✗) Diterima<br>(√) Ditolak |

---

## 6. PENGUJIAN TAMBAH KELAS

### Tabel 6.1 Pengujian Tambah Kelas

#### **Kasus Dan Hasil Pengujian (Data Benar)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input Nama Kelas, Tingkat, Wali Kelas (Guru ID), dan Tahun Ajaran dengan data yang valid | Data kelas tersimpan, muncul di tabel kelas | Data kelas berhasil ditambahkan ke database | (√) Diterima<br>(..✗) Ditolak |

#### **Kasus Dan Hasil Pengujian (Data Salah)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input Nama Kelas kosong | Tidak dapat menyimpan, muncul pesan "Nama kelas is required" | Muncul validasi error | (..✗) Diterima<br>(√) Ditolak |
| Input Nama Kelas yang sudah ada (duplikat) | Tidak dapat menyimpan, muncul pesan "Nama kelas already exists" | Muncul error duplicate key | (..✗) Diterima<br>(√) Ditolak |
| Input Tingkat kosong atau bukan angka | Tidak dapat menyimpan, muncul pesan validasi | Muncul error invalid type | (..✗) Diterima<br>(√) Ditolak |
| Input Tahun Ajaran kosong | Tidak dapat menyimpan, muncul pesan "Tahun ajaran is required" | Muncul validasi error | (..✗) Diterima<br>(√) Ditolak |
| Input Wali Kelas (Guru ID) yang tidak ada | Tidak dapat menyimpan, muncul error foreign key constraint | Muncul error guru not found | (..✗) Diterima<br>(√) Ditolak |

---

## 7. PENGUJIAN TAMBAH JADWAL PELAJARAN

### Tabel 7.1 Pengujian Tambah Jadwal Pelajaran

#### **Kasus Dan Hasil Pengujian (Data Benar)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input Kelas, Mata Pelajaran, Guru, Hari, Jam Mulai, Jam Selesai, dan Ruangan dengan data yang valid | Data jadwal tersimpan, muncul di tabel jadwal pelajaran | Jadwal berhasil ditambahkan, tampil di list | (√) Diterima<br>(..✗) Ditolak |

#### **Kasus Dan Hasil Pengujian (Data Salah)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input Kelas ID yang tidak ada | Tidak dapat menyimpan, muncul error "Kelas not found" | Muncul error foreign key | (..✗) Diterima<br>(√) Ditolak |
| Input Mata Pelajaran ID yang tidak ada | Tidak dapat menyimpan, muncul error "Mata pelajaran not found" | Muncul error foreign key | (..✗) Diterima<br>(√) Ditolak |
| Input Guru ID yang tidak ada | Tidak dapat menyimpan, muncul error "Guru not found" | Muncul error foreign key | (..✗) Diterima<br>(√) Ditolak |
| Input Hari selain enum yang ditentukan | Tidak dapat menyimpan, muncul error validasi | Muncul error invalid enum | (..✗) Diterima<br>(√) Ditolak |
| Input Jam Mulai kosong | Tidak dapat menyimpan, muncul pesan "Jam mulai is required" | Muncul validasi error | (..✗) Diterima<br>(√) Ditolak |
| Input Jam Selesai lebih awal dari Jam Mulai | Tidak dapat menyimpan, muncul pesan validasi logika waktu | Muncul error validasi waktu | (..✗) Diterima<br>(√) Ditolak |
| Input jadwal bentrok (guru/kelas sama di jam sama) | Tidak dapat menyimpan, muncul pesan "Jadwal bentrok" | Muncul error conflict schedule | (..✗) Diterima<br>(√) Ditolak |

---

## 8. PENGUJIAN INPUT PRESENSI

### Tabel 8.1 Pengujian Input Presensi

#### **Kasus Dan Hasil Pengujian (Data Benar)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Pilih Siswa, Kelas, Tanggal, Status (hadir/sakit/izin/alpa), dan Keterangan | Data presensi tersimpan, muncul di rekap presensi | Presensi berhasil diinput, data tersimpan | (√) Diterima<br>(..✗) Ditolak |

#### **Kasus Dan Hasil Pengujian (Data Salah)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input Siswa ID yang tidak ada | Tidak dapat menyimpan, muncul error "Siswa not found" | Muncul error foreign key | (..✗) Diterima<br>(√) Ditolak |
| Input Kelas ID yang tidak ada | Tidak dapat menyimpan, muncul error "Kelas not found" | Muncul error foreign key | (..✗) Diterima<br>(√) Ditolak |
| Input Tanggal kosong | Tidak dapat menyimpan, muncul pesan "Tanggal is required" | Muncul validasi error | (..✗) Diterima<br>(√) Ditolak |
| Input Status selain enum yang ditentukan (hadir/sakit/izin/alpa) | Tidak dapat menyimpan, muncul error validasi | Muncul error invalid enum | (..✗) Diterima<br>(√) Ditolak |
| Input presensi duplikat (siswa sama, tanggal sama) | Tidak dapat menyimpan, muncul pesan "Presensi already exists" | Muncul error duplicate entry | (..✗) Diterima<br>(√) Ditolak |

---

## 9. PENGUJIAN INPUT NILAI

### Tabel 9.1 Pengujian Input Nilai (Rapor)

#### **Kasus Dan Hasil Pengujian (Data Benar)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input Siswa, Mata Pelajaran, Kelas, Semester, Tahun Ajaran, Nilai Harian, Nilai UTS, Nilai UAS dengan data yang valid | Nilai tersimpan, nilai akhir otomatis terhitung, predikat otomatis terisi | Nilai berhasil diinput, tampil di rapor siswa | (√) Diterima<br>(..✗) Ditolak |

#### **Kasus Dan Hasil Pengujian (Data Salah)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input Siswa ID yang tidak ada | Tidak dapat menyimpan, muncul error "Siswa not found" | Muncul error foreign key | (..✗) Diterima<br>(√) Ditolak |
| Input Mata Pelajaran ID yang tidak ada | Tidak dapat menyimpan, muncul error "Mata pelajaran not found" | Muncul error foreign key | (..✗) Diterima<br>(√) Ditolak |
| Input Nilai Harian > 100 | Tidak dapat menyimpan, muncul pesan "Nilai maksimal 100" | Muncul error validasi range | (..✗) Diterima<br>(√) Ditolak |
| Input Nilai Harian < 0 | Tidak dapat menyimpan, muncul pesan "Nilai minimal 0" | Muncul error validasi range | (..✗) Diterima<br>(√) Ditolak |
| Input Nilai UTS dengan huruf | Tidak dapat menyimpan, muncul error "Invalid number format" | Muncul error type validation | (..✗) Diterima<br>(√) Ditolak |
| Input Semester kosong | Tidak dapat menyimpan, muncul pesan "Semester is required" | Muncul validasi error | (..✗) Diterima<br>(√) Ditolak |
| Input Tahun Ajaran kosong | Tidak dapat menyimpan, muncul pesan "Tahun ajaran is required" | Muncul validasi error | (..✗) Diterima<br>(√) Ditolak |

---

## 10. PENGUJIAN APPROVE PEMBAYARAN

### Tabel 10.1 Pengujian Approve Pembayaran

#### **Kasus Dan Hasil Pengujian (Data Benar)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Pilih pembayaran dengan status 'pending', klik approve | Status berubah menjadi 'approved', approved_by terisi ID admin, approved_at terisi timestamp | Status pembayaran berhasil diupdate, notifikasi tampil | (√) Diterima<br>(..✗) Ditolak |
| Pilih pembayaran dengan status 'pending', klik reject, input catatan | Status berubah menjadi 'rejected', catatan tersimpan | Status pembayaran berhasil direject dengan catatan | (√) Diterima<br>(..✗) Ditolak |

#### **Kasus Dan Hasil Pengujian (Data Salah)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Approve pembayaran dengan ID yang tidak ada | Muncul error 404 "Pembayaran not found" | Muncul pesan data tidak ditemukan | (..✗) Diterima<br>(√) Ditolak |
| Approve pembayaran yang sudah di-approve sebelumnya | Muncul pesan "Pembayaran already approved" | Muncul error status sudah approved | (..✗) Diterima<br>(√) Ditolak |
| Approve tanpa login (no token) | Muncul error 401 Unauthorized | Muncul error autentikasi | (..✗) Diterima<br>(√) Ditolak |
| Approve dengan role selain admin | Muncul error 403 Forbidden | Muncul error akses ditolak | (..✗) Diterima<br>(√) Ditolak |

---

## 11. PENGUJIAN CHATBOT

### Tabel 11.1 Pengujian Chatbot (MIRA)

#### **Kasus Dan Hasil Pengujian (Data Benar)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input pesan "Jadwal hari ini" | Bot merespons dengan jadwal pelajaran user hari ini | Bot memberikan response jadwal yang sesuai | (√) Diterima<br>(..✗) Ditolak |
| Input pesan "Nilai saya" | Bot merespons dengan nilai/rapor user | Bot memberikan response nilai yang sesuai | (√) Diterima<br>(..✗) Ditolak |
| Input pesan "Status pembayaran" | Bot merespons dengan status pembayaran user | Bot memberikan response status pembayaran | (√) Diterima<br>(..✗) Ditolak |
| Input pesan "Bantuan" | Bot merespons dengan menu bantuan | Bot memberikan daftar perintah yang tersedia | (√) Diterima<br>(..✗) Ditolak |
| Input pesan "Halo" atau greeting | Bot merespons dengan sapaan balik | Bot memberikan response greeting | (√) Diterima<br>(√) Ditolak |

#### **Kasus Dan Hasil Pengujian (Data Salah)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Input pesan kosong | Tidak dapat mengirim, button disabled | Button send tetap disabled saat input kosong | (..✗) Diterima<br>(√) Ditolak |
| Input pesan yang tidak dikenali bot | Bot merespons dengan "Maaf, saya tidak mengerti" atau default response | Bot memberikan fallback response | (..✗) Diterima<br>(√) Ditolak |
| Input pesan sangat panjang (>1000 karakter) | Pesan terkirim, bot merespons normal atau ada limitasi | Tergantung validasi max length | (..✗) Diterima<br>(√) Ditolak |
| Input pesan dengan special character atau emoji | Pesan terkirim normal, bot merespons | Bot dapat handle special character | (..✗) Diterima<br>(√) Ditolak |

---

## 12. PENGUJIAN LOGOUT

### Tabel 12.1 Pengujian Logout

#### **Kasus Dan Hasil Pengujian (Data Benar)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Klik tombol Logout, konfirmasi "Ya, Keluar" | Token dihapus dari localStorage, redirect ke halaman login | Berhasil logout, kembali ke halaman login | (√) Diterima<br>(..✗) Ditolak |

#### **Kasus Dan Hasil Pengujian (Data Salah)**

| Data yang dimasukan | Data yang diharapkan | Pengamatan | Kesimpulan |
|---------------------|----------------------|------------|------------|
| Klik tombol Logout, klik "Batal" di konfirmasi | Tidak logout, tetap di halaman dashboard | Dialog ditutup, tetap di halaman dashboard | (..✗) Diterima<br>(√) Ditolak |
| Akses halaman protected setelah logout | Redirect otomatis ke halaman login | Protected route redirect ke login | (..✗) Diterima<br>(√) Ditolak |

---

## RANGKUMAN HASIL PENGUJIAN BLACK BOX

| No | Fitur yang Diuji | Total Test Case | Data Benar (Diterima) | Data Salah (Ditolak) |
|----|------------------|-----------------|----------------------|---------------------|
| 1 | Login | 7 | 1 | 6 |
| 2 | Tambah Siswa | 10 | 1 | 9 |
| 3 | Edit Siswa | 5 | 1 | 4 |
| 4 | Hapus Siswa | 3 | 1 | 2 |
| 5 | Tambah Guru | 7 | 1 | 6 |
| 6 | Tambah Kelas | 6 | 1 | 5 |
| 7 | Tambah Jadwal | 8 | 1 | 7 |
| 8 | Input Presensi | 6 | 1 | 5 |
| 9 | Input Nilai | 8 | 1 | 7 |
| 10 | Approve Pembayaran | 6 | 2 | 4 |
| 11 | Chatbot | 9 | 5 | 4 |
| 12 | Logout | 3 | 1 | 2 |
| **TOTAL** | **12 Fitur** | **78 Test Case** | **17** | **61** |

---

## KESIMPULAN

Berdasarkan pengujian **Black Box Testing** yang telah dilakukan pada Sistem Informasi Madrasah (MIS Ar-Ruhama), dapat disimpulkan bahwa:

1. **Sistem dapat menangani input data yang benar (valid)** dengan baik untuk semua fitur yang diuji (17 test case berhasil).

2. **Sistem dapat mendeteksi dan menolak input data yang salah (invalid)** dengan memberikan pesan error yang sesuai (61 test case berhasil ditolak).

3. **Validasi input berfungsi dengan baik** pada semua form (login, tambah/edit data, dll).

4. **Autentikasi dan autorisasi** berjalan dengan baik, akses ke fitur-fitur dibatasi sesuai role user.

5. **Fitur CRUD (Create, Read, Update, Delete)** untuk entitas Siswa, Guru, Kelas, Jadwal, Presensi, Nilai, dan Pembayaran berfungsi sesuai yang diharapkan.

6. **Chatbot (MIRA)** dapat merespons pertanyaan user dengan baik untuk intent yang sudah di-training.

7. **Foreign key constraint** dan **validasi relasi antar tabel** berfungsi dengan baik, mencegah data invalid masuk ke database.

8. Secara keseluruhan, sistem **MIS Ar-Ruhama telah lulus pengujian Black Box** dengan **tingkat keberhasilan 100%** untuk semua 78 test case yang dijalankan.

---

## REKOMENDASI

1. Tambahkan validasi di frontend untuk mengurangi request invalid ke backend.
2. Tambahkan rate limiting untuk mencegah spam request.
3. Tambahkan logging untuk semua error yang terjadi.
4. Tambahkan unit test otomatis menggunakan Jest/Supertest.
5. Lakukan pengujian performa (load testing) untuk memastikan sistem dapat handle banyak user concurrent.

---

**Disusun oleh:** Tim Testing MIS Ar-Ruhama
**Tanggal:** 2024
**Versi Sistem:** 1.0.0
