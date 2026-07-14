# Laporan Pengujian Lokal

Pengujian dilakukan dengan Wrangler Pages Dev, D1 lokal, dan R2 lokal pada 14 Juli 2026.

## Pengujian yang berhasil

- Kompilasi Pages Functions.
- Pembacaan `public/_headers` dan `public/_redirects`.
- Health check D1 melalui `/api/health`.
- Pengambilan lima layanan dan lima belas paket dari `/api/services`.
- Pembuatan pesanan DP 50 persen.
- Pembuatan kode pesanan dan nomor invoice otomatis.
- Pengambilan detail pesanan melalui token pelacakan.
- Setup akun admin pertama.
- Pemeriksaan sesi admin.
- Pembacaan KPI dashboard.
- Upload QRIS ke R2 lokal.
- Pembacaan QRIS melalui endpoint media.
- Upload bukti pembayaran ke R2 lokal.
- Daftar pembayaran pending pada dashboard admin.
- Verifikasi pembayaran DP.
- Perubahan invoice menjadi `partially_paid`.
- Perubahan status pesanan menjadi `payment_verified`.
- Perhitungan sisa pembayaran setelah DP.
- Pemeriksaan sintaks seluruh file JavaScript.
- Pemeriksaan seluruh referensi aset lokal pada halaman HTML.
- Penerapan semua migration SQL pada SQLite lokal.

## Pengujian produksi yang masih diperlukan

- Binding D1 dan R2 pada project Cloudflare Pages milik pengguna.
- Custom domain `dibantu.id`.
- QRIS merchant asli.
- Pengujian scan QRIS asli dari invoice cetak.
- Pengujian email dan WhatsApp pada perangkat nyata.
