# PERTEMUAN 3: CSS Framework - Bootstrap 5 vs Tailwind CSS 🚀

Di pertemuan ini, kita akan membandingkan dua CSS framework paling populer: Bootstrap 5 yang berbasis komponen dan Tailwind CSS yang berbasis utility-first. Anda akan belajar filosofi, kelebihan, dan kapan waktu yang tepat untuk menggunakan masing-masing framework.

## 📂 Daftar Materi

Berikut adalah file-file yang akan kita pelajari di pertemuan ini:

### 🅱️ Bootstrap 5 (Component-First)
1.  `01-bootstrap-cdn.html` - Cara memuat Bootstrap dan pengenalan dasar.
2.  `02-grid-system.html` - Memahami sistem grid 12 kolom Bootstrap.
3.  `03-bootstrap-components.html` - Bekerja dengan komponen siap pakai (Tombol, Card, Navbar).
4.  `04-bootstrap-utilities.html` - Menggunakan utility class Bootstrap untuk kustomisasi cepat.
5.  `studi-kasus-bootstrap.html` - **Studi Kasus**: Membangun halaman profil lengkap dengan Bootstrap.

### 🍃 Tailwind CSS (Utility-First)
1.  `05-tailwind-cdn.html` - Pengenalan filosofi utility-first dan setup via CDN.
2.  `06-tailwind-grid.html` - Membangun layout dengan Grid dan Flexbox di Tailwind.
3.  `07-tailwind-components-utilities.html` - Merakit komponen (Card, Form) dari utility classes.
4.  `studi-kasus-tailwind.html` - **Studi Kasus**: Membangun halaman profil yang sama dengan Tailwind CSS.

---

## 🏗️ **Filosofi Bootstrap: Standarisasi dan Efisiensi**

Bootstrap 5 mengusung filosofi **Mobile First** dan **Progressive Enhancement**. Mulai dari desain untuk perangkat kecil terlebih dahulu, kemudian tingkatkan fiturnya untuk perangkat yang lebih besar. Ini memastikan bahwa aplikasi web Anda selalu dapat diakses, cepat, dan responsif.

### **Mobile First**

- **Definisi**: Mendesain untuk layar kecil terlebih dahulu, kemudian memperluas ke layar yang lebih besar.
- **Manfaat**: 
  - Kinerja lebih baik di perangkat mobile.
  - Pengalaman pengguna yang konsisten.

### **Progressive Enhancement**

- **Definisi**: Memulai dengan fitur dasar yang berfungsi di semua perangkat, kemudian menambahkan fitur lanjutan.
- **Manfaat**:
  - Semua pengguna dapat mengakses konten dasar.
  - Pengguna dengan perangkat dan browser modern mendapatkan pengalaman terbaik.

## 📦 **Struktur Dasar Proyek Bootstrap**

```
/my-bootstrap-project
├── index.html
├── about.html
├── contact.html
├── css
│   └── styles.css
├── js
│   └── scripts.js
└── img
    └── logo.png
```

### **index.html - Halaman Utama**

```html
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Halaman Utama</title>
    <!-- Bootstrap CSS -->
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />
    <!-- Custom CSS -->
    <link rel="stylesheet" href="css/styles.css" />
  </head>
  <body>
    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container">
        <a class="navbar-brand" href="#">My Website</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">About</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Contact</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <header class="bg-primary text-white text-center py-5">
      <div class="container">
        <h1 class="display-4">Selamat Datang di Website Saya</h1>
        <p class="lead">
          Ini adalah contoh website yang dibangun dengan Bootstrap 5.
        </p>
        <a href="#" class="btn btn-light btn-lg">
          <i class="fas fa-download"></i> Unduh CV
        </a>
      </div>
    </header>

    <!-- Bootstrap JavaScript -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
  </body>
</html>
```

### **about.html - Halaman Tentang**

