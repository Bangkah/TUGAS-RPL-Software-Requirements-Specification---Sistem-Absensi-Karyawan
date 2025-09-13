# Software Requirements Specification (SRS)
**Sistem Absensi Karyawan Berbasis Web (Laravel 12 + Tailwind CSS)**  
**Versi 1.0 – 4 September 2025**

---

## Daftar Isi

1. [Pendahuluan](#1-pendahuluan)
2. [Deskripsi Keseluruhan](#2-deskripsi-keseluruhan)
3. [Kebutuhan Fungsional](#3-kebutuhan-fungsional)
4. [Kebutuhan Non-Fungsional](#4-kebutuhan-non-fungsional)
5. [Antarmuka Pengguna](#5-antarmuka-pengguna-wireframe-level)
6. [Database Schema](#6-database-schema-ringkas)
7. [Alur Kerja](#7-alur-kerja-sequence-diagram)
8. [Lingkungan Pengembangan & DevOps](#8-lingkungan-pengembangan--devops)
9. [Rencana Pengujian](#9-rencana-pengujian)
10. [Deliverable & Timeline](#10-deliverable--timeline)
11. [Lampiran](#11-lampiran)

---

## 1. Pendahuluan

### 1.1 Tujuan Dokumen
Dokumen ini mendefinisikan kebutuhan fungsional dan non-fungsional sebagai dasar pengembangan sistem absensi karyawan berbasis web menggunakan Laravel 12 dan Tailwind CSS. Sistem ini dirancang dari awal sebagai bagian dari tugas mata kuliah Workshop Web Lanjut, dengan tujuan memberikan solusi modern, responsif, dan aman untuk manajemen absensi karyawan secara digital.

### 1.2 Ruang Lingkup

| Aspek | Detail |
|---|---|
| **Nama Produk** | AbsensiKaryawan-L12 |
| **Platform** | Web Browser (desktop & mobile) |
| **Pengguna** | Admin, Operator, Pegawai |
| **Lokasi Deploy** | Localhost (Development Environment) |
| **Maksimal Pengguna Simultan** | 4 orang (Tim Development) |

### 1.3 Istilah & Singkatan

| Istilah | Arti |
|---|---|
| QR Code | Quick Response Code untuk absensi otomatis |
| RBAC | Role-Based Access Control |
| CSV | Comma-Separated Values (format export laporan) |
| Excel | File .xlsx (format export laporan) |

---

## 2. Deskripsi Keseluruhan

### 2.1 Fungsi Utama
1. Manajemen data master (jabatan, pengguna, hari libur).
2. Absensi masuk & pulang via QR Code **atau** input manual NIP.
3. Pengajuan & persetujuan izin.
4. Laporan kehadiran harian, mingguan, bulanan (export Excel/CSV).
5. Role-based dashboard (Admin / Operator / Pegawai).

### 2.2 Arsitektur Teknologi

| Layer | Teknologi |
|---|---|
| Backend | Laravel 12.x (PHP 8.3) |
| Frontend | Blade + Livewire 3 + Tailwind CSS 3.x |
| DBMS | MySQL 8.x |
| Auth | Laravel Sanctum (session-based) |
| QR Library | `simplesoftwareio/simple-qrcode` |
| Excel Export | `maatwebsite/excel` 3.x |
| Tabel Interaktif | Livewire PowerGrid |

---

## 3. Kebutuhan Fungsional

### 3.1 Manajemen Pengguna & RBAC

| ID | Fitur | Deskripsi Detail |
|---|---|---|
| F-01 | CRUD Pegawai | Tambah/Edit/Hapus pegawai (nama, email, NIP unik, jabatan, foto). |
| F-02 | CRUD Operator & Admin | Sama dengan pegawai namun role = operator / admin. |
| F-03 | Reset Password | Admin/Operator dapat reset password pegawai; pegawai dapat ubah password sendiri. |
| F-04 | Role Permissions | Hak akses tabel:<br>- Admin = semua fitur<br>- Operator = absensi, izin, laporan (tidak bisa CRUD jabatan)<br>- Pegawai = absensi, lihat riwayat, ajukan izin |

### 3.2 Manajemen Jabatan & Hari Libur

| ID | Fitur | Deskripsi |
|---|---|---|
| F-05 | CRUD Jabatan | Nama jabatan, deskripsi, tingkat (untuk urutan laporan). |
| F-06 | CRUD Hari Libur | Tanggal, nama hari libur, flag nasional/lokal. Sistem otomatis menandai absensi "libur". |

### 3.3 Absensi

| ID | Fitur | Deskripsi |
|---|---|---|
| F-07 | Generate QR Code | Setiap hari sistem generate QR unik (berisi token 6 digit + tanggal). |
| F-08 | Scan QR | Pegawai scan → validasi token & lokasi (opsional) → catat jam masuk. |
| F-09 | Input Manual | Pegawai ketik NIP + PIN → catat masuk / pulang. |
| F-10 | Validasi Waktu | - Masuk: 07:00–09:00 (terlambat jika >09:00)<br>- Pulang: 16:00–19:00 (pulang cepat jika <16:00) |
| F-11 | Tidak Absen Pulang | Sistem otomatis tandai "belum absen pulang" setelah 24:00. |
| F-12 | Toleransi Keterlambatan | Admin setting menit toleransi; default 5 menit. |

### 3.4 Izin & Cuti

| ID | Fitur | Deskripsi |
|---|---|---|
| F-13 | Pengajuan Izin | Pegawai pilih tanggal, jenis (sakit/izin/cuti), upload bukti (jpg/pdf). |
| F-14 | Persetujuan | Operator/Admin approve/reject + keterangan; pegawai dapat notifikasi email. |
| F-15 | Saldo Cuti | Admin set saldo cuti tahunan; sistem kurangi otomatis. |

### 3.5 Laporan & Export

| ID | Fitur | Deskripsi |
|---|---|---|
| F-16 | Rekap Harian | Tabel pegawai hadir, izin, alfa, terlambat. Filter tanggal. |
| F-17 | Rekap Bulanan | Summary per pegawai (jumlah hadir, izin, alfa, jam terlambat). |
| F-18 | Export | Excel (.xlsx) & CSV; nama file auto: `rekap_absensi_2025_09.xlsx`. |

### 3.6 Dashboard

| ID | Fitur | Deskripsi |
|---|---|---|
| F-19 | Admin Dashboard | Statistik total pegawai, hadir hari ini, izin pending, grafik kehadiran 7 hari. |
| F-20 | Pegawai Dashboard | Kartu kehadiran hari ini, riwayat 5 hari terakhir, sisa cuti, tombol absensi. |

---

## 4. Kebutuhan Non-Fungsional

| ID | Kategori | Spesifikasi |
|---|---|---|
| NF-01 | Performa | Halaman load < 3 detik (untuk development localhost). |
| NF-02 | Skalabilitas | Dapat menampung 10 pegawai, 1000 record absensi untuk testing tim (4 orang). |
| NF-03 | Keamanan | - Password minimal 8 karakter<br>- Hash bcrypt<br>- Rate-limit login 5 kali/gagal<br>- QR token expire 1 hari |
| NF-04 | Responsive | Tailwind breakpoint: mobile (≤640px), tablet (≤1024px), desktop. |
| NF-05 | Backup | Manual backup DB untuk development localhost (tidak perlu otomatis). |
| NF-06 | Audit Trail | Semua aksi admin (CRUD, approve) tercatat (tabel `audit_logs`). |

---

## 5. Antarmuka Pengguna (Wireframe-level)

### 5.1 Login
- Field email & password, tombol "Masuk", link "Lupa Password".

### 5.2 Dashboard Admin
- **Navbar:** Logo, nama admin, dropdown logout.
- **Sidebar:** Dashboard, Pegawai, Jabatan, Hari Libur, Laporan, Pengaturan.
- **Main Content:**
  - Card: Total Pegawai (ikon orang)
  - Card: Hadir Hari Ini (ikon hadir)
  - Card: Izin Pending (ikon izin)
  - Grafik Bar kehadiran 7 hari (Chart.js/Livewire Charts)

### 5.3 Scan QR
- Full-screen camera (mobile) atau modal pop-up (desktop).
- Tombol "Input NIP Manual" untuk fallback.

### 5.4 Form Pengajuan Izin
- Datepicker, dropdown jenis izin, textarea alasan, upload file (drag & drop), tombol "Kirim".

---

## 6. Database Schema (Ringkas)

| Tabel | Kolom Utama |
|---|---|
| users | id, name, email, nip, password, jabatan_id, role, foto_path, remember_token, timestamps |
| jabatans | id, nama_jabatan, deskripsi, level, timestamps |
| absensis | id, user_id, tanggal, jam_masuk, jam_keluar, status_hadir, terlambat_menit, pulang_cepat_menit, keterangan, timestamps |
| izins | id, user_id, tanggal_mulai, tanggal_selesai, jenis, alasan, file_bukti_path, status, approved_by, approved_at, timestamps |
| hari_liburs | id, tanggal, nama_libur, jenis, timestamps |
| audit_logs | id, user_id, aksi, tabel, data_lama, data_baru, ip_address, timestamps |

---

## 7. Alur Kerja (Sequence Diagram)

### 7.1 Absensi Masuk via QR
1. Pegawai → Klik "Absensi Masuk"
2. Sistem → Generate token & QR
3. Pegawai → Scan QR
4. Sistem → Validasi token & waktu → Simpan absensi → Tampilkan pesan sukses / gagal

---

## 8. Lingkungan Pengembangan & DevOps

| Item | Nilai |
|---|---|
| Repo Git | localhost/git atau GitHub private repo |
| Branch Strategy | main / develop (sederhana untuk tim 4 orang) |
| CI/CD | Manual testing dan deployment:<br>- Manual PHPUnit testing<br>- Local development server<br>- Manual code review |
| Staging URL | http://localhost:8000 atau http://127.0.0.1:8000 |
| Environment Variables | .env untuk localhost (DB_HOST=127.0.0.1, APP_ENV=local) |

---

## 9. Rencana Pengujian

| Jenis Uji | Cakupan |
|---|---|
| Unit Test | Model scope, service absensi, permission gate |
| Feature Test | CRUD pegawai, scan QR, approve izin |
| Browser Test | Dusk: login, absensi, export Excel |
| Load Test | 4 user simultan testing (sesuai jumlah tim) |

---

## 10. Deliverable & Timeline

| Minggu | Deliverable |
|---|---|
| 1 | Setup Laravel 12 + Tailwind + Auth + Local Database |
| 2 | CRUD Jabatan & Pegawai + Testing 4 user |
| 3 | Fitur QR Absensi + Manual + Local Testing |
| 4 | Izin & Cuti + Tim Testing |
| 5 | Laporan + Export + Localhost Optimization |
| 6 | Dashboard + Responsive + Team Review |
| 7 | Testing & Bugfix (4 orang tim) |
| 8 | Final Testing & Documentation |

---

## 11. Lampiran

- **A.** Setup guide untuk team development (4 orang)
- **B.** Checklist testing untuk tim development

---

## Tanda Tangan

#### **Disusun oleh: Muhammad Dhiyaul Atha**
#### **Disetujui oleh: FOUR A TEAM**
#### **Tanggal: 4 September 2025**

---
