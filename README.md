# Gasing Circle Community Layout — Theme Component

Theme component untuk Discourse forum **Gasing Circle Community**, menambahkan fitur background image kustom dengan efek glassmorphism pada halaman kategori.

---

## Fitur

- **Background image kustom** yang bisa diatur langsung dari panel pengaturan tema Discourse (tanpa edit kode)
- **Overlay gelap** tipis (`rgba(0,0,0,0.15)`) di atas gambar agar teks tetap terbaca
- **Efek glassmorphism** pada area konten (topic list, card) menggunakan `backdrop-filter: blur`
- **Conditional rendering** — tidak ada CSS yang di-emit sama sekali jika gambar belum diupload

---

## Cakupan

Style hanya diterapkan pada halaman kategori `general` (`body.category-general`). Halaman lain tidak terpengaruh.

---

## Instalasi

### Dari Git Repository

1. Buka **Admin → Appearance → Themes**
2. Klik **Install** → **From a git repository**
3. Masukkan URL repository ini
4. Aktifkan sebagai **component** dan pasangkan ke tema utama yang digunakan

### Manual (Upload File)

1. Buka **Admin → Appearance → Themes → Install → From local files**
2. Upload seluruh file dari repository ini

---

## Pengaturan

Setelah dipasang, buka tab **Settings** pada component ini:

| Setting | Tipe | Keterangan |
|---|---|---|
| `bg_image` | Upload | Gambar yang akan dijadikan background pada halaman kategori General |

Upload gambar di kolom `bg_image`, lalu simpan. Style akan otomatis aktif.

**Rekomendasi gambar:**
- Format: JPG atau WebP
- Resolusi minimal: 1920 × 1080 px
- Ukuran file: di bawah 500 KB untuk performa optimal

---

## Struktur File

```
├── about.json           # Metadata Discourse theme component
├── settings.yml         # Definisi setting bg_image (upload)
├── common/
│   └── common.scss      # CSS utama — background + overlay + glassmorphism
└── README.md
```

---

## Detail Teknis

### CSS yang Diterapkan

```scss
// Hanya aktif jika bg_image sudah diisi
@if $bg_image != "" {
  body.category-general {
    background-image: url($bg_image);
    background-size: cover;
    background-attachment: fixed;
    background-position: center;

    // Overlay semi-transparan
    &::before {
      position: fixed; inset: 0;
      background: rgba(0, 0, 0, 0.15);
      z-index: -1;
    }

    // Glassmorphism pada area konten
    .topic-list, .topic-list-item,
    .card-content, .category-list {
      background: rgba(255, 255, 255, 0.85);
      backdrop-filter: blur(4px);
    }
  }
}
```

### Kompatibilitas Browser

| Browser | Background Image | Glassmorphism |
|---|---|---|
| Chrome 76+ | Didukung | Didukung |
| Firefox 103+ | Didukung | Didukung |
| Safari 14+ | Didukung | Didukung (`-webkit-`) |
| Edge 79+ | Didukung | Didukung |

---

## Lisensi

Dikembangkan untuk kebutuhan internal komunitas **Gasing Circle**.