```html
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Tentang Saya</title>
    <!-- Bootstrap CSS -->
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />
    <!-- Custom CSS -->
    <link rel="stylesheet" href="css/styles.css" />
  </head>
  <body>
    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container">
        <a class="navbar-brand" href="#">My Website</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <a class="nav-link" href="index.html">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">About</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Contact</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- About Section -->
    <section class="py-5">
      <div class="container">
        <div class="row">
          <div class="col-lg-6">
            <h2 class="text-primary mb-4">Tentang Saya</h2>
            <p class="lead">
              Nama saya Nazriel Rahman Al'afath, seorang web developer dari Indonesia.
            </p>
            <p>
              Saya memiliki keahlian dalam membangun aplikasi web menggunakan
              teknologi terkini seperti HTML, CSS, JavaScript, dan Bootstrap.
            </p>
            <a href="contact.html" class="btn btn-primary btn-lg mt-3">
              <i class="fas fa-envelope"></i> Hubungi Saya
            </a>
          </div>
          <div class="col-lg-6">
            <img
              src="https://via.placeholder.com/500x300"
              alt="Tentang Saya"
              class="img-fluid rounded-circle shadow"
            />
          </div>
        </div>
      </div>
    </section>

    <!-- Bootstrap JavaScript -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
  </body>
</html>
```

### **contact.html - Halaman Kontak**

```html
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Kontak Saya</title>
    <!-- Bootstrap CSS -->
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />
    <!-- Custom CSS -->
    <link rel="stylesheet" href="css/styles.css" />
  </head>
  <body>
    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container">
        <a class="navbar-brand" href="#">My Website</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <a class="nav-link" href="index.html">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="about.html">About</a>
            </li>
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">Contact</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Contact Section -->
    <section class="py-5">
      <div class="container">
        <h2 class="text-center text-primary mb-4">
          <i class="fas fa-address-book me-2"></i>Kontak Saya
        </h2>
        <div class="row">
          <div class="col-lg-8 mx-auto">
            <div class="card border-0 shadow-lg">
              <div class="card-body p-5">
                <form>
                  <div class="mb-3">
                    <label for="name" class="form-label">Nama Lengkap</label>
                    <input
                      type="text"
                      class="form-control"
                      id="name"
                      placeholder="Masukkan nama lengkap Anda"
                      required
                    />
                  </div>
                  <div class="mb-3">
                    <label for="email" class="form-label">Email</label>
                    <input
                      type="email"
                      class="form-control"
                      id="email"
                      placeholder="Masukkan alamat email Anda"
                      required
                    />
                  </div>
                  <div class="mb-3">
                    <label for="message" class="form-label">Pesan</label>
                    <textarea
                      class="form-control"
                      id="message"
                      rows="4"
                      placeholder="Tulis pesan Anda di sini"
                      required
                    ></textarea>
                  </div>
                  <button type="submit" class="btn btn-primary btn-lg w-100">
                    <i class="fas fa-paper-plane"></i> Kirim Pesan
                  </button>
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Bootstrap JavaScript -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
  </body>
</html>
```

## 🎯 **Teori Framework vs Custom CSS**

### **Mengapa Framework Diperlukan?**

**Analogi: Memasak vs Restoran Cepat Saji**

```
Custom CSS = Master Chef (kontrol penuh, waktu lama)
├── Kelebihan: Fleksibilitas tak terbatas
├── Kekurangan: Waktu development lama
└── Use Case: Project unik dengan requirement khusus

Bootstrap = Chef Terlatih dengan SOP (standar, cepat)
├── Kelebihan: Konsistensi, speed, best practices
├── Kekurangan: Limited customization
└── Use Case: Business application, prototyping
```

## 📐 **Grid System - Fondasi Layout Modern**

### **Teori 12-Column Grid System**

**Analogi: Sistem Koordinat Kota**

```
Container = Kota (max-width boundaries)
Row = Jalan horizontal (flex container)
Column = Blok bangunan (flex items)
Gutter = Jarak antar bangunan (padding)
```

### **Mathematical Foundation**

```css
/* Bootstrap Grid Mathematical Concept */
.container {
  max-width: 1200px; /* City boundary */
  margin: 0 auto; /* Center the city */
}

.row {
  display: flex; /* Street layout system */
  flex-wrap: wrap; /* Allow building overflow */
  margin: 0 -15px; /* Negative margin for gutters */
}

.col-6 {
  flex: 0 0 50%; /* 6/12 = 50% width */
  max-width: 50%;
  padding: 0 15px; /* Building setback (gutter) */
}
```

### **Responsive Breakpoints - Design untuk Semua Device**

**Analogi: Bangunan yang Bisa Berubah Bentuk**

