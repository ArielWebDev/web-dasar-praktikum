# PERTEMUAN 2: FONDASI CSS3 - Seni Visual Web 🎨

## 🎭 **Filosofi CSS: Dari Kerangka ke Karya Seni**

Jika HTML adalah **kerangka rumah**, maka CSS adalah **interior designer** yang mengubah ruang kosong menjadi ruang yang indah dan fungsional. CSS (Cascading Style Sheets) adalah bahasa yang mengontrol **presentasi visual** dari struktur HTML.

### **Analogi: CSS sebagai Fashion Designer**

```
HTML = Model (struktur tubuh)
CSS = Pakaian + Makeup + Aksesori (styling)
User = Audience yang melihat hasil akhir
```

## 📐 **Teori Fundamental CSS**

### **1. Cascade - Air Terjun Aturan**

**Analogi: Sistem Pewarisan Kerajaan**

```css
/* Raja (Universal) */
* { color: black; }

/* Pangeran (Element) */
h1 { color: blue; }

/* Duke (Class) */
.special { color: red; }

/* Emperor (ID) */
#unique { color: green; }

/* Dekrit Langsung (Inline) */
style="color: purple"
```

**Urutan Prioritas (Specificity):**

1. **Inline styles** (1000 points) - Dekrit langsung
2. **IDs** (100 points) - Identitas unik
3. **Classes** (10 points) - Kelompok
4. **Elements** (1 point) - Umum

### **2. Box Model - Anatomi Ruang Digital**

**Analogi: Lukisan dalam Bingkai**

```css
.kotak {
  content: "Lukisan"; /* Kanvas lukisan */
  padding: 20px; /* Matting/passepartout */
  border: 5px solid gold; /* Bingkai */
  margin: 10px; /* Jarak ke dinding */
}
```

### **3. Selector - GPS untuk Elemen**

```css
/* Element selector - semua h1 */
h1 {
  color: blue;
}

/* Class selector - elemen dengan class="special" */
.special {
  background: yellow;
}

/* ID selector - elemen dengan id="unique" */
#unique {
  font-size: 20px;
}

/* Kombinasi - h1 dengan class special */
h1.special {
  color: red;
}
```

## 🎨 **Implementasi Visual dengan Teori**

### **Contoh 1: Profil Mahasiswa dengan Design System**

```html
<!DOCTYPE html>
<html lang="id">
  <head>
    <link rel="stylesheet" href="style.css" />
    <title>Profil Nazriel Rahman Al'afath</title>
  </head>
  <body>
    <div class="profile-card">
      <img
        src="nazriel.jpg"
        alt="Nazriel Rahman Al'afath"
        class="profile-photo"
      />
      <div class="profile-info">
        <h1 class="student-name">Nazriel Rahman Al'afath</h1>
        <p class="student-id">NIM: 2025001001</p>
        <p class="student-major">Teknik Informatika</p>
      </div>
    </div>
  </body>
</html>
```

```css
/* File: style.css */

/* Reset dan base styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Arial", sans-serif;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Card styling - implementasi box model */
.profile-card {
  background: white;
  padding: 30px; /* Ruang dalam */
  margin: 20px; /* Ruang luar */
  border-radius: 15px; /* Sudut melengkung */
  border: 3px solid #e1e8ed; /* Garis tepi */
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
  text-align: center;
  max-width: 400px;
}

/* Image styling */
.profile-photo {
  width: 150px;
  height: 150px;
  border-radius: 50%; /* Membuat bulat */
  border: 4px solid #667eea;
  margin-bottom: 20px;
  object-fit: cover; /* Crop proporsional */
}

/* Typography hierarchy */
.student-name {
  color: #2c3e50;
  font-size: 1.8em;
  margin-bottom: 10px;
  font-weight: bold;
}

.student-id {
  color: #7f8c8d;
  font-size: 1em;
  font-family: monospace;
  margin-bottom: 5px;
}

.student-major {
  color: #3498db;
  font-size: 1.1em;
  font-weight: 500;
}
```

### **Contoh 2: Layout dengan Float (Teknik Klasik)**

