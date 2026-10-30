# Spec: Sampai Gajian!

## Requirements

### R1 — Input dasar
- SHALL menerima: sisa uang sekarang (Rp, >= 0), tanggal gajian berikutnya.
- WHEN tanggal gajian sudah lewat THEN tampilkan error yang jelas
  ("tanggal sudah lewat — pilih tanggal gajian berikutnya") dan JANGAN
  tampilkan hasil.
- WHEN tanggal gajian = hari ini THEN tampilkan status khusus
  ("Gajian hari ini") tanpa pembagian per hari.
- WHEN input kosong/tidak valid THEN tombol hitung tidak menghasilkan
  angka palsu; tampilkan pesan validasi di field yang bermasalah.

### R2 — Pengeluaran wajib
- SHALL memungkinkan tambah/hapus baris pengeluaran wajib
  (nama + nominal Rp >= 0).
- SHALL menyediakan chip cepat tambah: Kos/Kontrakan, Listrik, Air,
  Internet/HP, Cicilan, Transport.
- SHALL setiap baris punya saklar "bisa ditunda": item yang ditunda
  DIKELUARKAN dari perhitungan uang bebas dan ditampilkan terpisah
  sebagai total tertunda.
- SHALL menampilkan total wajib yang harus dibayar sebelum gajian.

### R3 — Hasil inti
- SHALL menghitung: hari tersisa = selisih hari kalender dari hari ini
  ke tanggal gajian; uang bebas = sisa uang − total wajib;
  jatah harian = floor(uang bebas / hari tersisa) bila hari tersisa > 0.
- SHALL menampilkan status: Defisit (uang bebas < 0), Ketat
  (jatah < Rp 25.000), Pas-pasan (Rp 25.000–49.999), Aman (>= Rp 50.000),
  dengan label bahwa ambang ini patokan sederhana.
- SHALL menampilkan hasil sebagai "struk" ringkas: sisa uang, total wajib,
  uang bebas, hari tersisa, jatah harian.
- SHALL menampilkan strip hari tersisa (satu titik per hari) sebagai
  visual "jalan ke gajian".

### R4 — Simulasi jajan
- SHALL menerima rencana jajan per hari (Rp >= 0).
- WHEN rencana jajan <= jatah harian THEN tampilkan proyeksi sisa uang
  di hari gajian (uang bebas − rencana × hari tersisa) dan pesan aman.
- WHEN rencana jajan > jatah harian THEN tampilkan tanggal proyeksi uang
  habis (hari ini + floor(uang bebas / rencana jajan) hari) dan pesan
  peringatan yang tidak menghakimi.
- WHEN uang bebas <= 0 THEN simulasi tidak menampilkan tanggal palsu;
  tampilkan pesan defisit.

### R5 — Jurus hemat
- SHALL menyediakan minimal 3 jurus hemat yang bisa dicentang, masing-masing
  dengan nominal hemat per hari yang BISA DIUBAH pengguna.
- WHEN jurus dicentang THEN jatah harian efektif = jatah harian + total
  hemat per hari dari jurus yang aktif, dan ditampilkan berdampingan
  dengan jatah dasar.
- SHALL nilai default jurus dinyatakan sebagai perkiraan yang bisa diubah,
  bukan data survei.

### R6 — Contoh & reset
- SHALL tombol "Coba contoh" mengisi data contoh yang masuk akal
  (sisa uang, tanggal gajian = hari ini + 12 hari, 2–3 pengeluaran wajib).
- SHALL tombol reset mengosongkan semua input dan menyembunyikan hasil.

### R7 — Delight, mobile, privasi
- SHALL ada momen delight: struk hasil muncul dengan animasi, dan satu
  kalimat semangat yang berubah sesuai status (empatik, tidak menghakimi).
- SHALL layout mobile-first, satu kolom, semua kontrol bisa dipakai
  dengan jempol; tidak ada tombol mati.
- SHALL ada catatan privasi: semua hitungan di browser, tidak ada data
  yang dikirim/disimpan permanen; dan disclaimer "panduan kasar, bukan
  nasihat keuangan".
- SHALL tidak ada lorem ipsum, placeholder palsu, atau fungsi mati.
- SHALL tidak ada backend, login, atau API key.