```scss
// Bootstrap Breakpoint Theory
$breakpoints: (
  xs: 0px,
  // Phone portrait
  sm: 576px,
  // Phone landscape
  md: 768px,
  // Tablet portrait
  lg: 992px,
  // Tablet landscape / Small desktop
  xl: 1200px,
  // Desktop
  xxl: 1400px // Large desktop,
);
```

## 🎨 **Component System - Modular Design**

### **Atomic Design Philosophy dalam Bootstrap**

```
Atoms (Basic elements)
├── Buttons (.btn)
├── Input fields (.form-control)
└── Typography (.h1, .text-primary)

Molecules (Simple combinations)
├── Input groups (.input-group)
├── Button groups (.btn-group)
└── Badges (.badge)

Organisms (Complex components)
├── Navigation bars (.navbar)
├── Cards (.card)
└── Modals (.modal)
```

### **Implementasi Praktis: Profil Mahasiswa**

```html
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Profil Nazriel Rahman Al'afath</title>
    <!-- Bootstrap CSS CDN -->
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />
    <link
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css"
      rel="stylesheet"
    />
  </head>
  <body class="bg-light">
    <!-- Navigation -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
      <div class="container">
        <a class="navbar-brand fw-bold" href="#">
          <i class="fas fa-user-graduate me-2"></i>
          Nazriel Rahman Al'afath
        </a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <a class="nav-link active" href="#profile">Profil</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#education">Pendidikan</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#skills">Keahlian</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#contact">Kontak</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Main Content -->
    <div class="container my-5">
      <!-- Profile Header -->
      <div class="row justify-content-center">
        <div class="col-lg-8">
          <div class="card shadow-lg border-0 rounded-3">
            <div class="card-body p-5 text-center">
              <img
                src="https://via.placeholder.com/150"
                alt="Nazriel Rahman Al'afath"
                class="rounded-circle mb-4 border border-primary border-3"
                style="width: 150px; height: 150px; object-fit: cover;"
              />
              <h1 class="card-title text-primary mb-3">
                Nazriel Rahman Al'afath
              </h1>
              <p class="text-muted fs-5 mb-4">
                <i class="fas fa-id-card me-2"></i>NIM: 2025001001
              </p>
              <p class="text-muted fs-5 mb-4">
                <i class="fas fa-university me-2"></i>Teknik Informatika
              </p>
              <div class="d-flex justify-content-center gap-3">
                <a href="#contact" class="btn btn-primary btn-lg">
                  <i class="fas fa-envelope me-2"></i>Hubungi Saya
                </a>
                <a href="#" class="btn btn-outline-primary btn-lg">
                  <i class="fas fa-download me-2"></i>Download CV
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Skills Section -->
      <div class="row mt-5">
        <div class="col-12">
          <h2 class="text-center text-primary mb-5">
            <i class="fas fa-code me-2"></i>Keahlian Teknis
          </h2>
        </div>

        <!-- Programming Languages -->
        <div class="col-md-4 mb-4">
          <div class="card h-100 border-0 shadow-sm">
            <div class="card-body text-center">
              <div
                class="bg-primary bg-gradient rounded-circle d-inline-flex align-items-center justify-content-center mb-3"
                style="width: 60px; height: 60px;"
              >
                <i class="fab fa-js-square text-white fa-2x"></i>
              </div>
              <h5 class="card-title text-primary">Programming</h5>
              <div class="mb-3">
                <span class="badge bg-secondary me-1">JavaScript</span>
                <span class="badge bg-secondary me-1">Python</span>
                <span class="badge bg-secondary me-1">Java</span>
                <span class="badge bg-secondary me-1">C++</span>
              </div>
              <div class="progress mb-2">
                <div class="progress-bar bg-primary" style="width: 85%"></div>
              </div>
              <small class="text-muted">Advanced - 85%</small>
            </div>
          </div>
        </div>

        <!-- Web Development -->
        <div class="col-md-4 mb-4">
          <div class="card h-100 border-0 shadow-sm">
            <div class="card-body text-center">
              <div
                class="bg-success bg-gradient rounded-circle d-inline-flex align-items-center justify-content-center mb-3"
                style="width: 60px; height: 60px;"
              >
                <i class="fas fa-globe text-white fa-2x"></i>
              </div>
              <h5 class="card-title text-success">Web Development</h5>
              <div class="mb-3">
                <span class="badge bg-secondary me-1">HTML5</span>
                <span class="badge bg-secondary me-1">CSS3</span>
                <span class="badge bg-secondary me-1">Bootstrap</span>
                <span class="badge bg-secondary me-1">React</span>
              </div>
              <div class="progress mb-2">
                <div class="progress-bar bg-success" style="width: 90%"></div>
              </div>
              <small class="text-muted">Expert - 90%</small>
            </div>
          </div>
        </div>

        <!-- Database -->
        <div class="col-md-4 mb-4">
          <div class="card h-100 border-0 shadow-sm">
            <div class="card-body text-center">
              <div
                class="bg-warning bg-gradient rounded-circle d-inline-flex align-items-center justify-content-center mb-3"
                style="width: 60px; height: 60px;"
              >
                <i class="fas fa-database text-white fa-2x"></i>
              </div>
              <h5 class="card-title text-warning">Database</h5>
              <div class="mb-3">
                <span class="badge bg-secondary me-1">MySQL</span>
                <span class="badge bg-secondary me-1">PostgreSQL</span>
                <span class="badge bg-secondary me-1">MongoDB</span>
                <span class="badge bg-secondary me-1">Redis</span>
              </div>
              <div class="progress mb-2">
                <div class="progress-bar bg-warning" style="width: 75%"></div>
              </div>
              <small class="text-muted">Intermediate - 75%</small>
            </div>
          </div>
        </div>
      </div>

      <!-- Contact Section -->
      <div class="row mt-5">
        <div class="col-12">
          <h2 class="text-center text-primary mb-5">
            <i class="fas fa-address-book me-2"></i>Informasi Kontak
          </h2>
        </div>
        <div class="col-lg-8 mx-auto">
          <div class="card border-0 shadow-lg">
            <div class="card-body p-5">
              <div class="row">
                <div class="col-md-6 mb-3">
                  <div class="d-flex align-items-center">
                    <div
                      class="bg-primary bg-gradient rounded-circle d-inline-flex align-items-center justify-content-center me-3"
                      style="width: 50px; height: 50px;"
                    >
                      <i class="fas fa-envelope text-white"></i>
                    </div>
                    <div>
                      <h6 class="mb-1 text-primary">Email</h6>
                      <p class="mb-0 text-muted">nazriel.rahman@email.com</p>
                    </div>
                  </div>
                </div>
                <div class="col-md-6 mb-3">
                  <div class="d-flex align-items-center">
                    <div
                      class="bg-success bg-gradient rounded-circle d-inline-flex align-items-center justify-content-center me-3"
                      style="width: 50px; height: 50px;"
                    >
                      <i class="fas fa-phone text-white"></i>
                    </div>
                    <div>
                      <h6 class="mb-1 text-success">Telepon</h6>
                      <p class="mb-0 text-muted">+62 812-3456-7890</p>
                    </div>
                  </div>
                </div>
                <div class="col-md-6 mb-3">
                  <div class="d-flex align-items-center">
                    <div
                      class="bg-info bg-gradient rounded-circle d-inline-flex align-items-center justify-content-center me-3"
                      style="width: 50px; height: 50px;"
                    >
                      <i class="fab fa-linkedin text-white"></i>
                    </div>
                    <div>
                      <h6 class="mb-1 text-info">LinkedIn</h6>
                      <p class="mb-0 text-muted">
                        linkedin.com/in/nazriel-rahman
                      </p>
                    </div>
                  </div>
                </div>
                <div class="col-md-6 mb-3">
                  <div class="d-flex align-items-center">
                    <div
                      class="bg-dark bg-gradient rounded-circle d-inline-flex align-items-center justify-content-center me-3"
                      style="width: 50px; height: 50px;"
                    >
                      <i class="fab fa-github text-white"></i>
                    </div>
                    <div>
                      <h6 class="mb-1 text-dark">GitHub</h6>
                      <p class="mb-0 text-muted">github.com/nazriel-rahman</p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Footer -->
    <footer class="bg-dark text-white py-4 mt-5">
      <div class="container text-center">
        <p class="mb-0">
          &copy; 2025 Nazriel Rahman Al'afath.
          <span class="text-muted">Dibuat dengan</span>
          <i class="fas fa-heart text-danger"></i>
          <span class="text-muted">dan Bootstrap 5</span>
        </p>
      </div>
    </footer>

    <!-- Bootstrap JavaScript -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
  </body>
</html>
```

