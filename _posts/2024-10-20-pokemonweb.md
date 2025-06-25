---
title: 🖼️ Pokemon Gallery Website
date: 2024-10-20 00:00:00 +0800
categories: [praktikum]
tags: [HTML, CSS, Bootstrap]
image:
  path: /assets/images/post/pokemon/pokemon wallpaper.png
  alt: Pokemon Gallery WEB Thumbnail
---

# Pokemon Gallery Website

## Deskripsi Proyek

**Pokemon Gallery** adalah sebuah website interaktif yang menampilkan berbagai macam Pokemon berdasarkan pengelompokan warnanya. Website ini dirancang sebagai bagian dari tugas praktikum web development, dengan fokus pada pengalaman pengguna yang menarik dan desain yang responsif.

---

## 🎨 Fitur Utama

### 🔗 **Navigasi Multi-halaman**
Website ini terdiri dari tiga halaman utama berdasarkan pengelompokan warna Pokemon:
- **Halaman Pokemon Merah** (`index3.html`)
- **Halaman Pokemon Biru** (`index.html`)
- **Halaman Pokemon Kuning** (`index2.html`)

Navigasi dapat dilakukan melalui logo di navbar.

---

### 🖼️ **Hero Section**
Setiap halaman memiliki hero section yang unik:
- Latar belakang warna sesuai tema (merah, biru, atau kuning)
- Logo Pokemon yang relevan untuk setiap kategori

---

### 📷 **Screenshot Website**
<div align="center">
    <table>
        <tr>
            <td align="center" width="50%">
                <strong>Pokemon Blue</strong><br>
                <img src="/assets/images/post/pokemon/screencapture-127-0-0-1-5500-index-html-2025-06-25-17_04_12.png" alt="SignUp" style="width: 100%; max-width: 400px; height: auto;">
            </td>
        </tr>
    </table>
</div>
<div align="center">
    <table>
        <tr>
            <td align="center" width="50%">
                <strong>Pokemon Red</strong><br>
                <img src="/assets/images/post/pokemon/screencapture-127-0-0-1-5500-index3-html-2025-06-25-17_04_27.png" alt="SignUp" style="width: 100%; max-width: 400px; height: auto;">
            </td>
            <td align="center" width="50%">
                <strong>Pokemon Yellow</strong><br>
                <img src="/assets/images/post/pokemon/screencapture-127-0-0-1-5500-index2-html-2025-06-25-17_03_44.png" alt="SignIn" style="width: 100%; max-width: 400px; height: auto;">
            </td>
        </tr>
    </table>
</div>

---

### 📱 **Responsive Design**
Dirancang dengan **Bootstrap 5** untuk memastikan tampilan yang konsisten di semua ukuran layar.

---

### ℹ️ **About Section**
Berisi informasi tentang tujuan website dan misi untuk menampilkan berbagai jenis Pokemon.

---

## 🚀 Teknologi yang Digunakan

- **HTML5**
- **CSS3**
- **Bootstrap 5.3.3**
- **Custom CSS** (styles.css)

---

## 📁 Struktur Folder

```plaintext
├── index.html           # Halaman Pokemon Biru
├── index2.html          # Halaman Pokemon Kuning
├── index3.html          # Halaman Pokemon Merah
├── styles.css           # Custom CSS styling
├── Pokemon Logo.png     # Logo utama Pokemon
├── BluePokemon/         # Folder untuk aset Pokemon biru
│   ├── Blastoise.png
│   ├── Green Ninja.png
│   ├── Pokemon Blue Logo.png
│   └── Sharpedo.png
├── RedPokemon/          # Folder untuk aset Pokemon merah
│   ├── Cinderace.png
│   ├── Emboar.png
│   ├── Infernape.png
│   └── Pokemon Red Logo.png
├── YellowPokemon/       # Folder untuk aset Pokemon kuning
│   ├── Manectric.png
│   ├── Pikachu.png
│   ├── Pokemon Yellow Logo.png
│   └── Zapdos.png
└── TypeIkon/            # Ikon tipe Pokemon
    ├── Dark Type.png
    ├── Electric.png
    ├── Fighter Type.png
    ├── Fire Type.png
    └── Water Type.png
```

---

## 🔧 Masalah yang Perlu Diperbaiki

1. **Path Navbar**: Saat ini menggunakan path absolut (`C:\T_Praktikum3_H071231092\`) yang tidak kompatibel dengan deployment. Path perlu diperbarui agar relatif terhadap root proyek.
2. **Konsistensi Navigasi**: Beberapa tautan di navbar perlu diperbaiki agar lebih konsisten.

---

## 💡 Cara Menggunakan

1. Buka salah satu file HTML (`index.html`, `index2.html`, atau `index3.html`) di browser web.
2. Gunakan navbar di bagian atas untuk berpindah antara halaman Pokemon merah, biru, dan kuning.
3. Klik tombol **"Explore Now"** pada hero section untuk langsung menuju ke galeri Pokemon.
4. Jelajahi deskripsi setiap Pokemon untuk mengetahui informasi lebih lanjut.

---

## 🌟 Pengembangan di Masa Depan

- 🌟 Menambahkan lebih banyak Pokemon ke dalam galeri
- 🔍 Menambahkan fitur pencarian
- 📄 Menambahkan halaman detail untuk setiap Pokemon
- 🔄 Menambahkan fitur filter berdasarkan tipe Pokemon
- ✉️ Implementasi form kontak yang berfungsi

---

💻 **Dibuat sebagai tugas praktikum H071231092**