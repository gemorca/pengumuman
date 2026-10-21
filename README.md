<div align="center">

# 🎓 Pengumuman Kelulusan

**Website pengumuman kelulusan siswa kelas IX. Cukup masukkan NISN, hasil langsung tampil.**

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Google Sheets](https://img.shields.io/badge/Google_Sheets-34A853?style=for-the-badge&logo=googlesheets&logoColor=white)

</div>

---

## 📖 Tentang Proyek

Portal sederhana untuk mengumumkan hasil kelulusan siswa SMP. Siswa memasukkan **NISN 10 digit**, lalu halaman menampilkan nama, foto, status kelulusan, dan pesan pribadi dari sekolah. Data dikelola lewat **Google Sheets** dan dilayani oleh **Google Apps Script**, sehingga pihak sekolah bisa memperbarui data tanpa menyentuh kode.

Situs ini murni statis (HTML, CSS, dan JavaScript), ringan, dan bisa di-hosting gratis di mana saja.

## ✨ Fitur

- **Pencarian berdasarkan NISN** dengan validasi: harus 10 digit angka.
- **Hasil instan**: nama siswa, foto (opsional), status, dan pesan pribadi.
- **Status berwarna**: `LULUS` tampil dengan gaya khusus, status lain (misalnya ditunda) dengan gaya berbeda.
- **Indikator loading** dan tombol yang dinonaktifkan selama pemeriksaan.
- **Pesan galat yang jelas** untuk NISN tidak valid, data tidak ditemukan, atau server tidak dapat dijangkau.
- **Tekan Enter** untuk mencari, tanpa perlu klik tombol.
- **Responsif**: nyaman dibuka di ponsel, tablet, maupun desktop.
- **Pesan Kepala Sekolah** di bagian bawah halaman.
- **Tanpa framework dan tanpa proses build**.

## 🗂️ Struktur Proyek

```
.
├── index.html       # Halaman utama
├── css/
│   └── style.css    # Seluruh gaya tampilan
└── js/
    └── script.js    # Validasi NISN, pengambilan data, dan tampilan hasil
```

## 🚀 Menjalankan Secara Lokal

```bash
git clone https://github.com/gemorca/<nama-repo>.git
cd <nama-repo>

# pilih salah satu
python -m http.server 8000
npx serve .
```

Buka `http://localhost:8000`.

> Berkas CSS dan JS dipanggil dengan jalur dari akar situs (`/css/style.css` dan `/js/script.js`). Jalankan situs dari **akar domain** atau server lokal seperti di atas. Membuka `index.html` langsung lewat `file://` tidak akan memuat gaya dan skrip.

## 🔌 Menyiapkan Backend (Google Sheets + Apps Script)

### 1. Siapkan Google Sheets

Buat satu sheet dengan **baris pertama sebagai header** berikut:

| id | nama | status | pesan | foto |
|---|---|---|---|---|
| `1234567890` | Nama Siswa | `LULUS` | Selamat atas kelulusanmu! | `https://.../foto.jpg` |

| Kolom | Keterangan |
|---|---|
| `id` | **NISN** siswa, 10 digit angka. Simpan sebagai teks agar angka nol di depan tidak hilang |
| `nama` | Nama lengkap siswa |
| `status` | `LULUS`, atau teks lain untuk status selain lulus |
| `pesan` | Pesan pribadi yang tampil di bawah status |
| `foto` | URL foto (opsional). Kosongkan bila tidak ada |

### 2. Buat Web App Apps Script

Buat Web App yang mengembalikan isi sheet sebagai **JSON berbentuk array objek**, dengan nama kunci sama dengan header di atas.

```json
[
  { "id": "1234567890", "nama": "Nama Siswa", "status": "LULUS", "pesan": "Selamat!", "foto": "" }
]
```

### 3. Sambungkan ke situs

Buka `js/script.js` lalu ganti nilai `urlAPI` dengan URL Web App Anda.

```js
const urlAPI = "https://script.google.com/macros/s/XXXXXXXX/exec";
```

## ⚙️ Kustomisasi

| Yang ingin diubah | Lokasi |
|---|---|
| URL backend | variabel `urlAPI` di `js/script.js` |
| Nama sekolah, judul halaman, dan tahun ajaran | `index.html` |
| Pesan Kepala Sekolah | bagian `message-section` di `index.html` |
| Logo sekolah | ganti elemen `.logo-placeholder` di `index.html` dengan gambar |
| Warna tema | variabel `--primary-color` dan `--secondary-color` di `css/style.css` |
| Panjang NISN | pemeriksaan `input.length !== 10` di `js/script.js` dan atribut `maxlength` di `index.html` |

## 🔒 Catatan Keamanan dan Privasi

Data kelulusan bersifat pribadi. Perhatikan hal berikut sebelum situs dipublikasikan:

- **Pencocokan NISN saat ini dilakukan di browser.** Skrip mengunduh seluruh daftar siswa dari Apps Script, lalu mencari NISN yang cocok. Artinya siapa pun yang mengetahui URL Web App bisa melihat data seluruh siswa.
- **Rekomendasi:** ubah Apps Script agar menerima NISN sebagai parameter (misalnya `?id=1234567890`) dan **hanya mengembalikan satu data** yang cocok, lalu sesuaikan `js/script.js` untuk memanggil URL tersebut.
- Pertimbangkan membuka pengumuman hanya pada waktu yang ditentukan, misalnya dengan menolak permintaan sebelum jam pengumuman di sisi Apps Script.
- Batasi akses edit pada Google Sheets hanya untuk panitia yang berwenang.

## 🛠️ Teknologi

- **HTML5**, **CSS3**, dan **JavaScript** (Vanilla)
- **Google Sheets** dan **Google Apps Script** sebagai database dan backend
- [Google Fonts](https://fonts.google.com/specimen/Poppins) (Poppins)

## 👤 Kredit

Seluruh antarmuka, kode, dan desain proyek ini dibuat sepenuhnya oleh:

**Moh. Agil S. Abdul**
[GitHub](https://github.com/gemorca) · [Instagram](https://instagram.com/mohammadagill)

> Pustaka dan layanan pihak ketiga yang disebutkan di bagian Teknologi tetap menjadi milik masing-masing pembuatnya dan digunakan sesuai ketentuan mereka.

## 📄 Lisensi

Hak Cipta © 2026 **Moh. Agil S. Abdul**. Seluruh hak dilindungi (*All Rights Reserved*).

Kode sumber dan desain dalam repositori ini dibuat dan dimiliki sepenuhnya oleh pemilik hak cipta. Anda bebas memakai, mengubah, dan membagikannya dengan tetap mencantumkan pemberitahuan hak cipta di atas.

---

<div align="center">

**Pengumuman Kelulusan** · Dibuat sendiri oleh Moh. Agil S. Abdul.

</div>
