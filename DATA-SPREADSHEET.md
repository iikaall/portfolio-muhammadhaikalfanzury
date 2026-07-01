# Panduan Data Spreadsheet

Website ini membaca satu CSV publik dari Google Sheets. Semua baris data memakai kolom yang sama, lalu dipisahkan oleh kolom `section`.

## Kolom Utama

- `section` - jenis data, misalnya `work`, `project`, `skill`, atau `certification`.
- `order` - urutan tampil, angka kecil muncul lebih dulu.
- `visible` - isi `TRUE` untuk tampil, `FALSE` untuk disembunyikan.
- `key` - dipakai untuk beberapa section, misalnya nama setting, grup skill, jenis kontak, kode proyek, atau ukuran galeri.
- `title` - judul utama data.
- `subtitle` - keterangan pendek, misalnya nama perusahaan atau kategori proyek.
- `period` - periode waktu, misalnya `2021 - Sekarang`.
- `value` - nilai data, sering dipakai untuk setting, stat, skill, dan kontak.
- `description` - deskripsi utama.
- `bullets` - daftar poin, pisahkan dengan `|`.
- `tags` - tools atau label, pisahkan dengan `|`.
- `image` - path gambar lokal atau URL gambar publik.
- `alt` - deskripsi gambar untuk aksesibilitas.
- `link_label` - teks tombol link.
- `link_url` - URL tujuan.
- `featured` - isi `TRUE` untuk membuat project tampil sebagai kartu utama.
- `size` - ukuran galeri, bisa `tall`, `wide`, atau dikosongkan.

Untuk custom tampilan, gunakan `section = setting`, lalu isi `key` dengan nama yang diawali `style_`. Daftar style yang aman dipakai ada di `CUSTOMIZE.md`.

## Contoh Section

### Histori Pekerjaan

```text
section: work
title: Admin HRD
subtitle: PT Sahabat Alif Indonesia
period: 2021 - Sekarang
description: Mengelola absensi guru, pengajuan fee, dashboard reporting, dan sistem absensi.
```

### Portfolio Projek

```text
section: project
key: sistem-input-laporan
title: Sistem Input Laporan Guru
subtitle: Akademik Alif Iqra
description: Web app berbasis Apps Script untuk input laporan guru dan export PDF.
bullets: Form input laporan|Validasi data|Export PDF|Dashboard monitoring
tags: Google Apps Script|Google Sheets|HTML/CSS|PDF Automation
image: assets/student-report.jpeg
featured: TRUE
```

Kartu proyek akan tampil ringkas lebih dulu. Saat diklik, kartu akan membuka detail lengkap seperti `description`, `bullets`, `tags`, tombol `link_url`, dan media terkait.

### Galeri atau Video Terkait Proyek

Gunakan `section: project_media`. Isi `key` dengan kode yang sama seperti proyeknya.

```text
section: project_media
key: sistem-input-laporan
title: Video demo laporan
subtitle: video
description: Video singkat cara kerja sistem.
image: assets/student-report.jpeg
alt: Thumbnail video laporan
link_label: Lihat video
link_url: https://www.youtube.com/watch?v=VIDEO_ID
size: wide
```

Untuk gambar terkait proyek, isi `subtitle: image`, lalu isi kolom `image`.

### Skill

```text
section: skill
key: professional
value: Google Apps Script
```

Grup skill yang tersedia:

- `professional`
- `additional`
- `language`

### Sertifikasi

```text
section: certification
title: Nama Sertifikasi
subtitle: Nama lembaga
period: 2026
description: Ringkasan singkat sertifikasi.
tags: Certificate|Data
link_label: Lihat sertifikat
link_url: https://example.com
```

### Instagram

Tambahkan baris kontak seperti ini:

```text
section: contact
key: instagram
title: Instagram
value: @username_instagram
```

Kalau `link_url` dikosongkan, website otomatis membuat link Instagram dari `value`.

### Video di Galeri

Gunakan `section: gallery`, isi `subtitle: video`, lalu taruh URL YouTube/Vimeo/video di `link_url`.

```text
section: gallery
key: video
title: Video Profil
subtitle: video
image: assets/talent-qori.jpg
link_label: Lihat video
link_url: https://www.youtube.com/watch?v=VIDEO_ID
size: wide
```

## Kapan Perlu Upload Ulang ke GitHub

Tidak perlu upload ulang jika hanya mengubah teks, project, skill, pekerjaan, pendidikan, atau sertifikasi di Google Sheets.

Perlu upload ulang jika:

- mengganti desain CSS,
- mengganti struktur HTML,
- mengubah `site-config.js`,
- menambahkan gambar lokal baru ke folder `assets`.

## Bagian yang Membuat Website Dinamis

Bagian dinamisnya ada di tiga tempat:

- `site-config.js` menyimpan URL CSV Google Sheets.
- `script.js` mengambil data dari URL CSV tersebut, membaca kolom `section`, lalu mengganti isi HTML.
- elemen di `index.html` yang punya atribut `data-render` dan `data-field` menjadi tempat data spreadsheet ditampilkan.

Contoh:

```html
<div class="project-list" data-render="projects"></div>
```

Bagian itu akan diisi otomatis dari baris spreadsheet dengan `section` bernilai `project`.

## Cara Kerja Kolom Visible

Kolom `visible` dipakai untuk mengatur tampil/sembunyi:

- `TRUE` atau kosong: tampil.
- `FALSE`: sembunyi.

Jika semua data pada satu section dibuat `FALSE`, section tersebut akan disembunyikan dari halaman dan menu navigasi.

Jika `FALSE` tidak berpengaruh di website live, biasanya penyebabnya salah satu dari ini:

- `site-config.js` belum memakai URL CSV Google Sheets yang benar.
- Google Sheets belum dipublish ulang sebagai CSV.
- file terbaru belum diupload ke GitHub.
- browser masih memegang cache lama, coba hard refresh.