## 🔧 **Utility Classes - Atomic CSS Philosophy**

### **Spacing System - Mathematical Progression**

```css
/* Bootstrap Spacing Scale (rem-based) */
.m-0 {
  margin: 0;
} /* 0rem */
.m-1 {
  margin: 0.25rem;
} /* 4px */
.m-2 {
  margin: 0.5rem;
} /* 8px */
.m-3 {
  margin: 1rem;
} /* 16px */
.m-4 {
  margin: 1.5rem;
} /* 24px */
.m-5 {
  margin: 3rem;
} /* 48px */

/* Directional spacing */
.mt-3 {
  margin-top: 1rem;
}
.me-3 {
  margin-end: 1rem;
} /* margin-right in LTR */
.mb-3 {
  margin-bottom: 1rem;
}
.ms-3 {
  margin-start: 1rem;
} /* margin-left in LTR */
```

### **Flexbox Utilities - Layout Control**

```html
<!-- Flex Container -->
<div class="d-flex justify-content-between align-items-center">
  <div>Logo</div>
  <

```html
<!-- Flexbox Example -->
<div class="flex justify-between items-center p-4 bg-blue-500 text-white">
  <div class="text-xl font-bold">Logo</div>
  <nav>
    <a href="#" class="mx-2 hover:text-blue-200">Home</a>
    <a href="#" class="mx-2 hover:text-blue-200">About</a>
  </nav>
  <button class="bg-white text-blue-500 px-4 py-2 rounded-full">Login</button>
