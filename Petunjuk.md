**Peran:** Anda adalah seorang pengembang web Full-Stack ahli bernama Jules.

**Proyek:** Buat sebuah aplikasi web bernama "Peringkas Cerdas".

**Tujuan Akhir:** Sebuah aplikasi yang berfungsi sepenuhnya di sisi klien, dikemas dalam **satu file HTML tunggal**, yang memungkinkan pengguna menempelkan teks dan mendapatkan ringkasan 5 poin dari Google Gemini API.

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
   * Di dalam \<head\>, tambahkan link untuk memuat **Tailwind CSS**:  
     \<script src="https://cdn.tailwindcss.com"\>\</script\>

   * Di dalam \<head\>, tambahkan link untuk memuat font **Inter** dari Google Fonts:  
     \<link rel="preconnect" href="https://fonts.googleapis.com"\>  
     \<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin\>  
     \<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700\&display=swap" rel="stylesheet"\>

4. **Buat Struktur Konten Awal (Unstyled):**  
   * Di dalam \<body\>, buat elemen-elemen HTML berikut tanpa styling terlebih dahulu:  
     * header dengan h1 (Peringkas Cerdas) dan p (tagline).  
     * main yang akan berisi area input dan hasil.  
     * div untuk area input, berisi label dan textarea.  
     * div untuk tombol aksi, berisi button (Ringkas Sekarang).  
     * div untuk area hasil (awalnya kosong).  
     * div untuk indikator loading (awalnya kosong).  
     * div untuk pesan error (awalnya kosong).  
     * footer dengan teks hak cipta.

### **Bagian 2: Implementasi Desain dan Antarmuka Pengguna (Styling dengan Tailwind CSS)**

Sekarang, gunakan kelas-kelas Tailwind CSS untuk menata semua elemen HTML yang telah Anda buat di Bagian 1\.

1. **Layout Utama:**  
   * Pada \<body\>, atur warna latar belakang (bg-gray-50) dan warna teks utama (text-gray-800). Atur font menjadi font-family: 'Inter', sans-serif; menggunakan tag \<style\>.  
   * Buat sebuah div pembungkus utama di dalam \<body\> dengan kelas container mx-auto max-w-3xl px-4 py-8 md:py-12.  
2. **Styling Elemen:**  
   * **Header:** Pusatkan teksnya. Buat h1 menjadi besar dan tebal (text-4xl md:text-5xl font-bold). Buat p di bawahnya lebih kecil (text-lg text-gray-600).  
   * **Main Content Area:** Beri latar belakang putih, padding, sudut membulat, dan bayangan (bg-white p-6 md:p-8 rounded-2xl shadow-lg).  
   * **Area Input (textarea):** Buat lebarnya penuh, beri padding, border, sudut membulat, dan efek focus yang jelas (w-full p-4 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500). Beri placeholder yang deskriptif.  
   * **Tombol Aksi (button):** Beri warna latar belakang biru, teks putih, padding, sudut membulat, dan efek hover & focus yang menarik (bg-blue-600 text-white font-bold py-3 px-8 rounded-lg hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-300).  
   * **Area Hasil:** Beri margin-top, padding-top, dan border-top. Di dalamnya, buat h2 (Hasil Ringkasan) menjadi tebal. Buat tombol "Salin Hasil" di sebelahnya dengan gaya sekunder (bg-gray-200). Area untuk output ringkasan diberi latar belakang abu-abu muda (bg-gray-100).  
   * **Indikator Loading:** Buat sebuah *spinner* animasi sederhana menggunakan CSS dan div. Pusatkan secara horizontal dan vertikal, dan tambahkan teks di bawahnya.  
   * **Pesan Error:** Desain sebagai kotak peringatan dengan latar belakang dan border merah (bg-red-100 text-red-700 border border-red-300).  
   * **Footer:** Pusatkan teksnya dan beri warna abu-abu (text-center mt-8 text-gray-500).  
