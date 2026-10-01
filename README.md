# Pure Laundry

Aplikasi web sistem akuntansi laundry dengan empat entitas: pelanggan, layanan, transaksi, dan pembayaran.

## Dokumentasi

- [Dokumentasi skema database dan ERD](docs/skema-erd-sistem-akuntansi-laundry.md)

## Menjalankan

- Buka `frontend/index.html` langsung di browser. Tanpa konfigurasi Supabase, aplikasi berjalan dengan data contoh yang tersimpan di browser.
- Untuk mode web server opsional, jalankan `node backend/app.js`, lalu buka `http://localhost:3000`. Tidak ada dependensi npm.
- Untuk menyambungkan database, jalankan `database/schema.sql` di Supabase SQL Editor. Di aplikasi, buka ikon pengaturan lalu isi Project URL dan publishable key.

Mode browser langsung dan server lokal sama-sama mengakses Supabase dari frontend. File `backend/app.js` hanya menyajikan frontend dan menyediakan `GET /api/health`; ia tidak menyimpan kredensial database.

**Keamanan:** skema awal mengizinkan akses CRUD anon agar demo dapat digunakan langsung dengan publishable key. Batasi tabel memakai autentikasi dan policy RLS khusus sebelum memasukkan data laundry sungguhan. Jangan pernah memasukkan service role key ke frontend.

## Mengunggah ke GitHub

Pastikan **Git for Windows** sudah terpasang. Buat repository kosong di GitHub, lalu buka terminal pada folder proyek dan ganti URL remote dengan URL repository Anda:

```powershell
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/USERNAME/NAMA-REPOSITORY.git
git push -u origin main
```

Jika repository lokal sudah memiliki remote `origin`, gunakan `git remote set-url origin https://github.com/USERNAME/NAMA-REPOSITORY.git` sebagai pengganti perintah `git remote add`. File `.gitignore` di folder ini mengecualikan file environment lokal, dependensi, hasil build, dan file sistem operasi dari commit.

## Menerbitkan ke GitHub Pages

Workflow [`.github/workflows/deploy-pages.yml`](.github/workflows/deploy-pages.yml) menerbitkan isi folder `frontend/` sebagai akar situs setiap kali ada push ke branch `main` atau `master`. Dengan begitu, `index.html`, `app.js`, dan `styles.css` berada pada lokasi yang sama dan dapat dimuat dengan path relatif. Jika Pages masih memakai mode branch/root, `index.html` di root repository akan mengarahkan ke `frontend/index.html`.

1. Di repository GitHub, buka **Settings → Pages**.
2. Pada **Build and deployment → Source**, pilih **GitHub Actions**.
3. Push workflow ini ke branch `main` atau `master`, lalu buka tab **Actions** dan tunggu workflow **Deploy Pure Laundry to GitHub Pages** selesai dengan status berhasil.
4. Buka URL Pages yang ditampilkan pada job deployment. Jika masih 404, pastikan workflow berhasil dan URL menggunakan nama owner serta nama repository yang tepat.

GitHub Pages hanya menerbitkan frontend statis. Isi Project URL dan publishable key Supabase melalui pengaturan aplikasi setelah situs berhasil dibuka.
