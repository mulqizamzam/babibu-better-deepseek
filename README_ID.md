# Panduan Pemula — Babibu Better DeepSeek

Panduan ini ditujukan untuk pengguna yang baru pertama kali memasang plugin DSH. Tidak perlu mengubah kode sumber untuk mengikuti langkah-langkah di bawah.

## 1. Apa fungsi plugin ini?

**Babibu Better DeepSeek** adalah plugin untuk menghubungkan alur kerja DSH dengan bridge Better DeepSeek. Plugin menyediakan jalur komunikasi untuk memeriksa koneksi, membuat sesi, mengirim prompt, mengambil hasil, menerima event, dan membatalkan sesi.

Plugin ini bukan aplikasi DeepSeek mandiri. Anda perlu memiliki lingkungan DSH yang kompatibel dan layanan bridge yang memang digunakan oleh alur kerja Anda.

## 2. Sebelum mulai

Pastikan Anda sudah memiliki:

- DSH terpasang dan dapat dijalankan.
- Profil DSH bernama `web` (atau profil lain yang memang ingin Anda gunakan).
- Akses ke GitHub untuk mengambil plugin.
- Layanan Better DeepSeek bridge yang kompatibel dan alamat endpoint-nya, bila diperlukan oleh konfigurasi Anda.

> **Catatan:** Versi DSH, konfigurasi bridge, dan ketersediaan endpoint dapat berbeda antarlingkungan. Jika Anda tidak tahu apakah bridge sudah aktif, tanyakan kepada orang yang mengelola instalasi DSH Anda sebelum mengubah konfigurasi.

## 3. Pasang plugin

Buka terminal di lingkungan tempat perintah `dsh` tersedia, lalu jalankan:

```bash
dsh plugin --profile web add github:mulqizamzam/babibu-better-deepseek
```

Perintah ini meminta DSH menambahkan plugin dari repositori GitHub ke profil `web`.

Jika Anda memakai profil lain, ganti `web` dengan nama profil yang benar. Jangan menyalin tanda `$` atau karakter prompt terminal jika ada di contoh lain.

## 4. Jika instalasi berhasil

1. Baca keluaran terminal dan pastikan perintah selesai tanpa error.
2. Ikuti cara yang biasa Anda gunakan untuk menjalankan atau memuat ulang profil DSH.
3. Periksa log saat plugin dimuat. Jika ada error, simpan pesan lengkapnya—terutama baris pertama yang menyebut penyebab.
4. Uji alur kerja di lingkungan yang aman sebelum mengandalkannya untuk pekerjaan penting.

Langkah memuat ulang dan menguji dapat berbeda sesuai cara DSH dijalankan; README ini tidak mengasumsikan adanya perintah restart yang sama di semua instalasi.

## 5. Troubleshooting untuk pemula

### Error `ERR_PNPM_WORKSPACE_PKG_NOT_FOUND`

Jika error menyebut dependensi `workspace:` atau paket workspace yang tidak ditemukan, pastikan Anda mengambil revisi terbaru dari repositori ini dan coba ulangi instalasi. Versi terbaru repositori sudah mengganti referensi dependensi workspace yang tidak tersedia pada instalasi profil terpisah dengan versi paket yang dapat di-resolve dari registry.

### Error terkait build scripts atau `allowBuilds`

Jika pnpm memberi peringatan atau error tentang build scripts yang diblokir, baca instruksi yang dicetak oleh pnpm dan izinkan hanya paket yang memang diperlukan dan Anda percayai. Jangan mengaktifkan semua build scripts secara membabi buta.

### Plugin tidak ditemukan atau gagal diunduh

- Pastikan koneksi internet tersedia.
- Pastikan URL repositori dapat dibuka: https://github.com/mulqizamzam/babibu-better-deepseek
- Coba lagi setelah memastikan nama pemilik dan repositori benar.
- Jika DSH menyimpan entri instalasi gagal, gunakan perintah pengelolaan plugin yang didukung oleh versi DSH Anda untuk memperbaiki atau menghapus entri tersebut sebelum mencoba kembali.

### Plugin terpasang tetapi alur kerja tidak berjalan

- Pastikan layanan bridge yang diperlukan memang sedang berjalan.
- Pastikan konfigurasi endpoint sesuai dengan lingkungan Anda.
- Baca log DSH dan bridge untuk mencari error koneksi atau sesi.
- Jangan menebak endpoint atau token. Gunakan nilai yang diberikan oleh dokumentasi atau administrator lingkungan Anda.

## 6. Apa yang dilakukan endpoint bridge?

Pada tingkat tinggi, plugin ini mendukung operasi berikut:

| Endpoint | Kegunaan |
| --- | --- |
| `/api/better-deepseek/ping` | Memeriksa apakah bridge merespons |
| `/api/better-deepseek/events` | Menerima event melalui SSE |
| `/api/better-deepseek/session.create` | Membuat sesi |
| `/api/better-deepseek/session.prompt` | Mengirim prompt ke sesi |
| `/api/better-deepseek/session.result` | Mengambil hasil sesi |
| `/api/better-deepseek/session.cancel` | Membatalkan sesi |

Endpoint ini adalah gambaran antarmuka bridge, bukan perintah terminal. Jangan mengetikkannya sebagai perintah shell.

## 7. Butuh bantuan?

Saat meminta bantuan, sertakan:

- Sistem operasi dan versi DSH yang digunakan.
- Perintah yang Anda jalankan (hapus rahasia atau token terlebih dahulu).
- Pesan error lengkap dari terminal.
- Apakah error muncul saat instalasi, saat plugin dimuat, atau saat menjalankan alur kerja.

Jangan membagikan API key, cookie sesi, token autentikasi, atau data pribadi dalam log publik.

## Dokumentasi lainnya

- [README utama (Bahasa Inggris)](README.md)
- [Repositori GitHub](https://github.com/mulqizamzam/babibu-better-deepseek)
