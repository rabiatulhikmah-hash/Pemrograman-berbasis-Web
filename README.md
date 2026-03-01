# Pemrograman-berbasis-Web
# Nama : Rabiatul Hikmah
# Nim : 2409116049
------------------------
# 🌸 Personal Portfolio Website
Project ini dibuat sebagai pemenuhan tugas Praktikum Mini Project 1. Website yang dikembangkan merupakan portfolio pribadi berbasis web yang menampilkan informasi profil, pengalaman, keterampilan, dan sertifikat.

Pengembangan dilakukan menggunakan HTML, CSS, Bootstrap 5, dan Vue JS (CDN) untuk menerapkan konsep dasar struktur halaman, styling, komponen responsif, serta data binding dinamis.


## 📁 Struktur File

```
portfolio/
│
├── index.html        # Halaman utama website
├── style.css         # File styling custom
├── README.md         # Dokumentasi proyek
├── img/
│   └── rabi.jpg
└── certificates/
    ├── ASLEB.pdf
    ├── inforsa.png
    └── kepanitiaan.pdf
```

---

## 🚀 Teknologi yang Digunakan

| Teknologi | Keterangan |
|-----------|-----------|
| HTML5 | Struktur dan konten halaman web |
| CSS3 | Styling custom dan CSS Variables |
| Bootstrap 5.3 | Grid system, Navbar, Card, Progress Bar, Utilities |
| Bootstrap Icons 1.11 | Ikon pada card sertifikat dan timeline |
| Vue.js 3 | Render data dinamis ke tampilan HTML |

---

## 🖥️ Tampilan & Penjelasan Setiap Section

---

### 1. Navbar
<img width="1900" height="65" alt="image" src="https://github.com/user-attachments/assets/8466371e-3b33-46a9-a681-ab09baf7ea70" />

**Tampilan:** Navigasi fixed di bagian atas halaman dengan efek blur transparan. Berisi logo "RH" di kiri dan 3 link navigasi di kanan. Pada tampilan mobile, menu collapsed menjadi tombol hamburger.

**Penjelasan Code:**

```html
<nav class="navbar navbar-expand-lg fixed-top">
  <div class="container">
    <a class="navbar-brand" href="#">RH</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item"><a class="nav-link" href="#home">Home</a></li>
        <li class="nav-item"><a class="nav-link" href="#about">About</a></li>
        <li class="nav-item"><a class="nav-link" href="#certificates">Certificates</a></li>
      </ul>
    </div>
  </div>
</nav>
```

- `fixed-top` → navbar tetap di atas saat halaman di-scroll
- `navbar-expand-lg` → menu horizontal di layar besar, hamburger di layar kecil
- `data-bs-toggle="collapse"` → mengaktifkan efek buka/tutup menu di mobile
- `ms-auto` → mendorong menu ke sisi kanan
- CSS: efek kaca transparan diatur via `backdrop-filter: blur(8px)`

---

### 2. Home (Hero Section)
<img width="1898" height="719" alt="image" src="https://github.com/user-attachments/assets/1639aee6-084f-4b7c-8839-d625000389d6" />

**Tampilan:** Section penuh layar dengan background gradient pastel pink–mint–lavender. Menampilkan foto profil bulat di kanan, nama, tagline, dan dua tombol navigasi di kiri.

**Penjelasan Code:**

```html
<section id="home" class="hero-section">
  <div class="container">
    <div class="row align-items-center">
      <div class="col-lg-7">
        <p class="greeting">Hello, I'm</p>
        <h1 class="hero-name">{{ profile.name }}</h1>
        <p class="hero-tagline">{{ profile.tagline }}</p>
        <a href="#about" class="btn btn-dark me-2">About Me</a>
        <a href="#certificates" class="btn btn-outline-dark">Certificates</a>
      </div>
      <div class="col-lg-5 text-center">
        <img :src="profile.image" class="profile-photo" alt="Profile Photo">
      </div>
    </div>
  </div>
</section>
```

- `.hero-section` → background gradient pastel via `linear-gradient` di CSS
- `{{ profile.name }}` → sintaks Vue.js untuk menampilkan data secara dinamis
- `:src="profile.image"` → Vue binding untuk atribut `src` gambar
- `.profile-photo` → foto dibuat bulat dengan `border-radius: 50%` dan border putih
- `col-lg-7 / col-lg-5` → layout 2 kolom Bootstrap, otomatis stack di mobile

---

### 3. About Me
<img width="1900" height="841" alt="image" src="https://github.com/user-attachments/assets/07c8ffac-8320-4bf0-9373-c7dfcd522ae2" />

