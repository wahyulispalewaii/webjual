# Panduan Penggunaan Admin

## Setup pertama

Buka `/admin/setup/`, lalu buat password untuk akun `admin@dibantu.id`. Setup hanya dapat digunakan ketika tabel `admins` masih kosong.

## Dashboard

Dashboard menampilkan jumlah pesanan, pendapatan pembayaran yang sudah diverifikasi, bukti pembayaran yang menunggu pemeriksaan, proyek aktif, dan pesanan selesai.

## Pesanan

Menu **Pesanan** digunakan untuk:

- mencari pesanan berdasarkan kode, invoice, pelanggan, atau WhatsApp;
- membuka brief dan rincian layanan;
- mengubah status proyek;
- menyimpan catatan internal;
- membuka tampilan pelanggan;
- membuka dan mencetak invoice.

Status utama:

```text
awaiting_payment   Menunggu Pembayaran
payment_review     Bukti Sedang Diverifikasi
payment_verified   Pembayaran Diverifikasi
in_progress        Sedang Dikerjakan
awaiting_review    Menunggu Review Pelanggan
revision           Tahap Revisi
completed          Selesai
cancelled          Dibatalkan
```

## Pembayaran

Admin wajib membuka bukti pembayaran sebelum menekan **Verifikasi**. Nominal yang disetujui dapat dikoreksi sesuai bukti. Sistem menghitung total pembayaran terverifikasi dan mengubah invoice menjadi `Dibayar Sebagian` atau `Lunas`.

Jika bukti tidak valid, isi alasan penolakan secara spesifik. Alasan tersebut dapat dilihat pelanggan pada riwayat pembayaran.

## Layanan dan paket

Admin dapat:

- mengaktifkan atau menonaktifkan layanan;
- mengubah nama dan deskripsi;
- mengubah harga paket;
- mengubah label harga seperti `Rp1jt+`;
- mengubah estimasi pengerjaan;
- mengubah fitur paket;
- menambah layanan dan paket baru.

Harga pada invoice lama tidak berubah ketika harga katalog diperbarui.

## Pengaturan

Menu **Pengaturan** memuat identitas bisnis, aturan DP, batas waktu pembayaran, dan QRIS.

QRIS baru tampil pada invoice dan halaman pembayaran setelah:

1. nama merchant diisi;
2. gambar QRIS diunggah;
3. status QRIS aktif.

## Invoice PDF

Buka invoice lalu pilih **Cetak / Simpan PDF**. Pada dialog browser, pilih tujuan `Save as PDF`, ukuran kertas A4, skala 100 persen, dan nonaktifkan header/footer browser agar hasil bersih.
