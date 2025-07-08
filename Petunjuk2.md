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
   * **Header:** Pusatkan teksnya. Buat h1 besar dan tebal, dan p lebih kecil. Untuk membuat header lebih dinamis dan modern, tambahkan instruksi untuk menyisipkan ikon SVG kecil yang relevan dengan 'kecerdasan' atau 'peringkasan' (seperti ikon otak, bola lampu, atau dokumen) di sebelah judul h1. Berikan juga arahan untuk menambahkan animasi halus pada ikon ini, seperti berdenyut lembut atau berputar perlahan saat kursor mouse menyentuhnya.  
   * **Main Content Area:** Beri latar belakang putih, padding, sudut membulat, dan bayangan.  
   * **Area Input (textarea):** Buat lebarnya penuh, beri padding, border, sudut membulat, dan efek focus. Di bawah textarea, tambahkan sebuah div kecil untuk penghitung karakter (misal: 0/10000) yang diperbarui secara dinamis saat pengguna mengetik. Ini meningkatkan UX dan kontrol.  
   * **Tombol Aksi (button):** Beri gaya dasar (warna, padding, sudut membulat).  
   * **Area Hasil, Loading, Error:** Beri struktur dasar dan styling awal. Untuk Area Hasil, sebelum ada output, tampilkan pesan 'empty state' yang ramah seperti Ringkasan Anda akan muncul di sini. dengan gaya yang sedikit redup. Ini memberikan konteks pada area kosong tersebut.  
   * **Footer:** Pusatkan teksnya dan beri warna abu-abu.  
3. **State Awal:**  
   * Untuk state awal, sembunyikan elemen-elemen ini menggunakan kelas utilitas Tailwind seperti opacity-0, invisible, dan scale-95. Ini akan mempersiapkan elemen untuk animasi yang halus sesuai instruksi di Bagian 5\.

### **Bagian 3: Fungsionalitas Inti (Logika JavaScript & Integrasi API)**

Tulis semua logika JavaScript di dalam tag \<script\> di bagian bawah \<body\>.

1. **Referensi DOM:**  
   * Buat variabel untuk semua elemen interaktif.  
2. **Event Listener Utama:**  
   * Tambahkan event listener click pada tombol "Ringkas Sekarang".  
3. **Fungsi async untuk Meringkas:**  
   * Buat fungsi async function getSummary(text).  
   * **Validasi Input:** Hentikan fungsi jika input kosong.  
   * **Kelola UI State:** Sembunyikan tombol 'Ringkas' dan 'Hapus', lalu tampilkan indikator loading bersama dengan tombol 'Batalkan'. Logika JavaScript harus menggunakan AbortController untuk membatalkan permintaan fetch saat tombol 'Batalkan' diklik.  
   * **Panggilan fetch ke Gemini API:**  
     * Gunakan try...catch...finally.  
     * Targetkan model gemini-2.0-flash:generateContent.  
     * Untuk meningkatkan pengalaman pengembang secara signifikan, ganti pendekatan ini. Instruksikan untuk membuat sebuah input field (mungkin di footer atau modal yang dapat disembunyikan) tempat pengembang dapat memasukkan kunci API mereka. Simpan kunci ini ke localStorage browser. Saat aplikasi dimuat, periksa localStorage terlebih dahulu. Jika tidak ada kunci, minta pengguna untuk memasukkannya. Ini menghilangkan kebutuhan untuk mengedit kode setiap kali menguji.  
     * Gunakan prompt yang lebih fleksibel: Analisis teks berikut. Buatkan ringkasan utama dalam format bullet-point dan Bahasa Indonesia (antara 3 hingga 5 poin, tergantung panjang teks). Jangan tambahkan kalimat pembuka atau penutup. Jika teks tidak dapat diringkas, jawab HANYA dengan satu frasa: \[TIDAK DAPAT DIRINGKAS\]. Teksnya: "\[TEKS\_DARI\_PENGGUNA\]"  
     * Setelah menerima respons dari API, instruksikan untuk memproses teksnya. Gunakan regular expression atau metode string untuk hanya mengekstrak baris yang dimulai dengan tanda \* atau \-. Ini memastikan hanya poin-poin ringkasan yang ditampilkan, menghilangkan teks lain yang tidak relevan.  
   * **Proses Respons & Error Granular:** Di dalam blok catch, periksa status error. Jika error.response.status adalah 400 atau 403, tampilkan pesan spesifik seperti "Kunci API tidak valid atau salah. Silakan periksa kembali." Untuk error lainnya, tampilkan pesan generik seperti "Terjadi kesalahan jaringan." Di dalam blok try, setelah memastikan response.ok, periksa apakah response.candidates ada dan tidak kosong. Jika tidak, tampilkan pesan error Maaf, teks ini tidak dapat diringkas.  
   * **Blok finally:** Selalu kembalikan UI ke keadaan normal (sembunyikan loading, aktifkan tombol).

