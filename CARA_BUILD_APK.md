# Cara Membangun APK — Gittry Browser

Saya tidak bisa mengompilasi file .apk langsung di lingkungan ini (tidak ada Android SDK/Gradle terpasang), tapi project ini **siap build**. Pilih salah satu cara di bawah.

## Fitur yang sudah dibuat
- Tanpa kolom alamat/URL — aplikasi otomatis membuka `https://gittry.github.io/open/login.html`
- Tautan di dalam situs tetap terbuka di dalam aplikasi (perilaku browser normal)
- Izin lengkap ala Chrome: JavaScript, cookie, DOM storage, geolocation, kamera/mikrofon untuk upload file, unduh file ke folder Download
- Tombol **Back** di kiri toolbar
- Tombol **ubah tampilan Mobile ↔ Desktop** di kanan toolbar (ikon + label teks), mengganti User-Agent lalu reload halaman
- Pull-to-refresh

## Opsi 1 — Android Studio (paling mudah, gratis)
1. Download & install [Android Studio](https://developer.android.com/studio)
2. File → Open → pilih folder `GittryBrowser`
3. Tunggu Gradle sync selesai (otomatis download dependency)
4. Build → Build Bundle(s)/APK(s) → Build APK(s)
5. APK hasil ada di `app/build/outputs/apk/debug/app-debug.apk`
6. Untuk versi rilis (siap dibagikan), gunakan Build → Generate Signed Bundle/APK dan buat keystore sendiri

## Opsi 2 — Build via terminal (butuh Android SDK + Gradle terpasang)
```bash
cd GittryBrowser
./gradlew assembleDebug
```
Hasil APK ada di `app/build/outputs/apk/debug/app-debug.apk`

## Opsi 3 — Build APK gratis lewat HP saja (via GitHub Actions)
Project ini sudah dilengkapi file workflow di `.github/workflows/build-apk.yml`, jadi tinggal upload ke GitHub:

1. Ekstrak file zip ini di HP (pakai app "Files" / ZArchiver / dsb.)
2. Install app **GitHub** (resmi) dari Play Store, login/daftar akun (gratis)
3. Di app GitHub, buat repository baru (misal nama `GittryBrowser`), set **Public** atau **Private** (bebas)
4. Upload semua isi folder `GittryBrowser` ke repo tersebut (app GitHub mendukung upload file; kalau app GitHub official kurang leluasa untuk upload banyak file sekaligus, alternatif: buka **github.com** lewat browser HP → buka repo → "Add file" → "Upload files" → pilih semua file/folder hasil ekstrak, lalu commit)
5. Buka tab **Actions** di repo tersebut → workflow "Build APK" akan otomatis berjalan (atau klik "Run workflow" kalau belum jalan)
6. Tunggu sampai selesai (centang hijau, sekitar 2-5 menit)
7. Buka hasil run tersebut → scroll ke bagian **Artifacts** → download **GittryBrowser-apk** (berupa zip berisi `app-debug.apk`)
8. Ekstrak zip itu di HP, lalu install `app-debug.apk` seperti biasa (aktifkan "Izinkan sumber tidak dikenal" jika diminta)

Semua langkah di atas gratis dan hanya butuh browser/app GitHub di HP — tidak perlu laptop maupun install Android Studio.

## Catatan penting
- Karena `usesCleartextTraffic="true"` dan izin lengkap disertakan, Play Store mungkin meminta justifikasi izin (kamera/lokasi) jika nanti dipublikasikan — wajar untuk aplikasi browser.
- Ganti `applicationId` di `app/build.gradle` jika ingin nama paket sendiri.
- Icon aplikasi saat ini masih ikon generik (bentuk monitor) — silakan ganti file di `app/src/main/res/mipmap-anydpi-v26/` dengan logo Anda sendiri.
