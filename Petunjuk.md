**Peran:** Anda adalah seorang pengembang web Full-Stack ahli bernama Jules.

**Proyek:** Buat sebuah aplikasi web bernama "Peringkas Cerdas".

**Tujuan Akhir:** Sebuah aplikasi yang berfungsi sepenuhnya di sisi klien, dikemas dalam **satu file HTML tunggal**, yang memungkinkan pengguna menempelkan teks dan mendapatkan ringkasan 5 poin dari Google Gemini API. Aplikasi ini harus memiliki desain yang sangat modern dan menarik.

Ikuti instruksi ini secara bertahap.

### **Bagian 1: Konsep Umum dan Pengaturan Dasar (Struktur HTML & Teknologi)**

Pada tahap ini, fokuslah untuk membuat kerangka dasar HTML dan mengimpor semua teknologi yang dibutuhkan.

1. **Buat Struktur File:**  
   * Buat satu file bernama index.html. Semua kode (HTML, CSS, dan JavaScript) akan berada di dalam file ini.  
2. **Siapkan Kerangka HTML:**  
   * Gunakan struktur HTML5 semantik (\<\!DOCTYPE html\>, \<html\>, \<head\>, \<body\>).  
   * Di dalam \<head\>, tambahkan tag \<meta\> untuk charset="UTF-8" dan viewport.  
   * Berikan judul halaman: \<title\>Peringkas Cerdas\</title\>.  
3. **Impor Teknologi via CDN:**  
   * Di dalam \<head\>, tambahkan link untuk memuat **Tailwind CSS**.  
   * Di dalam \<head\>, tambahkan link untuk memuat font **Inter** dari Google Fonts.  
4. **Buat Struktur Konten Awal (Unstyled):**  
   * Di dalam \<body\>, buat elemen-elemen HTML berikut: header, main (dengan div untuk input, tombol, hasil, loading, error), dan footer.

### **Bagian 2: Implementasi Desain Dasar (Styling Awal dengan Tailwind CSS)**

Gunakan kelas-kelas Tailwind CSS untuk menata semua elemen HTML yang telah Anda buat. Ini adalah fondasi sebelum kita melakukan desain ulang di Bagian 5\.

1. **Layout Utama:**  
   * Atur warna latar belakang dasar, warna teks, dan font pada \<body\>.  
   * Buat div pembungkus utama dengan kelas container mx-auto max-w-3xl px-4 py-8 md:py-12.  
2. **Styling Elemen:**  
   * **Header:** Pusatkan teksnya. Buat h1 besar dan tebal, dan p lebih kecil.  
   * **Main Content Area:** Beri latar belakang putih, padding, sudut membulat, dan bayangan.  
   * **Area Input (**textarea**):** Buat lebarnya penuh, beri padding, border, sudut membulat, dan efek focus.  
   * **Tombol Aksi (**button**):** Beri gaya dasar (warna, padding, sudut membulat).  
   * **Area Hasil, Loading, Error:** Beri struktur dasar dan styling awal.  
   * **Footer:** Pusatkan teksnya dan beri warna abu-abu.  
3. **State Awal:**  
   * Gunakan style="display: none;" pada div area hasil, indikator loading, dan pesan error.

### **Bagian 3: Fungsionalitas Inti (Logika JavaScript & Integrasi API)**

Tulis semua logika JavaScript di dalam tag \<script\> di bagian bawah \<body\>.

1. **Referensi DOM:**  
   * Buat variabel untuk semua elemen interaktif.  
2. **Event Listener Utama:**  
   * Tambahkan event listener click pada tombol "Ringkas Sekarang".  
3. **Fungsi** async **untuk Meringkas:**  
   * Buat fungsi async function getSummary(text).  
   * **Validasi Input:** Hentikan fungsi jika input kosong.  
   * **Kelola UI State:** Tampilkan loading, sembunyikan elemen lain, nonaktifkan tombol.  
   * **Panggilan** fetch **ke Gemini API:**  
     * Gunakan try...catch...finally.  
     * Targetkan model gemini-2.0-flash:generateContent.  
     * Gunakan placeholder untuk API Key: const apiKey \= ""; dengan komentar yang jelas.  
     * Gunakan prompt yang tepat: Buatkan 5 poin ringkasan utama (bullet points) dari teks berikut, dalam Bahasa Indonesia:\\n\\n"\[TEKS\_DARI\_PENGGUNA\]"  
   * **Proses Respons & Error:** Tampilkan hasil atau pesan error di UI.  
   * **Blok** finally**:** Selalu kembalikan UI ke keadaan normal (sembunyikan loading, aktifkan tombol).

