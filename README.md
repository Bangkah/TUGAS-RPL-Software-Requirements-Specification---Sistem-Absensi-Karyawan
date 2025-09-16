# PROJEK: SISTEM MANAJEMEN ABSENSI KARYAWAN  
*(LEAS – Laravel Employee Attendance System)*

---

## LATAR BELAKANG  
Di banyak organisasi, proses absensi masih mengandalkan kertas, sidik jari berdiri sendiri, atau Google Form. Akibatnya:  
- Lembar absen mudah rusak / hilang  
- Kasus “titip tanda-tangan” masih sering terjadi  
- HR membutuhkan hari-an untuk merangkum gaji dan lembur  
- Tidak ada bukti visual (selfie) saat datang / pulang  
- Pimpinan kesulitan memantau karyawan yang bekerja di luar kantor (remote, proyek lapangan)  

LEAS dibuat untuk menggantikan cara-cara manual tersebut dengan satu aplikasi web yang mencatat kehadiran secara digital, otomatis menghitung keterlambatan, serta menyajikan laporan real-time agar seluruh proses HR menjadi lebih cepat, akurat, dan transparan.

---

## TUJUAN UTAMA  
1. Check-in / check-out dilakukan ≤ 5 detik  
2. Sistem otomatis menghitung menit keterlambatan dan jam lembur  
3. Admin & manajer langsung menerima notifikasi jika ada karyawan terlambat  
4. Setiap kehadiran dilengkapi foto selfie + koordinat GPS sebagai bukti  
5. Rekap gaji, lembur, dan statistik kehadiran dapat diunduh dalam satu klik (PDF atau Excel)

---

## FUNGSI (FITUR) INTI  
- **Autentikasi multi-role** – satu login, hak akses berbeda untuk karyawan, HRD, dan manajer  
- **Master data** – CRUD karyawan, departemen, jabatan, pola shift, hari libur nasional  
- **Absensi digital** – dua cara:  
  - Scan QR Code di pintu masuk (via smartphone)  
  - Tombol Check-in pada halaman web (dengan validasi lokasi 100 m)  
  Wajib mengunggah foto selfie; sistem mencatat waktu serta GPS  
- **Pengajuan cuti & lembur** – formulir online, alur approval 1 atau 2 level, notifikasi ke email / WhatsApp  
- **Dashboard real-time** – tampilan “who-is-in”, jumlah hadir, terlambat, alpha, grafik mingguan (Chart.js)  
- **Perhitungan otomatis** – lama kerja, menit telat, jam lembur, total per periode (bulanan / mingguan)  
- **Notifikasi** – e-mail native + WhatsApp (melalui Wablas) untuk reminder, hasil approval, dan ringkasan harian  
- **Laporan & export** – slip gaji (PDF), rekap bulanan (Excel), grafik pie / bar kehadiran  
- **API mobile** – endpoint REST (Laravel Sanctum) agar developer internal dapat membangun aplikasi Android / iOS check-in/out

---

## MANFAAT APLIKASI
- HRD mengurangi waktu rekap dari beberapa hari menjadi hitungan menit, serta meminimalkan kesalahan hitung manual  
- Pimpinan dapat melihat kinerja kehadiran tim secara langsung, tanpa menunggu laporan hard-copy  
- Karyawan merasa proses lebih adil karena tidak dapat dimanipulasi (foto + GPS)  
- Semua data tersimpan aman di database dan dapat dijadikan bukti sah jika dibutuhkan di masa depan  
- Payroll lebih cepat – file export langsung dapat diimpor ke sistem penggajian

---

## ALUR KERJA SISTEM (KONSEP)  
1. **Persiapan data**  
   Admin mengunggah data karyawan, menetapkan departemen, jadwal shift, dan hari libur  

2. **Proses absensi**  
   Karyawan scan QR-Code atau klik tombol Check-in → unggah selfie → sistem validasi lokasi & waktu → record tersimpan  

3. **Pemantauan harian**  
   Dashboard real-time menampilkan status hadir; HRD & manajer menerima notifikasi jika ada yang terlambat  

4. **Pengajuan cuti / lembur**  
   Karyawan mengisi form online → atasan menerima notifikasi → approve / reject → hasil dikirim via e-mail & WhatsApp  

5. **Penutupan periode**  
   HRD memilih periode → klik “Export Rekap” → sistem menghasilkan PDF (slip gaji) dan Excel (rekap bulanan) untuk kebutuhan payroll

Dengan alur tersebut, LEAS diharapkan menjadi solusi presensi modern yang praktis, aman, dan siap dipakai oleh perusahaan skala kecil hingga menengah.


## Berikut adalah ketentuan yang di kerjakan terpenuhi :
1.  Flow diagram / usecase diagram sederhana yang menggambarkan fitur sistem
  <img width="3522" height="1491" alt="image" src="https://github.com/user-attachments/assets/82c939b7-5c58-4fd7-a786-804b27138383" />

2. Mengatur Status Absen masuk yang dilakukan karyawan sebelum jam 09.00 pagi, sedangkan absen keluar dilakukan setelah jam 17.00 akan diberikan status tidak valid pada sistem.
3. menyediakan fitur pengajuan ketidakhadiran kerja dibagi menjadi 2 yaitu izin sakit dan izin cuti.
4. Semua data yang terekam dari semua fitur diatas dapat ditampilkan menjadi sebuah laporan yang berisi ketidakhadiran dan absensi karyawan.
5. Absen masuk dan keluar menggunakan geo-tagging dari tempat tertentu.
6. Menggunakan Eloquent ORM Laravel dalam melakukan interaksi database.
7. Menu Setting Lembur oleh Admin.
8. Pengajuan Lembur oleh Karyawan.
9. Slip Gaji Karyawan.
