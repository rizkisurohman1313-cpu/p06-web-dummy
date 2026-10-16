# P06 · Web Dummy Keamanan AI/LLM & Prompt Injection

Praktikum Mata Kuliah **Keamanan Sistem Informasi (PMI 1522)** - Semester 5  
Program Studi Manajemen Informatika - Politeknik Negeri Lampung

* **Nama:** Rizki Surohman
* **NPM:** 24781024
* **Kelas:** 5A
* **Kasus:** LIVE-2 · Peringkas Ulasan Produk (Indirect Prompt Injection)
* **Model AI:** Google Gemini (`gemini-2.5-flash`)

---

## Tautan Live Demo (Netlify)

* **Versi Rentan:** [https://quiet-tiramisu-441796.netlify.app/24781024-ulasan-rentan.html](https://quiet-tiramisu-441796.netlify.app/24781024-ulasan-rentan.html)
* **Versi Aman:** [https://quiet-tiramisu-441796.netlify.app/24781024-ulasan-aman.html](https://quiet-tiramisu-441796.netlify.app/24781024-ulasan-aman.html)

---

## File dalam Repositori

1. **`24781024-ulasan-rentan.html` (Versi Rentan)**
   * Menggabungkan aturan sistem, permintaan pengguna, dan teks ulasan pihak ketiga menjadi satu teks datar tanpa pemisahan peran/otoritas.
   * Tidak memiliki validasi keluaran maupun karantina konten.
   * Terbukti rentan terhadap injeksi tidak langsung ketika ulasan disisipi perintah tersembunyi `INJEKSI-P06-77-LIVE`.

2. **`24781024-ulasan-aman.html` (Versi Aman)**
   * Memasang empat lapis pertahanan **di luar model AI**:
     1. **Karantina Ulasan:** Mendeteksi kalimat bermotif perintah sebelum prompt dibentuk menggunakan normalisasi teks NFKC dan pencocokan pola instruksi.
     2. **Hierarki Instruksi:** Memisahkan peran aturan sistem, permintaan pengguna, dan membungkus ulasan ke dalam blok `<DATA_ULASAN>` sebagai data tak tepercaya.
     3. **Validasi Keluaran:** Memeriksa teks balasan model terhadap pola penanda terlarang, tag HTML, atau skrip berbahaya sebelum dirender.
     4. **Penonaktifan Tool:** Memastikan tidak ada aksi/tool yang dapat dieksekusi selama tugas meringkas ulasan.
