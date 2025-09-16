# PROJEK: SISTEM MANAJEMEN ABSENSI KARYAWAN  
*(Laravel-based Employee Attendance System – LEAS)*

---

## LATAR BELAKANG  
Presensi karyawan masih manual (kertas, sidik jari terpisah, Google Form) sehingga:  
- Data mudah hilang / tertimpa  
- Bisa "titip tanda tangan" (absen-bolos)  
- HRD lama rekap gaji & lembur  
- Tidak ada bukti foto saat check-in/out  
- Susah pantau karyawan remote / site-project  

Kami bangun sistem digital berbasis Laravel agar absensi lebih **cepat, akurat & transparan**.

---

## TUJUAN UTAMA PROYEK  
1. Absensi harian ≤ 5 detik  
2. Otomatis hitung keterlambatan & lembur  
3. Notifikasi real-time jika karyawan terlambat  
4. Simpan bukti foto + lokasi GPS  
5. Laporan presensi & rekap gaji dalam 1 klik  

---

## FUNGSI UTAMA (FITUR)  
- **Multi-role login** – karyawan, HRD, manajer  
- **Master data** – CRUD karyawan, departemen, shift, libur nasional  
- **Absensi digital** – scan QR / tombol, selfie, validasi radius 100 m  
- **Pengajuan cuti & lembur** – online, approval via e-mail/WA  
- **Dashboard live** – monitor hadir, terlambat, alpha  
- **Perhitungan otomatis** – jam kerja, telat (menit), lembur (jam)  
- **Notifikasi** – e-mail & WhatsApp (Wablas)  
- **Export laporan** – PDF slip gaji, Excel rekap, grafik Chart.js  
- **API mobile** – endpoint check-in/out untuk Android/iOS  

---

## MANFAAT  
- HRD hemat 70 % waktu rekap  
- Manajemen pantau kinerja real-time  
- Adil & aman (foto + GPS)  
- Payroll cepat, data aman & bisa jadi bukti hukum  

---

## ALUR KERJA SISTEM  
1. Admin input data karyawan & jadwal shift  
2. Karyawan scan QR → selfie → validasi lokasi & waktu  
3. Simpan record absensi & hitung jam kerja  
4. HRD pantau dashboard & terima notifikasi  
5. Akhir bulan klik "Export Rekap" → PDF & Excel otomatis jadi
