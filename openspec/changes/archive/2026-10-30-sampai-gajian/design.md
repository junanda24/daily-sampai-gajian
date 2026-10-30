# Design: Sampai Gajian!

## Stack
Web artifact static (HTML/CSS/JS client-side, satu halaman). Tanpa backend,
tanpa build step, tanpa dependensi eksternal yang menyimpan data.
Format mata uang memakai `Intl.NumberFormat('id-ID', { currency: 'IDR' })`.

## Struktur (single-file section discipline, sesuai ARCHITECTURE.md)
Satu halaman dengan seksi berurutan, masing-masing < 300 baris logika:
1. Hero + penjelasan satu kalimat.
2. Form input dasar (sisa uang, tanggal gajian).
3. Daftar pengeluaran wajib (tambah via chip cepat + form bebas, saklar tunda).
4. Struk hasil (animasi muncul, strip hari, status).
5. Simulasi jajan per hari.
6. Jurus hemat (checkbox + nominal yang bisa diubah).
7. Catatan privasi + disclaimer + tombol contoh/reset.

## State (lima keranjang, sesuai ARCHITECTURE.md)
- Input pengguna (sisa uang, tanggal gajian, daftar wajib, rencana jajan,
  jurus aktif): state lokal halaman, sesi browser saja.
- Hasil turunan (uang bebas, hari tersisa, jatah, status, proyeksi):
  dihitung murni dari input — tidak disimpan terpisah.
- Tidak ada server state, tidak ada cache, tidak ada state global.

## Visual (mode Operate, local-impeccable)
- Mobile-first satu kolom, kartu "struk" sebagai signature visual:
  latar kertas krem, tinta hijau tua, aksen amber, tepi struk bergerigi.
- Tipografi tebal dan besar untuk angka jatah harian — angka itu
  pahlawannya, bukan dekorasi.
- Status memakai warna + kata, bukan warna saja (aksesibilitas).
- Delight: struk "tercetak" (animasi slide/fade dari atas), strip hari
  berupa titik-titik jalan ke gajian, kalimat semangat yang berubah
  per status.
- Tanpa gradasi ungu-biru generik, tanpa emoji di label UI.
- Copy Bahasa Indonesia natural, nada ringan dan empatik.

## Aturan perhitungan (dinyatakan di app)
- Hari tersisa = selisih hari kalender (tanggal gajian − hari ini).
- Jatah harian dibulatkan ke bawah ke rupiah utuh.
- Ambang status: Defisit < 0; Ketat < 25.000; Pas-pasan 25.000–49.999;
  Aman >= 50.000 per hari. Dinyatakan sebagai patokan sederhana.
