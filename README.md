# Peringkas Cerdas

![image](https://github.com/user-attachments/assets/d1c4d4c2-5af2-40be-ba12-75d39739762f)

"Peringkas Cerdas" adalah aplikasi web sederhana yang memungkinkan pengguna meringkas teks panjang menjadi poin-poin ringkasan yang padat dan mudah dicerna. Aplikasi ini dirancang untuk membantu pengguna memahami inti dari suatu dokumen atau artikel dengan cepat, didukung oleh kemampuan kecerdasan buatan dari Google Gemini API.

## Fitur Utama

*   **Input Teks Fleksibel**: Pengguna dapat mengetik atau menempelkan teks ke dalam area input yang disediakan.
*   **Penghitung Karakter**: Menampilkan jumlah karakter saat ini dan batas maksimum yang diizinkan (10.000 karakter).
*   **Ringkasan Bertenaga AI**: Menggunakan Google Gemini API untuk menghasilkan ringkasan dalam format bullet-point (3-5 poin).
*   **Tombol Aksi**:
    *   **Ringkas Sekarang**: Memicu proses peringkasan teks.
    *   **Hapus Teks**: Membersihkan area input dan hasil ringkasan.
    *   **Coba Contoh**: Memuat contoh teks untuk demonstrasi cepat.
*   **Indikator Pemuatan**: Menampilkan animasi loading dan pesan saat proses peringkasan sedang berlangsung.
*   **Pembatalan Permintaan**: Pengguna dapat membatalkan permintaan peringkasan yang sedang berjalan.
*   **Penanganan Kesalahan Granular**: Memberikan pesan kesalahan yang spesifik untuk berbagai skenario (misalnya, kunci API tidak valid, teks kosong, terlalu banyak permintaan, dll.).
*   **Manajemen Kunci API Lokal**: Kunci API Gemini disimpan secara lokal di browser pengguna (menggunakan `localStorage`) untuk kenyamanan dan keamanan.
*   **Fungsionalitas Salin**: Tombol untuk menyalin hasil ringkasan sebagai teks biasa atau dalam format Markdown.
*   **Desain Responsif & Modern**: Antarmuka pengguna yang menarik dengan tema gelap, efek glassmorphism, dan animasi latar belakang yang dapat diaktifkan/dinonaktifkan.
*   **Aksesibilitas**: Menggunakan atribut ARIA untuk meningkatkan aksesibilitas bagi pembaca layar.

## Teknologi yang Digunakan

*   **HTML5**: Struktur dasar halaman web.
*   **Tailwind CSS**: Kerangka kerja CSS untuk styling yang cepat dan responsif.
*   **JavaScript (Vanilla JS)**: Logika inti aplikasi, interaksi UI, dan komunikasi API.
*   **Google Gemini API**: Digunakan untuk kemampuan peringkasan teks (model `gemini-1.5-flash-latest`).

## Cara Menggunakan

1.  **Buka Aplikasi**: Buka file `index.html` di browser web Anda.
2.  **Masukkan Kunci API**: Gulir ke bagian bawah halaman dan masukkan Kunci API Google Gemini Anda di kolom yang tersedia. Kunci ini akan disimpan secara lokal di browser Anda.
    *   Jika Anda belum memiliki kunci API, Anda bisa mendapatkannya dari [Google AI Studio](https://aistudio.google.com/app/apikey).
3.  **Tempel atau Ketik Teks**: Masukkan teks yang ingin Anda ringkas ke dalam area teks "Teks Asli Anda". Perhatikan penghitung karakter.
4.  **Ringkas Teks**: Klik tombol "Ringkas Sekarang". Aplikasi akan memproses teks dan menampilkan ringkasan dalam format bullet-point.
5.  **Hapus Teks**: Untuk membersihkan area input dan hasil, klik tombol "Hapus Teks".
6.  **Coba Contoh**: Jika Anda ingin melihat contoh ringkasan, klik tombol "Coba Contoh" untuk memuat teks sampel.
7.  **Salin Hasil**: Setelah ringkasan muncul, Anda dapat menggunakan tombol "Salin sebagai Teks Biasa" atau "Salin dengan Markdown" untuk menyalin hasilnya ke clipboard.
8.  **Matikan/Aktifkan Animasi**: Anda dapat mengaktifkan atau menonaktifkan animasi latar belakang melalui tombol di bagian footer.

## Integrasi API

Aplikasi ini berkomunikasi dengan Google Gemini API menggunakan model `gemini-1.5-flash-latest`. Permintaan dikirim ke endpoint `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash-latest:generateContent` dengan kunci API yang disediakan pengguna.

Prompt yang digunakan untuk peringkasan adalah:
`Analisis teks berikut. Buatkan ringkasan utama dalam format bullet-point dan Bahasa Indonesia (antara 3 hingga 5 poin, tergantung panjang teks). Jangan tambahkan kalimat pembuka atau penutup. Jika teks tidak dapat diringkas, jawab HANYA dengan satu frasa: [TIDAK DAPAT DIRINGKAS]. Teksnya: "..."`

## Pengembangan

Proyek ini adalah aplikasi web mandiri yang terdiri dari satu file HTML (`index.html`) yang mencakup HTML, CSS (dengan Tailwind CSS CDN), dan JavaScript. Tidak ada proses build yang kompleks atau dependensi Node.js yang diperlukan untuk menjalankan aplikasi ini.