### **Bagian 4: Fitur Tambahan Awal**

Selesaikan fungsionalitas kecil sebelum desain ulang.

1. **Fungsi Salin ke Clipboard:**  
   * Implementasikan fungsi salin pada tombol "Salin Hasil".  
   * Berikan umpan balik visual singkat saat berhasil menyalin (misal: teks tombol berubah menjadi "Tersalin\!").

### **Bagian 5: Desain Ulang Modern & Peningkatan UX**

Sekarang, tingkatkan desain dari Bagian 2 menjadi sesuatu yang luar biasa, modern, dan futuristik.

1. **Palet Warna & Tema Gelap (Dark Mode):**  
   * Ubah \<body\> menjadi tema gelap: bg-gray-900 text-gray-200.  
   * Gunakan **Glassmorphism** untuk kontainer utama (main): Beri warna latar belakang semi-transparan dengan efek blur. Contoh: bg-white/10 backdrop-blur-lg border border-white/20.  
2. **Tombol Aksi dengan Gradient:**  
   * Ubah tombol "Ringkas Sekarang" agar menggunakan **gradient** yang cerah, misalnya dari ungu ke biru (bg-gradient-to-r from-purple-500 to-blue-500).  
   * Tambahkan transisi halus dan efek hover yang membuatnya sedikit lebih cerah atau membesar (transition-all duration-300 hover:scale-105 hover:shadow-lg hover:shadow-blue-500/50).  
3. **Animasi & Transisi Halus:**  
   * Ganti display: none dengan kelas-kelas transisi dari Tailwind. Gunakan opacity-0, invisible, scale-95 untuk state tersembunyi, dan opacity-100, visible, scale-100 untuk state terlihat, ditambah dengan kelas transition-all duration-300.  
   * Terapkan ini pada area hasil, indikator loading, dan pesan error agar muncul dan menghilang dengan efek *fade* dan *scale* yang lembut.  
4. **Desain Area Hasil yang Lebih Baik:**  
   * Hilangkan latar belakang abu-abu pada summaryOutput.  
   * Untuk setiap \<li\> hasil ringkasan, berikan padding, border-bottom yang tipis (border-white/10), dan tambahkan ikon SVG kecil (misalnya ikon panah atau *bullet*) di sebelah kiri setiap poin untuk hierarki visual yang lebih baik.  
5. **Ikonografi Modern (SVG):**  
   * Ganti teks "Salin Hasil" pada tombol salin dengan **ikon SVG** untuk menyalin. Saat berhasil disalin, ganti ikon tersebut dengan ikon centang (check mark) selama beberapa detik. Gunakan ikon dari sumber seperti Heroicons atau Feather Icons.  
6. **Indikator Loading yang Elegan:**  
   * Ganti spinner standar dengan animasi yang lebih modern, misalnya tiga titik yang berdenyut (pulsing dots) dengan warna gradient yang sama dengan tombol utama.

### **Bagian 6: Validasi Akhir**

Selesaikan fungsionalitas dan pastikan semua persyaratan terpenuhi.

1. **Daftar Periksa Final (Validasi Mandiri):**  
   * Apakah semua kode ada dalam **satu file HTML**?  
   * Apakah aplikasi sepenuhnya responsif dan terlihat luar biasa di mode gelap?  
   * Apakah semua transisi dan animasi berjalan mulus?  
   * Apakah tidak ada *framework* JS yang digunakan?  
   * Apakah tidak ada logika backend, server, atau database?  
   * Apakah semua state (loading, error, success) berfungsi dengan benar dan terlihat elegan?

Silakan mulai pengembangan berdasarkan panduan bertahap yang komprehensif ini.