**Tampilan:** Section background pink pucat dengan layout 2 kolom. Kolom kiri berisi deskripsi diri dan timeline pengalaman. Kolom kanan berisi skill dengan progress bar bergradien.

**Penjelasan Code:**

```html
<div class="row g-5">
  <!-- Kiri: About + Experience -->
  <div class="col-lg-6">
    <p v-for="(paragraph, i) in profile.about" :key="i" class="about-text">{{ paragraph }}</p>
    <h3 class="sub-title">Experience</h3>
    <div class="timeline">
      <div class="timeline-item" v-for="(exp, i) in experiences" :key="i">
        <div class="timeline-dot"></div>
        <div class="timeline-content">
          <span class="timeline-year">{{ exp.year }}</span>
          <h5>{{ exp.role }}</h5>
        </div>
      </div>
    </div>
  </div>
  <!-- Kanan: Skills -->
  <div class="col-lg-6">
    <div v-for="skill in skills" :key="skill.name" class="mb-3">
      <div class="d-flex justify-content-between mb-1">
        <span class="skill-label">{{ skill.name }}</span>
        <span class="skill-pct">{{ skill.level }}%</span>
      </div>
      <div class="progress skill-bar">
        <div class="progress-bar" :style="{ width: skill.level + '%' }"></div>
      </div>
    </div>
  </div>
</div>
```

- `v-for` → Vue.js directive untuk looping data array menjadi elemen HTML
- `:style="{ width: skill.level + '%' }"` → Vue binding mengatur lebar progress bar secara dinamis
- `.timeline` → garis vertikal kiri dibuat dengan `border-left: 2px solid var(--pink)`
- `.timeline-dot` → titik bulat di timeline menggunakan `border-radius: 50%`
- `col-lg-6` → dua kolom sejajar di desktop, stack vertikal di mobile

---

### 4. Certificates
<img width="1900" height="533" alt="image" src="https://github.com/user-attachments/assets/376466cd-badd-4cac-8fc6-bbd9c689dbb0" />

**Tampilan:** Section putih dengan grid 3 card sertifikat di tengah. Setiap card memiliki ikon Bootstrap, judul, provider, tahun, dan badge "Completed" berwarna mint. Card bisa diklik untuk membuka file sertifikat.

**Penjelasan Code:**

```html
<div class="row g-4 justify-content-center">
  <div class="col-12 col-sm-6 col-lg-4" v-for="(cert, i) in certificates" :key="i">
    <a :href="cert.link" target="_blank" class="cert-link">
      <div class="cert-card h-100">
        <div class="cert-icon"><i :class="cert.icon"></i></div>
        <h5 class="cert-title">{{ cert.title }}</h5>
        <p class="cert-meta">{{ cert.provider }}</p>
        <p class="cert-meta">{{ cert.year }}</p>
        <span class="cert-badge">{{ cert.status }}</span>
      </div>
    </a>
  </div>
</div>
```

- `justify-content-center` → card berada di tengah halaman
- `col-12 col-sm-6 col-lg-4` → 1 kolom di mobile, 2 di tablet, 3 di desktop
- `:class="cert.icon"` → Vue binding mengatur class ikon Bootstrap Icons secara dinamis
- `:href="cert.link"` → link ke file sertifikat (PDF/gambar), dibuka di tab baru
- `.cert-badge` → label status berwarna mint menggunakan CSS custom

---

### 5. Footer
<img width="1899" height="70" alt="image" src="https://github.com/user-attachments/assets/96ae5ca8-09e5-4efb-af48-d3c6d46e1ee1" />

**Tampilan:** Bar tipis di bagian paling bawah, background gelap dengan teks copyright di tengah.

**Penjelasan Code:**

```html
<footer class="footer">
  <p class="mb-0">© 2026 {{ profile.name }}</p>
</footer>
```

- `{{ profile.name }}` → nama diambil dinamis dari data Vue
- `.footer` → background `var(--text-dark)`, warna teks putih semi-transparan via `rgba`

---

## 🎨 Sistem Warna (CSS Variables)

Seluruh warna dikelola melalui CSS Variables agar konsisten di semua section:

```css
:root {
  --pink:      #FFB3C6;   /* aksen utama, progress bar, timeline */
  --mint:      #B5EAD7;   /* badge sertifikat */
  --yellow:    #FFDAC1;   /* aksen tambahan hero gradient */
  --lavender:  #C7CEEA;   /* year tag, gradient hero */
  --bg-about:  #FFF0F5;   /* background section about */
  --text-dark: #2D2D2D;   /* teks utama, footer, tombol */
  --text-mid:  #5A5A6A;   /* teks sekunder */
}
```

---