```html
<div class="container">
  <header class="site-header">
    <h1>Website Nazriel Rahman Al'afath</h1>
  </header>

  <nav class="navigation">
    <ul>
      <li><a href="#">Beranda</a></li>
      <li><a href="#">Portfolio</a></li>
      <li><a href="#">Kontak</a></li>
    </ul>
  </nav>

  <main class="content">
    <h2>Konten Utama</h2>
    <p>Ini adalah area konten utama...</p>
  </main>

  <aside class="sidebar">
    <h3>Info Tambahan</h3>
    <p>Sidebar content...</p>
  </aside>

  <footer class="site-footer">
    <p>&copy; 2025 Nazriel Rahman Al'afath</p>
  </footer>
</div>
```

```css
/* Container utama */
.container {
  width: 90%;
  max-width: 1200px;
  margin: 0 auto;
  background: white;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
}

/* Header */
.site-header {
  background: #2c3e50;
  color: white;
  padding: 20px;
  text-align: center;
}

/* Navigation */
.navigation {
  background: #34495e;
  padding: 0;
}

.navigation ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.navigation li {
  float: left; /* Float untuk horizontal */
  width: 33.333%; /* 3 item = 100%/3 */
}

.navigation a {
  display: block;
  padding: 15px;
  color: white;
  text-decoration: none;
  text-align: center;
  border-right: 1px solid #2c3e50;
}

.navigation a:hover {
  background: #2c3e50;
}

/* Clearfix untuk mengatasi float */
.navigation:after {
  content: "";
  display: table;
  clear: both;
}

/* Main content area */
.content {
  float: left;
  width: 70%;
  padding: 20px;
  min-height: 400px;
}

/* Sidebar */
.sidebar {
  float: right;
  width: 30%;
  padding: 20px;
  background: #ecf0f1;
  min-height: 400px;
}

/* Footer */
.site-footer {
  clear: both; /* Clear float */
  background: #2c3e50;
  color: white;
  text-align: center;
  padding: 15px;
}
```

## 🎯 **Color Theory dalam CSS**

### **Psikologi Warna untuk Web**

```css
/* Warna dan maknanya */
.trust {
  color: #3498db;
} /* Biru - kepercayaan, profesional */
.success {
  color: #27ae60;
} /* Hijau - sukses, positif */
.warning {
  color: #f39c12;
} /* Orange - peringatan, energi */
.danger {
  color: #e74c3c;
} /* Merah - bahaya, urgensi */
.info {
  color: #9b59b6;
} /* Ungu - informasi, kreatif */

/* Kombinasi harmonis */
.warm-palette {
  background: linear-gradient(45deg, #ff6b6b, #feca57, #ff9ff3);
}

.cool-palette {
  background: linear-gradient(45deg, #74b9ff, #0ddbff, #fd79a8);
}

.monochrome {
  background: linear-gradient(45deg, #2d3436, #636e72, #b2bec3);
}
```

### **Accessibility dalam Warna**

```css
/* Kontras yang cukup untuk readability */
.good-contrast {
  background: #2c3e50; /* Dark blue */
  color: #ffffff; /* White - kontras ratio > 7:1 */
}

/* Tidak bergantung hanya pada warna */
.error-message {
  color: #e74c3c; /* Merah untuk error */
  border-left: 4px solid #e74c3c; /* Visual indicator */
  background: #fadbd8; /* Background tint */
  padding: 10px;
}

.error-message::before {
  content: "⚠️ "; /* Icon sebagai indikator tambahan */
}
```

## 📱 **Responsive Foundations**

### **Viewport dan Meta Tag**

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

### **Media Queries - Dasar Responsive**

```css
/* Base styles - Mobile first */
.container {
  width: 100%;
  padding: 15px;
}

.navigation li {
  width: 100%; /* Stack di mobile */
  float: none;
}

/* Tablet */
@media screen and (min-width: 768px) {
  .container {
    width: 90%;
    padding: 20px;
  }

  .navigation li {
    width: 33.333%; /* 3 kolom di tablet */
    float: left;
  }
}

/* Desktop */
@media screen and (min-width: 1024px) {
  .container {
    width: 80%;
    max-width: 1200px;
    padding: 30px;
  }

  .content {
    width: 70%;
  }

  .sidebar {
    width: 30%;
  }
}
```

## 🔧 **CSS Organization - Struktur Kode**

### **CSS Architecture dengan Comments**

