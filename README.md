# Tugas Praktikum Mobile Pertemuan 7

Nama : Muhammad Sultan Alhakim

NIM : H1D022105

Shift Baru : A

Berikut adalah penjelasan lengkap dari cara kerja sistem login berbasis Ionic dan Angular yang Anda lampirkan:

1. Komponen Login

   Dalam login.page.ts, terdapat fungsi login() yang memvalidasi input username dan password. Jika tidak kosong, data akan dikirim ke authService menggunakan metode postMethod, yang mengarahkannya ke login.php. Tanggapan dari server (dalam res.status_login) memeriksa status login. Jika berhasil, token
dan username disimpan menggunakan saveData(), dan pengguna diarahkan ke halaman /home. Jika gagal, notifikasi akan muncul dengan pesan kesalahan.

3. Layanan Otentikasi (authentication.service.ts)

   Layanan ini mengelola autentikasi dan status pengguna dengan menggunakan isAuthenticated, yang berbasis BehaviorSubject. Ini mengontrol status login dalam aplikasi. Metode saveData menyimpan token dan username di Capacitor Preferences, yang memastikan pengguna tetap login hingga mereka memilih untuk keluar. Metode loadData() akan memuat token dan nama pengguna saat aplikasi dibuka, memungkinkan kontrol status login yang baik dan mulus.

5. Guard dan Rute (app-routing.module.ts, auth.guard.ts, auto-login.guard.ts)

   authGuard dan autoLoginGuard mencegah akses ke halaman tertentu tergantung pada status autentikasi pengguna. authGuard memblokir akses ke halaman /home bagi pengguna yang belum login, sedangkan autoLoginGuard mengalihkan pengguna yang telah login ke halaman /home meskipun mereka mencoba mengakses halaman login.

7. Notifikasi Kesalahan dan Logout

   Jika terdapat masalah dengan koneksi internet atau kredensial yang salah, pesan notifikasi akan muncul untuk memandu pengguna. Metode logout() akan menghapus token, nama, dan status autentikasi, mengembalikan pengguna ke status belum login, sehingga meningkatkan keamanan aplikasi.

9. Backend PHP (login.php, koneksi.php)

    Script PHP ini bertanggung jawab untuk menerima data username dan password, melakukan hashing pada password, dan membandingkannya dengan data di database (user table). Jika kredensial cocok, server mengembalikan token yang berbasis waktu sebagai tanda autentikasi berhasil, dikirim bersama status_login sebagai "berhasil." Sebaliknya, jika tidak cocok, status "gagal" dikembalikan tanpa token, memberi tahu pengguna bahwa login mereka tidak berhasil.

Sistem ini menggabungkan validasi frontend, autentikasi backend, dan pengelolaan sesi pengguna, memungkinkan pengalaman login yang aman, terstruktur, dan responsif.
