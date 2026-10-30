# Sampai Gajian!

**Sisa uangmu dibagi hari, bukan dibagi nafsu.**

Web app frontend-only yang menjawab pertanyaan tanggal tua paling nyata:
"Sisa uangku ini cukup nggak sampai gajian — dan berapa jatahku per hari
supaya cukup?" Masukkan sisa uang sekarang dan tanggal gajian berikutnya,
kurangi pengeluaran wajib yang belum dibayar, dan dapatkan satu angka yang
langsung bisa dipakai hari ini: **jatah harianmu**.

## Kenapa ide ini dipilih

Kebanyakan kalkulator keuangan bertanya "berapa pengeluaranmu bulan ini?" —
pertanyaan yang butuh rekap sebulan dan terasa berat. Sampai Gajian!
membalik sudutnya: mulai dari dua angka yang sudah ada di kepala (sisa uang,
tanggal gajian), lalu bagi sisanya per hari. Efek kejutnya ada di
pembalikan itu, plus dua fitur yang mengubah rasa bersalah menjadi angka
konkret:

- Saklar **"bisa ditunda"** di tiap pengeluaran wajib: saat hasil defisit,
  pengguna tidak cuma diberi kabar buruk — mereka bisa menggeser item yang
  bisa ditunda dan melihat angkanya membaik seketika.
- Simulasi **"kalau aku jajan Rp X/hari, uangku habis tanggal berapa?"** —
  jajan berubah dari rasa bersalah abstrak menjadi tanggal konkret.

## Fitur

- Input sisa uang sekarang (Rp) dan tanggal gajian berikutnya, dengan
  validasi: tanggal lewat ditolak dengan pesan jelas, tanggal = hari ini
  menampilkan status khusus "Gajian hari ini".
- Daftar pengeluaran wajib: tambah/hapus baris bebas, chip cepat tambah
  (Kos/Kontrakan, Listrik, Air, Internet/HP, Cicilan, Transport), dan
  saklar "bisa ditunda" per baris (item tertunda dikeluarkan dari hitungan
  dan ditotal terpisah).
- Struk hasil: sisa uang, total wajib, uang bebas, hari tersisa,
  jatah harian, dan status Defisit / Ketat / Pas-pasan / Aman.
- Strip hari: satu titik per hari tersisa, visual "jalan ke gajian".
- Simulasi jajan harian: proyeksi sisa uang di hari gajian (bila jajan
  masih dalam jatah) atau tanggal proyeksi uang habis (bila jajan melebihi
  jatah).
- Jurus hemat: minimal 3 jurus yang bisa dicentang, masing-masing dengan
  nominal hemat per hari yang BISA DIUBAH; jatah efektif ditampilkan
  berdampingan dengan jatah dasar.
- Tombol "Coba contoh" (mengisi data contoh yang masuk akal) dan reset.
- Momen delight: struk hasil muncul dengan animasi seperti tercetak, dan
  kalimat semangat yang berubah sesuai status — empatik, tidak menghakimi.
- Privasi: semua hitungan terjadi di browser; tidak ada data yang dikirim
  atau disimpan permanen. Tanpa backend, tanpa login.

## Cara pakai

1. Buka link hasil di bawah.
2. Isi sisa uangmu sekarang dan tanggal gajian berikutnya.
3. Tambahkan pengeluaran wajib yang belum dibayar (centang "bisa ditunda"
   untuk yang masih bisa digeser).
4. Baca jatah harianmu di struk hasil. Coba simulasi jajan dan jurus hemat
   untuk melihat bagaimana angkanya berubah.

## Cara menjalankan dari source

Project ini adalah web app static (HTML/CSS/JS client-side, hasil export
artifact). Tidak ada build step dan tidak ada server:

```bash
# dari folder src/ (atau buka file HTML hasil export langsung)
python3 -m http.server 8000
# lalu buka http://localhost:8000 di browser
```

Atau cukup buka file HTML di `src/` langsung di browser — semua hitungan
berjalan client-side.

## Tech stack

- HTML/CSS/JavaScript client-side (web artifact static)
- `Intl.NumberFormat('id-ID', { currency: 'IDR' })` untuk format rupiah
- Tanpa backend, tanpa database, tanpa dependensi yang menyimpan data

## Struktur folder

```
2026-10-30-sampai-gajian/
├── README.md
├── src/                          # hasil export artifact (halaman web utuh)
└── openspec/changes/archive/2026-10-30-sampai-gajian/
    ├── proposal.md
    ├── specs/sampai-gajian/spec.md
    ├── design.md
    └── tasks.md
```

## Link hasil

- Web app: artifact slug `sampai-gajian` (card widget:
  web-artifact-build-completed-fcfc052a-9cc2-4510-af32-19a1a09767c5)
- Repo: https://github.com/junanda24/daily-sampai-gajian
- Tanggal rilis: 2026-10-30

## Aturan perhitungan (dinyatakan juga di dalam app)

- Hari tersisa = selisih hari kalender (tanggal gajian − hari ini).
- Uang bebas = sisa uang − total pengeluaran wajib yang harus dibayar
  sebelum gajian (item "bisa ditunda" tidak dihitung).
- Jatah harian = floor(uang bebas / hari tersisa), dibulatkan ke bawah
  ke rupiah utuh.
- Ambang status (patokan sederhana, bukan standar resmi):
  Defisit bila uang bebas < 0; Ketat bila jatah < Rp 25.000;
  Pas-pasan Rp 25.000–49.999; Aman >= Rp 50.000 per hari.
- Proyeksi uang habis = hari ini + floor(uang bebas / rencana jajan) hari.

## Catatan / temuan saat build

- Sengaja TIDAK dibuat: penyimpanan permanen (localStorage/database).
  Alasan: app static dan privasi — orang memasukkan angka keuangan
  pribadinya, jadi input hanya hidup selama sesi browser.
- Sengaja TIDAK dibuat: backend atau sinkronisasi antar perangkat, karena
  seluruh perhitungan deterministik dan seketika di browser.
- Nominal default jurus hemat adalah perkiraan awal yang bisa diubah
  pengguna, bukan data survei — hal ini dinyatakan di dalam app.
- Ini panduan kasar, bukan nasihat keuangan.
