# PERTEMUAN 4: JAVASCRIPT DOM - Memberikan Kehidupan pada Web 🧠

## ⚡ **Filosofi JavaScript: Dari Statis ke Dinamis**

Jika HTML adalah **kerangka rumah** dan CSS adalah **interior design**, maka JavaScript adalah **sistem otomasi pintar** yang membuat rumah tersebut hidup, responsif, dan interaktif. JavaScript mengubah halaman web dari dokumen statis menjadi aplikasi yang dapat berinteraksi dengan user.

### **Analogi: JavaScript sebagai Sistem Saraf Digital**

```
HTML = Tulang rangka (struktur)
CSS = Kulit dan penampilan (presentasi)
JavaScript = Sistem saraf (interaktivitas)
DOM = Peta saraf yang menghubungkan semuanya
```

## 🧠 **Teori Document Object Model (DOM)**

### **DOM: Representasi Digital dari HTML**

**Analogi: DOM sebagai Pohon Keluarga**

```javascript
// HTML Structure
<html>
  <head>
    <title>My Page</title>
  </head>
  <body>
    <h1 id="title">Hello World</h1>
    <div class="container">
      <p>Paragraph 1</p>
      <p>Paragraph 2</p>
    </div>
  </body>
</html>

// DOM Tree Representation
document (root)
├── html (element node)
    ├── head (element node)
    │   └── title (element node)
    │       └── "My Page" (text node)
    └── body (element node)
        ├── h1#title (element node)
        │   └── "Hello World" (text node)
        └── div.container (element node)
            ├── p (element node)
            │   └── "Paragraph 1" (text node)
            └── p (element node)
                └── "Paragraph 2" (text node)
```

### **Node Types - Jenis-jenis Elemen DOM**

```javascript
// 1. Element Node (Tag HTML)
const titleElement = document.getElementById('title');
console.log(titleElement.nodeType); // 1

// 2. Text Node (Konten teks)
const textNode = titleElement.firstChild;
console.log(textNode.nodeType); // 3

// 3. Attribute Node (Atribut element)
const idAttribute = titleElement.getAttributeNode('id');
console.log(idAttribute.nodeType); // 2

// 4. Comment Node (Komentar HTML)
<!-- This is a comment -->
console.log(commentNode.nodeType); // 8
```

## 🎯 **DOM Selection - Menemukan Elemen**

### **Analogi: DOM Selection seperti GPS Navigation**

```javascript
// 1. getElementById - GPS dengan koordinat tepat
const titleElement = document.getElementById("student-name");
// Seperti: "Pergi ke alamat dengan kode pos 12345"

// 2. getElementsByClassName - Cari semua rumah di kompleks yang sama
const cardElements = document.getElementsByClassName("student-card");
// Seperti: "Temukan semua rumah di Perumahan Green Hills"

// 3. getElementsByTagName - Cari berdasarkan tipe bangunan
const allParagraphs = document.getElementsByTagName("p");
// Seperti: "Temukan semua toko dalam radius 5km"

// 4. querySelector - GPS dengan deskripsi detail
const firstCard = document.querySelector(".student-card");
// Seperti: "Rumah pertama dengan pagar biru di Jalan Mawar"

// 5. querySelectorAll - Temukan semua yang cocok deskripsi
const allCards = document.querySelectorAll(".student-card");
// Seperti: "Semua rumah dengan pagar biru di kota ini"
```

### **CSS Selectors dalam JavaScript**

```javascript
// Basic selectors
document.querySelector("#student-name"); // ID selector
document.querySelector(".student-info"); // Class selector
document.querySelector("div"); // Element selector

// Advanced selectors
document.querySelector("div.student-card"); // Element + class
document.querySelector("#profile .student-name"); // Descendant selector
document.querySelector('input[type="email"]'); // Attribute selector
document.querySelector("li:first-child"); // Pseudo selector
document.querySelector("p:nth-child(2)"); // Nth-child selector
```

#### Deklarasi Variabel:

```javascript
var nama = "John"; // Function scoped (avoid)
let umur = 25; // Block scoped (recommended)
const PI = 3.14159; // Constant value
```

#### Tipe Data Primitif:

- **String**: `"Hello World"`
- **Number**: `42`, `3.14`
- **Boolean**: `true`, `false`
- **Undefined**: `undefined`
- **Null**: `null`
- **Symbol**: `Symbol("id")`
- **BigInt**: `123n`

