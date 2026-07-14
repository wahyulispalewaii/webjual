# dibantu.id Sales App

Aplikasi penjualan jasa full-stack untuk Cloudflare Pages. Frontend mempertahankan dasar UI website dibantu.id. Backend menggunakan Pages Functions, database Cloudflare D1, dan penyimpanan bukti pembayaran serta QRIS menggunakan Cloudflare R2.

## Fitur MVP

- Landing page lama tetap dipertahankan dan dihubungkan ke katalog pemesanan.
- Katalog jasa dan paket dinamis dari D1.
- Keranjang lokal dan checkout tanpa akun pelanggan.
- Brief proyek, kode pesanan, token pelacakan, dan invoice otomatis.
- Pembayaran lunas atau DP 50 persen.
- Batas pembayaran awal 60 menit.
- QRIS statis yang dapat diunggah admin kemudian.
- Upload bukti pembayaran ke R2.
- Verifikasi manual pembayaran.
- Pelacakan status proyek oleh pelanggan.
- Invoice A4 yang dapat dicetak atau disimpan sebagai PDF dari browser.
- Dashboard admin untuk pesanan, pembayaran, layanan, harga, dan pengaturan.
- Setup admin pertama tanpa password bawaan di source code.

## Stack

- Cloudflare Pages
- Cloudflare Pages Functions
- Cloudflare D1
- Cloudflare R2
- HTML, CSS, dan JavaScript tanpa framework frontend
- Web Crypto API untuk PBKDF2 password hashing

## Data bisnis awal

- Bisnis: dibantu.id
- Pemilik: Wahyulis Hersya
- Alamat: Marioriwawo, Soppeng, Sulawesi Selatan
- WhatsApp: 6287858468082
- Email: wahyulishersyaa@gmail.com
- Model pembayaran: lunas dan DP
- DP: 50 persen
- Batas pembayaran: 60 menit
- Email admin awal: admin@dibantu.id
- QRIS: belum diaktifkan sampai admin mengunggah aset dan data merchant

Baca `PANDUAN_DEPLOYMENT.md` untuk proses instalasi lengkap.
