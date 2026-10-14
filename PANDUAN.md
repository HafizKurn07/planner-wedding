# Panduan Pasang Planner Pernikahan Kita (Firebase + GitHub Pages)

Hasil akhir: satu alamat web yang dibuka di HP masing-masing. Data tersinkron antara kamu dan pasangan, dan hanya dua akun kalian yang bisa mengaksesnya. Semua langkah memakai paket gratis. Perkiraan waktu: 20-30 menit.

## A. Siapkan Firebase

1. Buka https://console.firebase.google.com lalu login dengan akun Google. Klik **Create a project**, beri nama (misal planner-nikah). Google Analytics boleh dimatikan.
2. Menu **Build > Firestore Database > Create database**. Pilih mode **Production**. Untuk lokasi pilih yang terdekat (misal asia-southeast2 Jakarta).
3. Menu **Build > Authentication > Get started > Sign-in method**. Aktifkan **Email/Password** (jangan aktifkan "Email link"), lalu Save.
4. Masih di Authentication, tab **Users > Add user**. Buat dua akun (email + kata sandi): satu untukmu, satu untuk pasangan. Setelah dibuat, salin kolom **User UID** masing-masing akun.
5. Di Authentication > **Settings > User actions**, matikan **Enable create (sign-up)** bila opsinya ada, supaya tidak ada orang lain bisa mendaftar.
6. Menu **Firestore Database > Rules**. Hapus isi lama, tempel isi file `firestore.rules`, ganti `UID_PASANGAN_1` dan `UID_PASANGAN_2` dengan dua UID tadi, lalu **Publish**.
7. Klik ikon roda gigi > **Project settings > General**. Di bagian **Your apps**, klik ikon web `</>`, beri nama bebas, lalu daftarkan. Salin isi `firebaseConfig`.
8. Buka file `firebase-config.js`, ganti nilai ISI_... dengan nilai dari langkah 7 (apiKey, authDomain, projectId, appId).

Catatan: apiKey Firebase untuk web memang tampil di file publik dan itu normal. Yang menjaga data adalah login dan aturan Firestore pada langkah 4-6.

## B. Unggah ke GitHub Pages

1. Buka https://github.com lalu **New repository**. Nama misal planner-nikah, pilih **Public**, Create.
2. Klik **uploading an existing file** (atau Add file > Upload files). Unggah semua file dari folder ini: index.html, firebase-config.js, manifest.webmanifest, sw.js, tiga file ikon .png. Klik **Commit changes**. (firestore.rules dan PANDUAN.md tidak perlu diunggah.)
3. Buka **Settings > Pages**. Pada Source pilih **Deploy from a branch**, Branch **main**, folder **/(root)**, lalu Save.
4. Tunggu 1-2 menit. Alamat aplikasi: https://NAMA-GITHUB-KAMU.github.io/planner-nikah/

## C. Pakai di HP

1. Buka alamat tadi, lalu login dengan email dan kata sandi dari langkah A4.
2. **iPhone (Safari):** tombol Bagikan > **Tambah ke Layar Utama**.
   **Android (Chrome):** menu titik tiga > **Instal aplikasi** atau **Tambahkan ke layar utama**.
3. Pasangan melakukan hal yang sama dengan akunnya sendiri. Data yang diisi satu orang akan muncul di HP yang lain.

## D. Catatan

- Saat pertama login, aplikasi berisi data contoh. Tekan **Mulai dari nol** di Beranda untuk mengosongkannya.
- Kalau sudah punya data di versi Claude, unduh cadangan di sana (Lainnya > Profil > Unduh cadangan), lalu di sini pakai **Pulihkan cadangan**.
- Kalau muncul "Akun ini belum diizinkan", periksa lagi UID di aturan Firestore (langkah A6).
- Kalau mengubah file lalu muncul tampilan lama, tutup aplikasi sepenuhnya dan buka lagi.
- Paket gratis Firebase (Spark) jauh melebihi kebutuhan aplikasi ini.