#### Tipe Data Non-Primitif:

- **Object**: `{name: "Nazriel Rahman Al'afath", age: 25}`
- **Array**: `[1, 2, 3, 4, 5]`
- **Function**: `function myFunc() {}`

### 3. DOM (Document Object Model)

#### Definisi DOM:

DOM adalah representasi struktur dokumen HTML sebagai tree of objects yang dapat dimanipulasi dengan JavaScript.

#### Struktur DOM Tree:

```
Document
└── html
    ├── head
    │   ├── title
    │   └── meta
    └── body
        ├── h1
        ├── p
        └── div
            ├── span
            └── img
```

#### Mengakses Elemen DOM:

```javascript
// By ID
const element = document.getElementById("myId");

// By Class Name
const elements = document.getElementsByClassName("myClass");

// By Tag Name
const paragraphs = document.getElementsByTagName("p");

// Query Selector (CSS Selector)
const element = document.querySelector("#myId");
const elements = document.querySelectorAll(".myClass");
```

### 4. Manipulasi DOM

#### Mengubah Konten:

```javascript
// Text Content
element.textContent = "New text";

// HTML Content
element.innerHTML = "<strong>Bold text</strong>";

// Attribute
element.setAttribute("src", "image.jpg");
element.getAttribute("src");
```

#### Mengubah Style:

```javascript
// Direct style
element.style.color = "red";
element.style.backgroundColor = "blue";

// CSS Classes
element.classList.add("active");
element.classList.remove("hidden");
element.classList.toggle("visible");
```

#### Membuat dan Menghapus Elemen:

```javascript
// Membuat elemen baru
const newDiv = document.createElement("div");
newDiv.textContent = "Hello World";

// Menambahkan ke DOM
parentElement.appendChild(newDiv);
parentElement.insertBefore(newDiv, referenceElement);

// Menghapus elemen
parentElement.removeChild(childElement);
element.remove(); // Modern way
```

### 5. Event Handling

#### Menambahkan Event Listener:

```javascript
// Method 1: addEventListener (Recommended)
button.addEventListener("click", function () {
  console.log("Button clicked!");
});

// Method 2: Event property
button.onclick = function () {
  console.log("Button clicked!");
};

// Method 3: Inline HTML (Not recommended)
// <button onclick="handleClick()">Click Me</button>
```

#### Event Object:

```javascript
button.addEventListener("click", function (event) {
  event.preventDefault(); // Mencegah default behavior
  event.stopPropagation(); // Mencegah event bubbling
  console.log(event.target); // Element yang memicu event
});
```

### 6. Functions dalam JavaScript

#### Function Declaration:

```javascript
function salam(nama) {
  return "Halo, " + nama + "!";
}
```

#### Function Expression:

```javascript
const salam = function (nama) {
  return "Halo, " + nama + "!";
};
```

#### Arrow Function (ES6):

```javascript
const salam = (nama) => {
  return "Halo, " + nama + "!";
};

// Sintaks pendek
const salam = (nama) => "Halo, " + nama + "!";
```

### 7. Conditional Statements

```javascript
// if-else
if (umur >= 18) {
  console.log("Dewasa");
} else {
  console.log("Anak-anak");
}

// switch
switch (hari) {
  case "Senin":
    console.log("Awal minggu");
    break;
  case "Jumat":
    console.log("Hampir weekend!");
    break;
  default:
    console.log("Hari biasa");
}

// Ternary operator
const status = umur >= 18 ? "Dewasa" : "Anak-anak";
```

### 8. Loops

```javascript
// for loop
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// while loop
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}

// for...of (arrays)
const fruits = ["apple", "banana", "orange"];
for (const fruit of fruits) {
  console.log(fruit);
}

// for...in (objects)
const person = { name: "John", age: 25 };
for (const key in person) {
  console.log(key + ": " + person[key]);
}
```

### 9. Array Methods

```javascript
const numbers = [1, 2, 3, 4, 5];

// forEach - iterate
numbers.forEach((num) => console.log(num));

// map - transform
const doubled = numbers.map((num) => num * 2);

// filter - select
const evens = numbers.filter((num) => num % 2 === 0);

// find - first match
const found = numbers.find((num) => num > 3);

// reduce - combine
const sum = numbers.reduce((total, num) => total + num, 0);
```