### **Bagian 4: Fitur Tambahan Awal**

Selesaikan fungsionalitas kecil sebelum desain ulang.

1. **Tombol Aksi Tambahan:** Di sebelah tombol 'Ringkas Sekarang', tambahkan tombol 'Hapus' dengan gaya sekunder. Selain tombol 'Hapus', tambahkan tautan atau tombol 'Coba Contoh'. Untuk membuat fitur ini lebih efektif, berikan instruksi yang lebih spesifik mengenai konten contoh. Instruksikan AI untuk menggunakan cuplikan artikel berita netral (sekitar 200-300 kata) dalam Bahasa Indonesia tentang topik umum seperti teknologi atau lingkungan. Ini memastikan contohnya relevan dan bebas dari bias.  
2. **Fungsi Salin Fleksibel & Simpan Otomatis:**  
   * Di sebelah judul "Hasil Ringkasan", sediakan dua tombol ikon kecil: satu untuk "Salin sebagai Teks Biasa" (menghilangkan markdown) dan satu lagi untuk "Salin dengan Markdown" (mempertahankan tanda \* atau \-). Ini adalah fitur canggih yang berguna untuk berbagai kasus penggunaan.  
   * Berikan umpan balik visual singkat saat berhasil menyalin (misal: ikon berubah menjadi ikon centang).  
   * Tambahkan fitur 'Simpan Otomatis Draf' untuk UX yang superior. Instruksikan untuk menggunakan localStorage untuk secara otomatis menyimpan konten dari textarea saat pengguna mengetik (misalnya, setiap beberapa detik). Saat halaman dimuat, periksa apakah ada draf yang tersimpan dan jika ada, pulihkan teks tersebut ke dalam textarea. Ini mencegah kehilangan pekerjaan jika halaman tidak sengaja disegarkan.

### **Bagian 5: Desain Ulang Modern & Peningkatan UX**

Sekarang, tingkatkan desain dari Bagian 2 menjadi sesuatu yang luar biasa, modern, dan futuristik.

1. **Palet Warna & Tema Gelap (Dark Mode):**  
   * Selain latar belakang gelap, tambahkan elemen SVG gradien yang lembut dan beranimasi lambat di latar belakang. Objek ini harus bergerak perlahan di belakang konten utama untuk menciptakan kedalaman dan daya tarik visual tanpa mengganggu. Di footer, sertakan sebuah tombol sakelar (toggle) kecil untuk "Matikan Animasi". Secara default, animasi latar belakang ini aktif. Jika pengguna mematikannya, sembunyikan atau hentikan animasi SVG latar belakang melalui JavaScript. Ini menghormati preferensi pengguna dan membantu perangkat dengan spesifikasi lebih rendah.  
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
7. **Aksesibilitas (A11y) Fundamental**: Instruksikan untuk memastikan semua elemen interaktif dapat diakses sepenuhnya melalui keyboard. Tambahkan atribut ARIA yang relevan, misalnya aria-live="polite" pada div area hasil agar pembaca layar dapat mengumumkan ringkasan baru secara otomatis saat muncul.

### **Bagian 6: Validasi Akhir**

Selesaikan fungsionalitas dan pastikan semua persyaratan terpenuhi.

1. **Daftar Periksa Final (Validasi Mandiri):**  
   * Apakah semua kode ada dalam **satu file HTML**?  
   * Apakah aplikasi sepenuhnya responsif dan terlihat luar biasa di mode gelap?  
   * Apakah semua transisi dan animasi berjalan mulus? Perkuat poin ini dengan menambahkan spesifikasi teknis. Instruksikan: 'Pastikan animasi, terutama SVG latar belakang yang bergerak, dioptimalkan untuk performa. Gunakan properti CSS transform dan opacity untuk animasi yang dipercepat perangkat keras (hardware-accelerated) dan hindari properti yang memicu layout-reflow seperti margin atau top/left. Animasi harus terasa mulus bahkan pada perangkat dengan spesifikasi lebih rendah.'  
   * Apakah tidak ada *framework* JS yang digunakan?  
   * Apakah tidak ada logika backend, server, atau database?  
   * Apakah semua state (loading, error, success) berfungsi dengan benar dan terlihat elegan?  
   * Apakah perilaku textarea setelah peringkasan sudah jelas? (Contoh: Teks asli harus tetap ada di textarea untuk memungkinkan modifikasi dan peringkasan ulang).  
   * Apakah kode JavaScript terstruktur dengan baik, menggunakan nama variabel yang jelas, dan memiliki komentar di bagian yang kompleks untuk menjelaskan logika? Kode harus mudah dibaca dan dipelihara oleh pengembang lain.

Silakan mulai pengembangan berdasarkan panduan bertahap yang komprehensif ini.