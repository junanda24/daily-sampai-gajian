# Proposal: Sampai Gajian!

## Apa & kenapa

**Sampai Gajian!** adalah web app frontend-only yang menjawab satu pertanyaan
tanggal tua yang hampir semua orang Indonesia pernah rasakan: "Sisa uangku
ini cukup nggak sampai gajian — dan berapa jatahku per hari supaya cukup?"

Kebanyakan kalkulator keuangan bertanya "berapa pengeluaranmu bulan ini?"
— pertanyaan yang butuh rekap sebulan dan terasa berat. Aplikasi ini membalik
sudutnya: mulai dari DUA angka yang sudah ada di kepala (sisa uang sekarang,
tanggal gajian berikutnya), kurangi pengeluaran wajib yang belum dibayar,
lalu bagi sisanya per hari. Hasilnya satu angka yang langsung bisa dipakai
hari ini: **jatah harianmu**.

## Kenapa ini mengejutkan

- Sudut pandang terbalik: bukan budgeting sebulan, tapi *survival budgeting*
  dari sekarang sampai satu tanggal pasti. Angkanya kecil, konkret, dan
  langsung bisa dipegang ("Rp 38.000/hari"), bukan abstrak.
- Pengeluaran wajib punya saklar "bisa ditunda": saat hasil defisit, pengguna
  tidak cuma diberi kabar buruk — mereka bisa menggeser item yang bisa
  ditunda dan melihat angkanya membaik seketika.
- Simulasi "kalau aku jajan Rp X/hari, uangku habis tanggal berapa?" mengubah
  jajan dari rasa bersalah abstrak menjadi tanggal konkret.
- Jurus hemat yang bisa dicentang menambah jatah harian secara transparan
  (nominal per hari bisa diubah), bukan sekadar tips generik.

## Kenapa bentuk ini

Web app static, frontend-only, tanpa login/database. Semua hitungan terjadi
di browser; tidak ada data keuangan yang dikirim ke mana pun. Ini penting:
orang tidak akan memasukkan sisa uangnya ke layanan yang menyimpan data.
Tidak ada backend karena tidak ada logika yang butuh server — seluruh
perhitungan deterministik dan seketika.

## Untuk siapa

Karyawan/gajian bulanan, freelancer yang menunggu pembayaran berikutnya,
anak kos, dan siapa pun yang pernah menghitung hari sampai gajian.
Bahasa Indonesia natural, nada empatik dan ringan — tidak menghakimi,
tidak sok menasihati soal keuangan.

## Batasan jujur

- Ini panduan kasar, bukan nasihat keuangan. Ambang status
  (Aman/Pas-pasan/Ketat/Defisit) adalah patokan sederhana yang dinyatakan
  di dalam app, bukan standar resmi.
- Nominal jurus hemat adalah perkiraan awal yang bisa diubah pengguna,
  bukan data survei.
- App static: input hanya hidup selama sesi browser, tidak tersimpan
  permanen.