</div>

<!-- Grid Example (2 columns on medium screens, 3 on large) -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 p-4">
  <div class="col-span-1 bg-gray-100 p-4 rounded shadow">Card 1</div>
  <div class="col-span-1 bg-gray-100 p-4 rounded shadow">Card 2</div>
  <div class="col-span-1 bg-gray-100 p-4 rounded shadow">Card 3</div>
</div>
```

### **Responsive Breakpoints - Konfigurasi Default Tailwind**

**Analogi: Pakaian yang Berubah Ukuran Otomatis**

```javascript
// Tailwind CSS Default Breakpoints
module.exports = {
  theme: {
    extend: {
      screens: {
        'sm': '640px',  // Small screens, default
        'md': '768px',  // Medium screens
        'lg': '1024px', // Large screens
        'xl': '1280px', // Extra large screens
        '2xl': '1536px',// 2 Extra large screens
      }
    }
  }
}
```

## 🎨 **Utility Classes - Membangun Desain dari Nol**

### **Atomic CSS Philosophy dalam Tailwind**

```
Utility Classes (Setiap kelas = satu properti CSS)
├── Spacing: `m-4`, `px-2`, `py-8`
├── Typography: `text-xl`, `font-bold`, `text-blue-500`
├── Backgrounds: `bg-red-500`, `bg-gradient-to-r`
├── Borders: `border`, `border-gray-300`, `rounded-lg`
├── Flexbox: `flex`, `justify-center`, `items-end`
└── Grid: `grid`, `grid-cols-4`, `gap-4`
```

### **Implementasi Praktis: Card dengan Tailwind**

```html
<!-- Card dengan Tailwind CSS -->
<div class="max-w-sm mx-auto bg-white rounded-xl shadow-md overflow-hidden md:max-w-2xl my-4">
  <div class="md:flex">
    <div class="md:flex-shrink-0">
      <img class="h-48 w-full object-cover md:w-48" src="https://via.placeholder.com/192x192" alt="Man looking at item" />
    </div>
    <div class="p-8">
      <div class="uppercase tracking-wide text-sm text-indigo-500 font-semibold">Company Name</div>
      <a href="#" class="block mt-1 text-lg leading-tight font-medium text-black hover:underline">Product Title</a>
      <p class="mt-2 text-gray-500">Finding the right product for your needs is essential. We help you find it.</p>
      <button class="mt-4 bg-indigo-600 text-white px-4 py-2 rounded-md hover:bg-indigo-700">Learn More</button>
    </div>
  </div>
</div>
```

### **Contoh Komponen & Utilities Tailwind CSS**

#### Komponen Button
```html
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
  Button Tailwind