### 10. Objects

```javascript
// Object literal
const person = {
  name: "John",
  age: 25,
  greet: function () {
    return "Hello, I'm " + this.name;
  },
};

// Accessing properties
console.log(person.name); // Dot notation
console.log(person["age"]); // Bracket notation

// Adding properties
person.email = "john@email.com";

// Deleting properties
delete person.age;
```

## 🎯 Konsep Penting

### 1. **Scope dan Hoisting**

```javascript
// Global scope
var globalVar = "I'm global";

function myFunction() {
  // Function scope
  var functionVar = "I'm in function";

  if (true) {
    // Block scope (let, const)
    let blockVar = "I'm in block";
    const constVar = "I'm constant";
  }
}
```

### 2. **Event Bubbling dan Capturing**

```javascript
// Event bubbling (default)
child.addEventListener("click", handler);

// Event capturing
child.addEventListener("click", handler, true);

// Stopping propagation
function handler(event) {
  event.stopPropagation();
}
```

### 3. **this Keyword**

```javascript
const obj = {
  name: "John",
  greet: function () {
    console.log(this.name); // "John"
  },
  greetArrow: () => {
    console.log(this.name); // undefined (arrow function)
  },
};
```

## 🔧 Best Practices

### 1. **Naming Conventions**

```javascript
// Variables and functions: camelCase
const userName = "john";
function calculateTotal() {}

// Constants: UPPER_CASE
const MAX_USERS = 100;

// Constructor functions: PascalCase
function UserAccount() {}
```

### 2. **Code Organization**

```javascript
// Use strict mode
"use strict";

// Group related functionality
const utils = {
  formatDate: function (date) {},
  validateEmail: function (email) {},
};

// Use modules (modern approach)
export function myFunction() {}
import { myFunction } from "./utils.js";
```

### 3. **Error Handling**

```javascript
try {
  // Code that might throw error
  const result = riskyOperation();
} catch (error) {
  console.error("Error occurred:", error);
} finally {
  // Cleanup code
  console.log("Cleanup completed");
}
```

### 4. **Performance Tips**

```javascript
// Cache DOM queries
const button = document.getElementById("myButton");

// Use event delegation
document.addEventListener("click", function (event) {
  if (event.target.matches(".button")) {
    // Handle button click
  }
});

// Minimize DOM manipulation
const fragment = document.createDocumentFragment();
// Add multiple elements to fragment
document.body.appendChild(fragment);
```

## 📖 Debugging

### 1. **Console Methods**

```javascript
console.log("Basic logging");
console.error("Error message");
console.warn("Warning message");
console.table(arrayOrObject);
console.time("timer");
console.timeEnd("timer");
```

### 2. **Debugging Techniques**

```javascript
// Breakpoints in code
debugger;

// Type checking
console.log(typeof variable);
console.log(variable instanceof Array);

// Value inspection
console.log("Value:", variable, "Type:", typeof variable);
```

## 🚀 Modern JavaScript (ES6+)

### 1. **Template Literals**

```javascript
const name = "John";
const age = 25;
const message = `Hello, my name is ${name} and I'm ${age} years old.`;
```

### 2. **Destructuring**

```javascript
// Array destructuring
const [first, second] = [1, 2, 3];

// Object destructuring
const { name, age } = { name: "John", age: 25 };
```

### 3. **Default Parameters**

```javascript
function greet(name = "World") {
  return `Hello, ${name}!`;
}
```

### 4. **Spread Operator**

```javascript
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5]; // [1, 2, 3, 4, 5]

const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3 }; // {a: 1, b: 2, c: 3}
```

## 📝 Latihan Praktik

### 1. **Manipulasi DOM Dasar**

- Mengubah text content
- Mengubah HTML content
- Menambah/menghapus CSS classes
- Mengubah style properties

### 2. **Event Handling**

- Click events
- Form events
- Keyboard events
- Mouse events

### 3. **Dynamic Content**

- Membuat elemen baru
- Menambahkan elemen ke DOM
- Menghapus elemen dari DOM
- Mengkloning elemen

### 4. **Interaktivitas**

- Toggle visibility
- Form validation
- Dynamic lists
- Simple calculations

Praktikum ini akan membantu Anda memahami konsep fundamental JavaScript dan DOM manipulation yang menjadi dasar untuk pengembangan web interaktif.