```css
/* ==========================================================================
   RESET & BASE STYLES
   ========================================================================== */

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* ==========================================================================
   TYPOGRAPHY
   ========================================================================== */

body {
  font-family: "Arial", sans-serif;
  font-size: 16px;
  line-height: 1.6;
  color: #333;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  margin-bottom: 1em;
  font-weight: 600;
  line-height: 1.2;
}

/* ==========================================================================
   LAYOUT COMPONENTS
   ========================================================================== */

.container {
  width: 90%;
  max-width: 1200px;
  margin: 0 auto;
}

/* ==========================================================================
   NAVIGATION
   ========================================================================== */

.navigation {
  /* Styles here */
}

/* ==========================================================================
   UTILITIES
   ========================================================================== */

.text-center {
  text-align: center;
}
.text-right {
  text-align: right;
}
.hidden {
  display: none;
}
.clearfix:after {
  content: "";
  display: table;
  clear: both;
}
```

## 💡 **Best Practices CSS**

### **1. Naming Conventions**

```css
/* BEM-like naming */
.profile-card {
} /* Block */
.profile-card__header {
} /* Element */
.profile-card--featured {
} /* Modifier */

/* Semantic naming */
.btn-primary {
} /* Function-based */
.text-large {
} /* Property-based */
.student-info {
} /* Content-based */
```

### **2. Performance Optimization**

```css
/* Efficient selectors */
.navigation-link {
} /* Class - fast */
#unique-element {
} /* ID - fast */

/* Avoid overly specific */
/* body div.container ul.navigation li.item a.link { } */ /* Too specific */

/* Use shorthand properties */
.element {
  margin: 10px 15px 20px 25px; /* top right bottom left */
  padding: 10px 20px; /* vertical horizontal */
  background: #fff url(bg.jpg) no-repeat center;
  border: 1px solid #ccc;
}
```

### **3. Maintainable CSS**

```css
/* Use CSS custom properties for consistency */
:root {
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  --font-size-base: 16px;
  --line-height-base: 1.6;
}

.button {
  background: var(--primary-color);
  font-size: var(--font-size-base);
  line-height: var(--line-height-base);
}

/* Avoid magic numbers */
.spacing-medium {
  margin-bottom: 1.5rem;
} /* 24px at 16px base */
.spacing-large {
  margin-bottom: 2rem;
} /* 32px at 16px base */
```

## 🎓 **Analisis dan Refleksi**

### **Pertanyaan Teoritis:**

1. **Mengapa** cascade dalam CSS berguna untuk maintenance?
2. **Bagaimana** box model mempengaruhi layout design?
3. **Kapan** menggunakan float vs positioning?
4. **Mengapa** mobile-first approach direkomendasikan?

### **Analogi Pembelajaran:**

**CSS seperti mempelajari bahasa asing:**

- **Vocabulary** = Properties (color, margin, padding)
- **Grammar** = Selectors dan specificity rules
- **Style** = Design patterns dan best practices
- **Fluency** = Kemampuan mengkombinasikan semuanya dengan natural

### **Real-world Applications:**

1. **E-commerce**: Product cards dengan hover effects
2. **Blog**: Typography hierarchy untuk readability
3. **Portfolio**: Grid layouts untuk showcase
4. **Corporate**: Professional color schemes dan spacing

## 🚀 **Transisi ke Framework**

### **Mengapa Belajar CSS Murni Dulu?**

```css
/* Understanding this... */
.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  background: #007bff;
  color: white;
  cursor: pointer;
}

/* ...helps you understand Bootstrap's... */
/* .btn class internal implementation */
```

### **Persiapan untuk Bootstrap:**

- **Box Model** → Bootstrap grid system
- **Responsive** → Bootstrap breakpoints
- **Components** → Bootstrap pre-built components
- **Utilities** → Bootstrap utility classes

## 🌟 **Kesimpulan Transformatif**

CSS adalah **bahasa visual web** yang mengubah struktur HTML menjadi pengalaman user yang bermakna. Memahami CSS fundamental berarti memahami:

1. **Visual Communication** - Bagaimana design menyampaikan pesan
2. **User Psychology** - Bagaimana user berinteraksi dengan interface
3. **Technical Foundation** - Dasar untuk framework modern
4. **Problem Solving** - Bagaimana mengatasi layout challenges

**Philosophy**: "CSS yang baik adalah CSS yang tidak terlihat - user hanya merasakan pengalaman yang menyenangkan, bukan kompleksitas teknikalnya."

Dengan fondasi CSS yang kuat, Anda siap melangkah ke Bootstrap dan framework modern lainnya! 🎨✨