</button>
```

#### Komponen Alert
```html
<div class="bg-green-100 border border-green-400 text-green-700 px-4 py-3 rounded relative" role="alert">
  <strong class="font-bold">Sukses!</strong>
  <span class="block sm:inline">Data berhasil disimpan.</span>
</div>
```

#### Komponen Card Profile
```html
<div class="max-w-xs mx-auto bg-white rounded-xl shadow-lg overflow-hidden my-4">
  <img class="w-full h-32 object-cover" src="https://randomuser.me/api/portraits/men/32.jpg" alt="Profile">
  <div class="p-4">
    <h2 class="text-xl font-semibold text-gray-800">Ariel WebDev</h2>
    <p class="text-gray-600">Web Developer & Educator</p>
    <button class="mt-3 w-full bg-blue-500 text-white py-2 rounded hover:bg-blue-600">Follow</button>
  </div>
</div>
```

#### Utilities Tailwind CSS
```html
<!-- Spacing & Layout -->
<div class="p-4 m-2 bg-gray-100">Padding 4, Margin 2</div>

<!-- Typography -->
<h1 class="text-3xl font-bold underline text-blue-600">Judul Besar</h1>

<!-- Flexbox & Grid -->
<div class="flex justify-between items-center">
  <span>Left</span>
  <span>Right</span>
</div>
<div class="grid grid-cols-3 gap-2">
  <div class="bg-red-200">1</div>
  <div class="bg-green-200">2</div>
  <div class="bg-blue-200">3</div>
</div>
```
## 💡 **Best Practices dan Common Patterns di Tailwind**

### **Responsive Design dengan Utility Classes**

```html
<!-- Responsive Text Alignment -->
<h1 class="text-center md:text-left lg:text-right">
  Teks ini akan center di mobile, kiri di medium, kanan di large
</h1>

<!-- Responsive Spacing -->
<div class="p-2 md:p-4 lg:p-8">
  Padding akan berubah sesuai ukuran layar
</div>

<!-- Responsive Display -->
<div class="hidden md:block">
  Div ini hanya akan terlihat di layar medium ke atas
</div>
```

### **Customization dan Konfigurasi**

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        'custom-blue': '#243c5a',
        'custom-purple': '#7e5bef',
      },
      fontFamily: {
        'sans': ['Inter', 'sans-serif'],
      }
    },
  },
  variants: {
    extend: {},
  },
  plugins: [],
}
```

## 🌟 **Kesimpulan Perbandingan: Bootstrap vs Tailwind CSS**

| Fitur / Aspek        | Bootstrap                               | Tailwind CSS                                  |
| :------------------- | :-------------------------------------- | :-------------------------------------------- |
| **Filosofi**         | Component-based, siap pakai             | Utility-first, bangun dari nol                |
| **Ukuran File CSS**  | Lebih besar (banyak komponen tidak terpakai) | Lebih kecil (hanya utility yang digunakan)    |
| **Kustomisasi**      | Terbatas, override CSS, SASS            | Sangat fleksibel, konfigurasi `tailwind.config.js` |
| **Kecepatan Dev**    | Cepat untuk desain standar              | Cepat setelah terbiasa dengan utility         |
| **Desain Unik**      | Cenderung seragam                       | Sangat unik, sesuai keinginan                 |
| **Kurva Pembelajaran** | Rendah (langsung pakai komponen)        | Sedang (perlu hafal utility classes)          |
| **Markup HTML**      | Lebih bersih (sedikit kelas)            | Lebih "ramai" (banyak kelas utility)          |
| **Best Use Case**    | Prototyping, aplikasi bisnis, admin panel | Desain kustom, design system, proyek skala besar |

**Pilihan Terbaik**:

- **Bootstrap**: Jika Anda ingin membangun sesuatu dengan cepat, tidak keberatan dengan tampilan standar, atau membutuhkan banyak komponen interaktif out-of-the-box.
- **Tailwind CSS**: Jika Anda menginginkan kontrol penuh atas desain, membangun design system kustom, atau ingin mengoptimalkan ukuran file CSS sekecil mungkin.

Keduanya adalah alat yang hebat, pilihan tergantung pada kebutuhan proyek dan preferensi tim Anda! 🎨🚀
