# Panduan Deployment Cloudflare

## 1. Buat repository GitHub

Unggah seluruh isi folder proyek ini ke repository baru. Folder `functions` harus tetap berada di root repository, bukan di dalam folder `public`.

Struktur penting:

```text
public/
functions/
migrations/
wrangler.jsonc
package.json
```

## 2. Buat database D1

Pada Cloudflare Dashboard:

1. Buka **Storage & Databases**.
2. Pilih **D1 SQL Database**.
3. Buat database bernama `dibantu-id-db`.
4. Buka Console D1 dan jalankan file SQL secara berurutan:
   - `migrations/0001_schema.sql`
   - `migrations/0002_seed.sql`
   - `migrations/0003_indexes_and_triggers.sql`

Alternatif dengan Wrangler:

```bash
npm install
npx wrangler d1 create dibantu-id-db
npx wrangler d1 execute dibantu-id-db --remote --file=./migrations/0001_schema.sql
npx wrangler d1 execute dibantu-id-db --remote --file=./migrations/0002_seed.sql
npx wrangler d1 execute dibantu-id-db --remote --file=./migrations/0003_indexes_and_triggers.sql
```

## 3. Buat bucket R2

1. Buka **Storage & Databases**.
2. Pilih **R2 Object Storage**.
3. Buat bucket bernama `dibantu-id-payment-files`.
4. Bucket tidak perlu dibuat publik.

R2 menyimpan QRIS dan bukti pembayaran. File bukti hanya dibaca melalui endpoint admin yang memeriksa sesi login.

## 4. Buat project Cloudflare Pages

1. Buka **Workers & Pages**.
2. Pilih **Create application** lalu **Pages**.
3. Hubungkan repository GitHub.
4. Konfigurasi build:

```text
Framework preset : None
Build command    : kosong
Build output     : public
Root directory   : /
```

Cloudflare akan membaca folder `functions` secara otomatis ketika deployment berasal dari integrasi Git.

## 5. Tambahkan bindings

Buka project Pages:

```text
Settings > Bindings
```

Tambahkan:

```text
D1 database binding
Variable name : DB
Database      : dibantu-id-db

R2 bucket binding
Variable name : PAYMENT_FILES
Bucket        : dibantu-id-payment-files
```

Tambahkan binding yang sama untuk **Production** dan **Preview** bila deployment preview juga perlu mengakses database.

Setelah bindings ditambahkan, lakukan **Retry deployment** atau push commit baru.

## 6. Uji health endpoint

Buka:

```text
https://NAMA-PROJECT.pages.dev/api/health
```

Respons yang benar:

```json
{
  "ok": true,
  "database": true
}
```

Jika muncul pesan binding D1 belum dikonfigurasi, periksa nama binding harus persis `DB`.

## 7. Buat akun admin pertama

Buka:

```text
https://NAMA-PROJECT.pages.dev/admin/setup/
```

Gunakan:

```text
Nama  : admin
Email : admin@dibantu.id
```

Buat password baru minimal 10 karakter yang memiliki huruf besar, huruf kecil, dan angka. Password tidak disediakan di dalam source code.

Setelah akun pertama dibuat, endpoint setup akan terkunci.

## 8. Unggah QRIS setelah data merchant tersedia

Masuk ke dashboard:

```text
/admin/pengaturan/
```

Lengkapi nama merchant, penyedia QRIS, NMID bila ada, lalu unggah gambar QRIS. Sistem otomatis menyimpan file ke R2 dan mengaktifkan QRIS.

Sebelum langkah ini, aplikasi tetap dapat menerima pesanan tetapi tombol unggah bukti pembayaran dinonaktifkan agar pelanggan tidak menerima instruksi palsu.

## 9. Hubungkan domain dibantu.id

Setelah alamat `pages.dev` berfungsi:

1. Buka **Custom domains** pada project Pages.
2. Tambahkan `dibantu.id`.
3. Ikuti konfigurasi DNS Cloudflare.
4. Pastikan `/api/health`, `/layanan/`, dan `/admin/login/` dapat dibuka dari domain final.

Metadata Open Graph pada landing page sudah mengarah ke `https://dibantu.id`.

## 10. Pengujian wajib sebelum produksi

Lakukan satu transaksi uji:

1. Buka `/layanan/`.
2. Tambahkan paket.
3. Checkout menggunakan data uji.
4. Pastikan kode pesanan, token, dan invoice dibuat.
5. Buka halaman invoice dan uji **Cetak / Simpan PDF**.
6. Setelah QRIS aktif, unggah bukti pembayaran uji.
7. Masuk dashboard dan verifikasi pembayaran.
8. Pastikan status pelanggan berubah.
9. Hapus atau batalkan transaksi uji bila tidak diperlukan.

## Catatan operasional

- Invoice PDF dibuat melalui print dialog browser agar ringan dan kompatibel dengan Cloudflare Pages.
- Status invoice kedaluwarsa dihitung ketika data pesanan dibuka. Tidak ada cron wajib untuk MVP.
- Harga pada invoice lama tidak berubah saat admin mengubah harga katalog.
- Bukti pembayaran maksimal 5 MB dan hanya menerima JPG, PNG, WebP, atau PDF.
- Aset QRIS maksimal 4 MB dan hanya menerima JPG, PNG, atau WebP.
