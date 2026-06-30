# Panduan Data Spreadsheet

Website ini membaca satu CSV publik dari Google Sheets. Semua baris data memakai kolom yang sama, lalu dipisahkan oleh kolom `section`.

## Kolom Utama

- `section` - jenis data, misalnya `work`, `project`, `skill`, atau `certification`.
- `order` - urutan tampil, angka kecil muncul lebih dulu.
- `visible` - isi `TRUE` untuk tampil, `FALSE` untuk disembunyikan.
- `key` - dipakai untuk beberapa section, misalnya nama setting, grup skill, jenis kontak, atau ukuran galeri.
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
title: Sistem Input Laporan Guru
subtitle: Akademik Alif Iqra
description: Web app berbasis Apps Script untuk input laporan guru dan export PDF.
bullets: Form input laporan|Validasi data|Export PDF|Dashboard monitoring
tags: Google Apps Script|Google Sheets|HTML/CSS|PDF Automation
image: assets/student-report.jpeg
featured: TRUE
```

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

## Kapan Perlu Upload Ulang ke GitHub

Tidak perlu upload ulang jika hanya mengubah teks, project, skill, pekerjaan, pendidikan, atau sertifikasi di Google Sheets.

Perlu upload ulang jika:

- mengganti desain CSS,
- mengganti struktur HTML,
- mengubah `site-config.js`,
- menambahkan gambar lokal baru ke folder `assets`.