3. **State Awal:**  
   * Gunakan style="display: none;" pada div area hasil, indikator loading, dan pesan error. Mereka hanya akan muncul saat dibutuhkan melalui JavaScript.

### **Bagian 3: Fungsionalitas Inti (Logika JavaScript & Integrasi API)**

Ini adalah bagian terpenting. Tulis semua logika JavaScript di dalam tag \<script\> di bagian bawah \<body\>.

1. **Referensi DOM:**  
   * Buat variabel untuk semua elemen interaktif yang Anda perlukan (textarea, tombol, area hasil, output ringkasan, loading, error, tombol salin).  
2. **Event Listener Utama:**  
   * Tambahkan event listener click pada tombol "Ringkas Sekarang".  
3. **Fungsi async untuk Meringkas:**  
   * Buat fungsi async function getSummary(text).  
   * **Validasi Input:** Di dalam event listener, periksa jika teks dari textarea kosong. Jika ya, tampilkan pesan error dan hentikan fungsi.  
   * **Kelola UI State:**  
     * Sembunyikan resultContainer dan errorMessage.  
     * Tampilkan loadingIndicator.  
     * Nonaktifkan summarizeBtn dan ubah gayanya menjadi opacity-50 cursor-not-allowed.  
   * **Panggilan fetch ke Gemini API:**  
     * Gunakan try...catch untuk menangani error jaringan atau API.  
     * **URL & API Key:** Targetkan model gemini-2.0-flash:generateContent. Gunakan placeholder untuk API Key: const apiKey \= ""; dan tambahkan komentar bahwa kunci API harus diisi.  
     * **Prompt:** Gunakan prompt yang **tepat** ini: Buatkan 5 poin ringkasan utama (bullet points) dari teks berikut, dalam Bahasa Indonesia:\\n\\n"\[TEKS\_DARI\_PENGGUNA\]"  
     * **Payload:** Buat struktur body JSON yang benar sesuai dokumentasi Gemini API.  
   * **Proses Respons:**  
     * Di dalam try, jika response.ok, parse JSON. Ekstrak teks ringkasan dari response.candidates\[0\].content.parts\[0\].text.  
     * **Tampilkan Hasil:** Ubah teks hasil (yang mungkin mengandung markdown \*) menjadi elemen \<li\> HTML dan masukkan ke dalam summaryOutput. Tampilkan resultContainer.  
   * **Tangani Error:**  
     * Di dalam catch, tampilkan pesan error yang relevan di errorMessage.  
   * **Finalisasi UI (Blok finally):**  
     * Sembunyikan loadingIndicator.  
     * Aktifkan kembali summarizeBtn dan kembalikan gayanya seperti semula.

### **Bagian 4: Fitur Tambahan dan Validasi Akhir**

Selesaikan fungsionalitas kecil dan pastikan semua persyaratan terpenuhi.

1. **Fungsi Salin ke Clipboard:**  
   * Tambahkan event listener click pada copyBtn.  
   * Saat diklik, ambil innerText dari summaryOutput.  
   * Gunakan document.execCommand('copy') (setelah membuat textarea sementara) untuk menyalin teks ke clipboard.  
   * Ubah teks tombol menjadi "Tersalin\!" selama 2-3 detik sebagai umpan balik visual, lalu kembalikan ke "Salin Hasil".  
2. **Daftar Periksa Final (Validasi Mandiri):**  
   * Apakah semua kode ada dalam **satu file HTML**?  
   * Apakah aplikasi sepenuhnya responsif?  
   * Apakah tidak ada *framework* JS yang digunakan?  
   * Apakah tidak ada logika backend, server, atau database?  
   * Apakah tidak ada fitur meringkas dari URL?  
   * Apakah semua state (loading, error, success) berfungsi dengan benar?

Silakan mulai pengembangan berdasarkan panduan bertahap ini.