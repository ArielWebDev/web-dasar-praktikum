# PERTEMUAN 1: FONDASI HTML5 - Membangun Rumah Digital 🏗️

## 🧠 **Filosofi dan Teori Fundamental**

### **Analogi: HTML sebagai Kerangka Rumah**

Bayangkan Anda seorang arsitek yang merancang rumah. HTML adalah **kerangka besi** yang menentukan struktur dasar:

- `<html>` = **Pondasi** rumah
- `<head>` = **Ruang teknis** (instalasi listrik, pipa) - tidak terlihat penghuni
- `<body>` = **Ruang hidup** - area yang dilihat dan digunakan penghuni
- `<div>` = **Ruangan-ruangan** dengan fungsi spesifik

### **Teori Komunikasi Digital**

HTML adalah **bahasa komunikasi** antara developer dan browser:

```
Developer → HTML → Browser → Visual Output → User
```

## 📚 **Konsep Teoritis Mendalam**

### **1. Struktur Hierarkis - Pohon Keluarga Digital**

```
<html> (Kakek)
├── <head> (Ayah - data meta)
│   ├── <title> (Cucu - judul)
│   └── <meta> (Cucu - informasi)
└── <body> (Ibu - konten visual)
    ├── <h1> (Cucu - judul utama)
    ├── <p> (Cucu - paragraf)
    └── <div> (Cucu - kontainer)
```

**Mengapa Hierarki Penting?**

- **Inheritansi**: Properti "turun" dari parent ke child
- **Scope**: Setiap elemen memiliki "wilayah kekuasaan"
- **Maintainability**: Struktur yang jelas = mudah diubah

### **2. Semantik vs Presentasi - Perbedaan Mendasar**

**Analogi: Kostum vs Karakter Aktor**

- **HTML = Karakter aktor** (siapa dia, perannya apa)
- **CSS = Kostum aktor** (bagaimana penampilannya)

```html
<!-- ❌ Presentational (Fokus tampilan) -->
<font size="6" color="red">Judul Besar</font>

<!-- ✅ Semantic (Fokus makna) -->
<h1>Judul Besar</h1>
<!-- Browser tahu ini heading utama -->
```

### **3. Teori Heading - Hierarki Informasi**

**Analogi: Struktur Organisasi Perusahaan**

```html
<h1>CEO (Judul Utama)</h1>
<h2>Direktur (Sub-topik)</h2>
<h3>Manager (Detail topik)</h3>
<h4>Supervisor (Sub-detail)</h4>
```

**Dampak SEO dan Accessibility:**

- **Search Engine**: Memahami prioritas konten
- **Screen Reader**: Navigasi cepat untuk tunanetra
- **User**: Scanning informasi lebih mudah

## 🎯 **Implementasi Praktis dengan Teori**

### **Contoh 1: Struktur Website Universitas**

```html
<!DOCTYPE html>
<!-- Deklarasi standar HTML5 -->
<html lang="id">
  <!-- Bahasa Indonesia untuk accessibility -->
  <head>
    <!-- Meta-informasi: Data tentang data -->
    <meta charset="UTF-8" />
    <!-- Set encoding untuk karakter Indonesia -->
    <title>Universitas Nazriel Rahman Al'afath</title>
  </head>
  <body>
    <!-- Konten visual yang dilihat user -->
    <h1>Universitas Nazriel Rahman Al'afath</h1>

    <h2>Fakultas Teknologi Informasi</h2>
    <p>Fakultas terdepan dalam bidang teknologi...</p>

    <h3>Program Studi</h3>
    <ul>
      <li>Teknik Informatika</li>
      <li>Sistem Informasi</li>
      <li>Teknik Komputer</li>
    </ul>

    <h3>Fasilitas</h3>
    <p>Laboratorium dengan teknologi terkini...</p>
  </body>
</html>
```

### **Contoh 2: Profil Mahasiswa dengan Konteks**

```html
<div>
  <!-- Container: Grouping logis -->
  <h2>Profil Mahasiswa</h2>

  <!-- Informasi personal -->
  <p><strong>Nama:</strong> Nazriel Rahman Al'afath</p>
  <p><strong>NIM:</strong> 2025001001</p>
  <p><strong>Program Studi:</strong> Teknik Informatika</p>

  <!-- Foto profil dengan accessibility -->
  <img
    src="foto-nazriel.jpg"
    alt="Foto profil Nazriel Rahman Al'afath, mahasiswa Teknik Informatika"
  />

  <!-- Navigasi ke halaman lain -->
  <p>Hubungi saya:</p>
  <ul>
    <li><a href="mailto:nazriel@example.com">Email</a></li>
    <li><a href="https://linkedin.com/in/nazriel">LinkedIn</a></li>
    <li><a href="tel:+6281234567890">Telepon</a></li>
  </ul>
</div>
```

## 🔬 **Analisis Teknis**

### **1. Box Model - Konsep Ruang Digital**

Setiap elemen HTML adalah "kotak" dengan properti:

```
Content (Isi) → Padding (Bantalan) → Border (Perbatasan) → Margin (Jarak)
```

**Analogi: Rumah dalam Kompleks**

- **Content** = Ruang dalam rumah
- **Padding** = Halaman rumah
- **Border** = Pagar rumah
- **Margin** = Jarak antar rumah

### **2. Document Object Model (DOM) - Pohon Kehidupan**

Browser mengubah HTML menjadi **struktur pohon** di memory:

```
Document
└── html
    ├── head
    │   └── title
    └── body
        ├── h1
        ├── p
        └── div
            └── img
```

**Mengapa DOM Penting?**

- **JavaScript** memanipulasi DOM untuk interaktivitas
- **CSS** menggunakan DOM untuk styling
- **Browser** merender berdasarkan DOM

### **3. Accessibility - Desain Universal**

**Prinsip POUR:**

- **Perceivable**: Dapat dipersepsi (alt text untuk gambar)
- **Operable**: Dapat dioperasikan (navigasi keyboard)
- **Understandable**: Dapat dipahami (bahasa yang jelas)
- **Robust**: Tangguh (kompatibel dengan assistive technology)

```html
<!-- Contoh implementasi accessibility -->
<img
  src="grafik-statistik.png"
  alt="Grafik menunjukkan kenaikan pengguna 25% tahun 2025"
/>

<a href="download.pdf" title="Download laporan tahunan (PDF, 2MB)">
  Download Laporan
</a>
```

## 💡 **Best Practices dan Filosofi**

### **1. Progressive Enhancement - Lapisan Perkembangan**

```
Lapisan 1: HTML (Konten) - Berfungsi di semua browser
Lapisan 2: CSS (Presentasi) - Enhanced visual
Lapisan 3: JavaScript (Interaktivitas) - Dynamic behavior
```

### **2. Separation of Concerns - Pembagian Tanggung Jawab**

- **HTML**: WHAT (Apa kontennya?)
- **CSS**: HOW (Bagaimana tampilannya?)
- **JavaScript**: WHEN/WHY (Kapan dan mengapa berubah?)

### **3. Content-First Approach**

"Mulailah dengan konten yang bermakna, bukan desain yang cantik"

```html
<!-- Pertama: Buat struktur konten yang logis -->
<h1>Judul</h1>
<p>Penjelasan</p>
<ul>
  <li>Poin 1</li>
  <li>Poin 2</li>
</ul>

<!-- Kemudian: Tambahkan styling dan interaktivitas -->
```

## 🎓 **Refleksi dan Evaluasi**

### **Pertanyaan Reflektif:**

1. Mengapa `<h1>` lebih baik dari `<p style="font-size:large">`?
2. Bagaimana struktur HTML mempengaruhi SEO?
3. Apa perbedaan antara `<div>` dan semantic elements?

### **Analogi Kehidupan Sehari-hari:**

**HTML seperti membuat outline essay:**

- Judul utama (H1)
- Sub-topik (H2)
- Detail (H3)
- Paragraf penjelasan (P)
- Daftar poin (UL/LI)

**Kesimpulan Filosofis:**
"HTML yang baik adalah HTML yang dapat 'bercerita' sendiri tentang struktur dan makna kontennya, bahkan tanpa styling visual."

## 🚀 **Langkah Selanjutnya**

Dengan memahami fondasi HTML yang solid, Anda siap untuk:

1. **CSS** - Memberikan "pakaian" pada struktur HTML
2. **JavaScript** - Memberikan "kehidupan" pada halaman web
3. **Frameworks** - Membangun aplikasi web yang kompleks

**Ingat**: Seperti membangun rumah, fondasi yang kuat menentukan kualitas seluruh bangunan! 🏠
