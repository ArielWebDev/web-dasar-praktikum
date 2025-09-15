# PERTEMUAN 6: JAVASCRIPT DATA MANAGEMENT - Ekosistem Informasi 📊

## 📊 **Filosofi Data: Kehidupan Digital Applications**

Data dalam JavaScript adalah **nyawa aplikasi web**. Seperti darah yang mengalir dalam tubuh manusia, data mengalir melalui aplikasi, membawa informasi vital yang menentukan bagaimana aplikasi berperilaku, tampil, dan berinteraksi dengan user.

### **Analogi: Data sebagai Perpustakaan Digital**

```
Raw Data → Processing → Storage → Retrieval → Presentation
    ↓           ↓          ↓         ↓           ↓
 "Input"   "Validate"  "LocalStorage" "Parse"  "Display"
```

## 🗃️ **Data Storage - Gudang Informasi Browser**

### **1. LocalStorage - Penyimpanan Permanen**

**Analogi: LocalStorage seperti Lemari di Rumah Anda**

```javascript
// LocalStorage: Data bertahan sampai dihapus manual
class LocalStorageManager {
  // Simpan data (seperti menaruh barang di lemari)
  static save(key, data) {
    try {
      const jsonData = JSON.stringify(data);
      localStorage.setItem(key, jsonData);
      console.log(`✅ Data '${key}' berhasil disimpan di LocalStorage`);
      return true;
    } catch (error) {
      console.error("❌ Gagal menyimpan ke LocalStorage:", error);
      return false;
    }
  }

  // Ambil data (seperti mengambil barang dari lemari)
  static load(key, defaultValue = null) {
    try {
      const jsonData = localStorage.getItem(key);
      if (jsonData === null) {
        console.log(`⚠️ Data '${key}' tidak ditemukan, menggunakan default`);
        return defaultValue;
      }
      const data = JSON.parse(jsonData);
      console.log(`✅ Data '${key}' berhasil dimuat dari LocalStorage`);
      return data;
    } catch (error) {
      console.error("❌ Gagal memuat dari LocalStorage:", error);
      return defaultValue;
    }
  }

  // Hapus data
  static remove(key) {
    localStorage.removeItem(key);
    console.log(`🗑️ Data '${key}' berhasil dihapus dari LocalStorage`);
  }

  // Cek apakah data ada
  static exists(key) {
    return localStorage.getItem(key) !== null;
  }

  // Dapatkan semua keys
  static getAllKeys() {
    return Object.keys(localStorage);
  }

  // Bersihkan semua data
  static clear() {
    localStorage.clear();
    console.log("🧹 Semua data LocalStorage berhasil dibersihkan");
  }

  // Dapatkan ukuran storage yang digunakan
  static getStorageSize() {
    let total = 0;
    for (let key in localStorage) {
      if (localStorage.hasOwnProperty(key)) {
        total += localStorage[key].length + key.length;
      }
    }
    return total;
  }
}

// Contoh penggunaan praktis
const studentData = {
  name: "Nazriel Rahman Al'afath",
  nim: "20230001",
  major: "Teknik Informatika",
  semester: 5,
  subjects: ["Web Programming", "Database", "Software Engineering"],
  gpa: 3.85,
};

// Simpan data mahasiswa
LocalStorageManager.save("currentStudent", studentData);

// Simpan preferences
LocalStorageManager.save("userPreferences", {
  theme: "dark",
  language: "indonesia",
  notifications: true,
  autoSave: true,
});

// Load data
const loadedStudent = LocalStorageManager.load("currentStudent");
const preferences = LocalStorageManager.load("userPreferences", {
  theme: "light",
  language: "english",
  notifications: false,
  autoSave: false,
});

console.log("Student Data:", loadedStudent);
console.log("User Preferences:", preferences);
```

### **2. SessionStorage - Penyimpanan Sementara**

**Analogi: SessionStorage seperti Meja Kerja**

```javascript
// SessionStorage: Data hilang saat tab ditutup
class SessionStorageManager {
  static save(key, data) {
    try {
      sessionStorage.setItem(key, JSON.stringify(data));
      console.log(`💾 Data '${key}' disimpan untuk sesi ini`);
      return true;
    } catch (error) {
      console.error("❌ Gagal menyimpan ke SessionStorage:", error);
      return false;
    }
  }

  static load(key, defaultValue = null) {
    try {
      const data = sessionStorage.getItem(key);
      return data ? JSON.parse(data) : defaultValue;
    } catch (error) {
      console.error("❌ Gagal memuat dari SessionStorage:", error);
      return defaultValue;
    }
  }

  static remove(key) {
    sessionStorage.removeItem(key);
    console.log(`🗑️ Data sesi '${key}' berhasil dihapus`);
  }

  static clear() {
    sessionStorage.clear();
    console.log("🧹 Semua data sesi berhasil dibersihkan");
  }
}

// Contoh penggunaan: Form data sementara
const tempFormData = {
  currentStep: 2,
  formData: {
    personalInfo: {
      name: "Nazriel Rahman Al'afath",
      email: "nazriel@email.com",
    },
    academicInfo: { nim: "20230001", semester: 5 },
  },
  startTime: new Date().toISOString(),
};

SessionStorageManager.save("formProgress", tempFormData);
```

### **3. Cookies - Komunikasi dengan Server**

**Analogi: Cookies seperti Tanda Pengenal**

```javascript
class CookieManager {
  // Set cookie dengan options
  static set(name, value, options = {}) {
    const defaults = {
      path: "/",
      expires: null,
      maxAge: null,
      secure: false,
      sameSite: "Lax",
    };

    const config = { ...defaults, ...options };

    let cookieString = `${encodeURIComponent(name)}=${encodeURIComponent(
      value
    )}`;

    if (config.path) cookieString += `; path=${config.path}`;
    if (config.expires)
      cookieString += `; expires=${config.expires.toUTCString()}`;
    if (config.maxAge) cookieString += `; max-age=${config.maxAge}`;
    if (config.secure) cookieString += "; secure";
    cookieString += `; samesite=${config.sameSite}`;

    document.cookie = cookieString;
    console.log(`🍪 Cookie '${name}' berhasil diset`);
  }

  // Get cookie
  static get(name) {
    const cookies = document.cookie.split(";");
    for (let cookie of cookies) {
      const [key, value] = cookie.trim().split("=");
      if (decodeURIComponent(key) === name) {
        return decodeURIComponent(value);
      }
    }
    return null;
  }

  // Remove cookie
  static remove(name, path = "/") {
    this.set(name, "", { expires: new Date(0), path });
    console.log(`🗑️ Cookie '${name}' berhasil dihapus`);
  }

  // Get all cookies
  static getAll() {
    const cookies = {};
    document.cookie.split(";").forEach((cookie) => {
      const [key, value] = cookie.trim().split("=");
      if (key) {
        cookies[decodeURIComponent(key)] = decodeURIComponent(value || "");
      }
    });
    return cookies;
  }
}

// Contoh penggunaan: User authentication
CookieManager.set("userToken", "abc123xyz", {
  maxAge: 24 * 60 * 60, // 24 jam
  secure: true,
  sameSite: "Strict",
});

CookieManager.set(
  "userPreference",
  JSON.stringify({
    language: "indonesia",
    theme: "dark",
  }),
  {
    maxAge: 30 * 24 * 60 * 60, // 30 hari
  }
);
```

## 🔄 **Data Processing - Pengolahan dan Transformasi**

### **1. JSON Operations - Format Data Universal**

**Analogi: JSON seperti Bahasa Esperanto untuk Data**

```javascript
class JSONProcessor {
  // Safe JSON parsing dengan error handling
  static safeParse(jsonString, fallback = null) {
    try {
      return JSON.parse(jsonString);
    } catch (error) {
      console.error("❌ Invalid JSON:", error.message);
      console.log("📝 JSON yang bermasalah:", jsonString);
      return fallback;
    }
  }

  // Safe JSON stringify dengan error handling
  static safeStringify(data, replacer = null, space = 2) {
    try {
      return JSON.stringify(data, replacer, space);
    } catch (error) {
      console.error("❌ Tidak bisa convert ke JSON:", error.message);
      return null;
    }
  }

  // Deep clone object menggunakan JSON
  static deepClone(obj) {
    return this.safeParse(this.safeStringify(obj));
  }

  // Validate JSON structure
  static validateStructure(data, schema) {
    function checkProperty(obj, path, expectedType) {
      const keys = path.split(".");
      let current = obj;

      for (let key of keys) {
        if (current === null || current === undefined) {
          return false;
        }
        current = current[key];
      }

      return typeof current === expectedType;
    }

    for (let path in schema) {
      if (!checkProperty(data, path, schema[path])) {
        console.error(
          `❌ Validation failed: ${path} should be ${schema[path]}`
        );
        return false;
      }
    }

    return true;
  }

  // Pretty print JSON
  static prettyPrint(data) {
    const jsonString = this.safeStringify(data, null, 2);
    console.log("📋 Pretty JSON:");
    console.log(jsonString);
    return jsonString;
  }

  // Flatten nested JSON
  static flatten(obj, prefix = "") {
    const flattened = {};

    for (let key in obj) {
      if (obj.hasOwnProperty(key)) {
        const newKey = prefix ? `${prefix}.${key}` : key;

        if (
          typeof obj[key] === "object" &&
          obj[key] !== null &&
          !Array.isArray(obj[key])
        ) {
          Object.assign(flattened, this.flatten(obj[key], newKey));
        } else {
          flattened[newKey] = obj[key];
        }
      }
    }

    return flattened;
  }
}

// Contoh penggunaan praktis
const complexStudentData = {
  personal: {
    name: "Nazriel Rahman Al'afath",
    contact: {
      email: "nazriel@email.com",
      phone: "081234567890",
      address: {
        street: "Jl. Pendidikan No. 123",
        city: "Jakarta",
        province: "DKI Jakarta",
      },
    },
  },
  academic: {
    nim: "20230001",
    major: "Teknik Informatika",
    courses: [
      { code: "TI101", name: "Web Programming", credits: 3, grade: "A" },
      { code: "TI102", name: "Database Systems", credits: 3, grade: "A-" },
    ],
  },
};

// Validasi struktur data
const studentSchema = {
  "personal.name": "string",
  "personal.contact.email": "string",
  "academic.nim": "string",
  "academic.major": "string",
};

const isValid = JSONProcessor.validateStructure(
  complexStudentData,
  studentSchema
);
console.log("✅ Data structure valid:", isValid);

// Flatten data
const flattenedData = JSONProcessor.flatten(complexStudentData);
console.log("📊 Flattened data:", flattenedData);

// Clone data
const clonedData = JSONProcessor.deepClone(complexStudentData);
console.log("📋 Data berhasil di-clone");
```

### **2. Array Operations - Manipulasi Koleksi Data**

**Analogi: Array seperti Daftar yang Bisa Dimanipulasi**

```javascript
class ArrayProcessor {
  // Filter dengan multiple conditions
  static filterBy(array, conditions) {
    return array.filter((item) => {
      return Object.keys(conditions).every((key) => {
        const condition = conditions[key];
        const value = item[key];

        if (typeof condition === "function") {
          return condition(value);
        } else if (typeof condition === "object" && condition.operator) {
          switch (condition.operator) {
            case ">":
              return value > condition.value;
            case "<":
              return value < condition.value;
            case ">=":
              return value >= condition.value;
            case "<=":
              return value <= condition.value;
            case "!=":
              return value != condition.value;
            case "contains":
              return value
                .toString()
                .toLowerCase()
                .includes(condition.value.toLowerCase());
            default:
              return value === condition.value;
          }
        } else {
          return value === condition;
        }
      });
    });
  }

  // Sort dengan multiple criteria
  static sortBy(array, criteria) {
    return [...array].sort((a, b) => {
      for (let criterion of criteria) {
        const { field, direction = "asc" } = criterion;
        const aVal = a[field];
        const bVal = b[field];

        let result = 0;
        if (aVal < bVal) result = -1;
        else if (aVal > bVal) result = 1;

        if (direction === "desc") result *= -1;

        if (result !== 0) return result;
      }
      return 0;
    });
  }

  // Group by field
  static groupBy(array, field) {
    return array.reduce((groups, item) => {
      const key = item[field];
      if (!groups[key]) {
        groups[key] = [];
      }
      groups[key].push(item);
      return groups;
    }, {});
  }

  // Calculate statistics
  static getStats(array, field) {
    const values = array
      .map((item) => item[field])
      .filter((val) => !isNaN(val));

    if (values.length === 0) return null;

    const sum = values.reduce((a, b) => a + b, 0);
    const avg = sum / values.length;
    const min = Math.min(...values);
    const max = Math.max(...values);

    // Standard deviation
    const variance =
      values.reduce((acc, val) => acc + Math.pow(val - avg, 2), 0) /
      values.length;
    const stdDev = Math.sqrt(variance);

    return { sum, avg, min, max, count: values.length, stdDev };
  }

  // Search dalam array objects
  static search(array, searchTerm, fields) {
    const term = searchTerm.toLowerCase();
    return array.filter((item) => {
      return fields.some((field) => {
        const value = item[field];
        return value && value.toString().toLowerCase().includes(term);
      });
    });
  }

  // Paginate array
  static paginate(array, page, itemsPerPage) {
    const startIndex = (page - 1) * itemsPerPage;
    const endIndex = startIndex + itemsPerPage;

    return {
      data: array.slice(startIndex, endIndex),
      totalItems: array.length,
      totalPages: Math.ceil(array.length / itemsPerPage),
      currentPage: page,
      hasNext: endIndex < array.length,
      hasPrev: page > 1,
    };
  }
}

// Data mahasiswa untuk testing
const studentsData = [
  {
    name: "Nazriel Rahman Al'afath",
    nim: "20230001",
    major: "TI",
    gpa: 3.85,
    semester: 5,
  },
  {
    name: "Siti Nur Aisyah",
    nim: "20230002",
    major: "SI",
    gpa: 3.92,
    semester: 5,
  },
  {
    name: "Ahmad Fauzi Rahman",
    nim: "20230003",
    major: "TI",
    gpa: 3.67,
    semester: 4,
  },
  {
    name: "Dewi Maharani",
    nim: "20230004",
    major: "TK",
    gpa: 3.78,
    semester: 6,
  },
  {
    name: "Budi Santoso",
    nim: "20230005",
    major: "TI",
    gpa: 3.55,
    semester: 5,
  },
];

// Filter mahasiswa TI dengan GPA > 3.7
const excellentTIStudents = ArrayProcessor.filterBy(studentsData, {
  major: "TI",
  gpa: { operator: ">", value: 3.7 },
});
console.log("🎓 Mahasiswa TI dengan GPA > 3.7:", excellentTIStudents);

// Sort berdasarkan GPA desc, lalu nama asc
const sortedStudents = ArrayProcessor.sortBy(studentsData, [
  { field: "gpa", direction: "desc" },
  { field: "name", direction: "asc" },
]);
console.log("📊 Mahasiswa diurutkan berdasarkan GPA dan nama:", sortedStudents);

// Group berdasarkan major
const groupedByMajor = ArrayProcessor.groupBy(studentsData, "major");
console.log("📋 Mahasiswa dikelompokkan berdasarkan jurusan:", groupedByMajor);

// Statistik GPA
const gpaStats = ArrayProcessor.getStats(studentsData, "gpa");
console.log("📈 Statistik GPA:", gpaStats);

// Search mahasiswa
const searchResults = ArrayProcessor.search(studentsData, "rahman", ["name"]);
console.log('🔍 Hasil pencarian "rahman":', searchResults);

// Pagination
const page1 = ArrayProcessor.paginate(studentsData, 1, 2);
console.log("📄 Halaman 1 (2 items per page):", page1);
```

## 🌟 **Kesimpulan Filosofis**

Data Management adalah **fondasi dari semua aplikasi modern**. Memahami data berarti memahami:

1. **Information Architecture** - Bagaimana informasi disusun dan diakses
2. **User Experience** - Bagaimana data mempengaruhi interaksi user
3. **Application Performance** - Bagaimana pengelolaan data mempengaruhi kecepatan
4. **Business Logic** - Bagaimana data mendukung tujuan aplikasi

**Philosophy**: "Data is not just storage—it's the memory, personality, and intelligence of your application."

Data mengajarkan kita bahwa **information is power**, dan mengelola informasi dengan baik adalah kunci sukses dalam pengembangan aplikasi yang meaningful dan impactful. 📊✨

---

## 📁 **File Praktikum dalam Folder**

1. `01-local-storage.html` - Penyimpanan data permanen dengan contoh Indonesia
2. `02-todo-app.html` - Aplikasi To-Do dengan data persistence dan UI Indonesia
3. `03-form-data.html` - Pengolahan data form dengan validasi Indonesia
4. `04-json-operations.html` - Operasi JSON dan data transformation
5. `05-student-crud.html` - CRUD mahasiswa dengan nama Indonesia
6. `studi-kasus-student-management.html` - Sistem manajemen mahasiswa lengkap

## 🎯 **Tujuan Pembelajaran**

Memahami dan mengimplementasikan data management dalam JavaScript, termasuk storage, processing, validation, dan architecture patterns untuk membangun aplikasi yang robust dan user-friendly.
Storage.clear() // Remove all items
Storage.key(index) // Get key at index
Storage.length // Number of items

````

#### Storage Events:
```javascript
// Listen for storage changes (works across tabs)
window.addEventListener('storage', function(event) {
    console.log('Storage changed:');
    console.log('Key:', event.key);
    console.log('Old Value:', event.oldValue);
    console.log('New Value:', event.newValue);
    console.log('URL:', event.url);
    console.log('Storage Area:', event.storageArea);
});
````

#### Best Practices:

```javascript
// Always wrap in try-catch (storage might be disabled)
function safeSetItem(key, value) {
  try {
    localStorage.setItem(key, value);
    return true;
  } catch (error) {
    console.error("Storage failed:", error);
    return false;
  }
}

// Check storage availability
function isStorageAvailable(type) {
  try {
    const storage = window[type];
    const test = "__storage_test__";
    storage.setItem(test, test);
    storage.removeItem(test);
    return true;
  } catch (error) {
    return false;
  }
}
```

### 3. JSON (JavaScript Object Notation)

#### JSON Syntax Rules:

- Data is in name/value pairs
- Data is separated by commas
- Objects are enclosed in curly braces {}
- Arrays are enclosed in square brackets []
- Strings must be in double quotes
- No functions, comments, or undefined values

#### JSON Methods:

```javascript
// Serialization (Object to JSON string)
const obj = {
  name: "Nazriel Rahman Al'afath",
  age: 30,
  hobbies: ["reading", "coding"],
};
const jsonString = JSON.stringify(obj);
// Result: '{"name":"Nazriel Rahman Al\'afath","age":30,"hobbies":["reading","coding"]}'

// Deserialization (JSON string to Object)
const parsedObj = JSON.parse(jsonString);
// Result: { name: "Nazriel Rahman Al'afath", age: 30, hobbies: ["reading", "coding"] }

// Advanced JSON.stringify options
JSON.stringify(obj, null, 2); // Pretty print with 2-space indentation
JSON.stringify(obj, ["name"]); // Only include 'name' property
JSON.stringify(obj, (key, value) => {
  return key === "age" ? undefined : value; // Exclude 'age' property
});
```

#### JSON Error Handling:

```javascript
function safeJsonParse(jsonString, defaultValue = null) {
  try {
    return JSON.parse(jsonString);
  } catch (error) {
    console.error("JSON parse error:", error);
    return defaultValue;
  }
}

function safeJsonStringify(obj, defaultValue = "{}") {
  try {
    return JSON.stringify(obj);
  } catch (error) {
    console.error("JSON stringify error:", error);
    return defaultValue;
  }
}
```

### 4. Advanced Array Methods

#### Transformation Methods:

```javascript
const numbers = [1, 2, 3, 4, 5];

// map() - Transform each element
const doubled = numbers.map((num) => num * 2);
// [2, 4, 6, 8, 10]

// filter() - Select elements based on condition
const evens = numbers.filter((num) => num % 2 === 0);
// [2, 4]

// reduce() - Reduce array to single value
const sum = numbers.reduce((acc, num) => acc + num, 0);
// 15

const max = numbers.reduce((max, num) => (num > max ? num : max));
// 5

// flatMap() - Map and flatten
const nested = [[1, 2], [3, 4], [5]];
const flattened = nested.flatMap((arr) => arr);
// [1, 2, 3, 4, 5]
```

#### Search and Test Methods:

```javascript
const users = [
  { id: 1, name: "Nazriel Rahman Al'afath", active: true },
  { id: 2, name: "Jane", active: false },
  { id: 3, name: "Bob", active: true },
];

// find() - First element that matches
const activeUser = users.find((user) => user.active);
// { id: 1, name: "Nazriel Rahman Al'afath", active: true }

// findIndex() - Index of first match
const index = users.findIndex((user) => user.name === "Jane");
// 1

// some() - Test if any element matches
const hasActiveUsers = users.some((user) => user.active);
// true

// every() - Test if all elements match
const allActive = users.every((user) => user.active);
// false

// includes() - Check if array contains value
const hasNazriel = users.map((u) => u.name).includes("Nazriel Rahman Al'afath");
// true
```

#### Sorting and Manipulation:

```javascript
const items = [3, 1, 4, 1, 5, 9, 2, 6];

// sort() - Sort array (modifies original)
items.sort((a, b) => a - b); // Ascending
items.sort((a, b) => b - a); // Descending

// Complex sorting
users.sort((a, b) => {
  // Sort by active status first, then by name
  if (a.active !== b.active) {
    return b.active - a.active; // Active users first
  }
  return a.name.localeCompare(b.name); // Then alphabetically
});

// reverse() - Reverse array order
const reversed = items.slice().reverse(); // Non-mutating

// splice() - Add/remove elements
items.splice(2, 1, "new"); // Remove 1 element at index 2, add 'new'

// slice() - Extract portion of array
const portion = items.slice(1, 4); // Elements from index 1 to 3
```

### 5. Object Manipulation

#### Object Property Operations:

```javascript
const person = { name: "Nazriel Rahman Al'afath", age: 30 };

// Object.keys() - Get all property names
const keys = Object.keys(person); // ["name", "age"]

// Object.values() - Get all property values
const values = Object.values(person); // ["Nazriel Rahman Al'afath", 30]

// Object.entries() - Get key-value pairs
const entries = Object.entries(person); // [["name", "Nazriel Rahman Al'afath"], ["age", 30]]

// Object.fromEntries() - Create object from entries
const newObj = Object.fromEntries(entries); // { name: "Nazriel Rahman Al'afath", age: 30 }
```

#### Object Property Descriptors:

```javascript
// Define property with descriptor
Object.defineProperty(person, "id", {
  value: 123,
  writable: false, // Cannot be changed
  enumerable: false, // Won't appear in for...in or Object.keys()
  configurable: false, // Cannot be deleted or reconfigured
});

// Get property descriptor
const descriptor = Object.getOwnPropertyDescriptor(person, "name");
// { value: "Nazriel Rahman Al'afath", writable: true, enumerable: true, configurable: true }
```

#### Object Copying and Merging:

```javascript
// Shallow copy
const copy1 = Object.assign({}, person);
const copy2 = { ...person }; // Spread syntax

// Deep copy (for simple objects)
const deepCopy = JSON.parse(JSON.stringify(person));

// Merge objects
const defaults = { theme: "light", language: "en" };
const userPrefs = { theme: "dark" };
const settings = Object.assign({}, defaults, userPrefs);
// { theme: 'dark', language: 'en' }

// Using spread (more readable)
const settings2 = { ...defaults, ...userPrefs };
```

### 6. ES6+ Features

#### Destructuring Assignment:

```javascript
// Array destructuring
const [first, second, ...rest] = [1, 2, 3, 4, 5];
// first = 1, second = 2, rest = [3, 4, 5]

// Object destructuring
const { name, age, email = "not provided" } = person;

// Nested destructuring
const user = {
  id: 1,
  profile: {
    name: "Nazriel Rahman Al'afath",
    preferences: {
      theme: "dark",
    },
  },
};

const {
  profile: {
    name: userName,
    preferences: { theme },
  },
} = user;
// userName = "Nazriel Rahman Al'afath", theme = "dark"

// Destructuring in function parameters
function greet({ name, age = 0 }) {
  return `Hello ${name}, you are ${age} years old`;
}
```

#### Template Literals:

```javascript
const name = "Nazriel Rahman Al'afath";
const age = 30;

// Basic template literal
const message = `Hello, my name is ${name} and I'm ${age} years old.`;

// Multi-line strings
const html = `
    <div class="user-card">
        <h2>${name}</h2>
        <p>Age: ${age}</p>
    </div>
`;

// Tagged template literals
function highlight(strings, ...values) {
  return strings.reduce((result, string, i) => {
    return result + string + (values[i] ? `<mark>${values[i]}</mark>` : "");
  }, "");
}

const highlighted = highlight`Hello ${name}, you are ${age} years old.`;
```

#### Arrow Functions and Methods:

```javascript
// Arrow function syntax
const square = (x) => x * x;
const add = (a, b) => a + b;
const greet = (name) => `Hello, ${name}!`;

// Array methods with arrow functions
const users = [
  { name: "Nazriel Rahman Al'afath", age: 30 },
  { name: "Jane", age: 25 },
  { name: "Bob", age: 35 },
];

const names = users.map((user) => user.name);
const adults = users.filter((user) => user.age >= 18);
const totalAge = users.reduce((sum, user) => sum + user.age, 0);
```

### 7. Data Validation

#### Type Checking:

```javascript
function validateData(data, schema) {
  const errors = [];

  for (const [key, rules] of Object.entries(schema)) {
    const value = data[key];

    // Required check
    if (
      rules.required &&
      (value === undefined || value === null || value === "")
    ) {
      errors.push(`${key} is required`);
      continue;
    }

    // Type check
    if (value !== undefined && rules.type) {
      const actualType = Array.isArray(value) ? "array" : typeof value;
      if (actualType !== rules.type) {
        errors.push(`${key} must be of type ${rules.type}`);
      }
    }

    // Length check for strings
    if (
      rules.minLength &&
      typeof value === "string" &&
      value.length < rules.minLength
    ) {
      errors.push(`${key} must be at least ${rules.minLength} characters`);
    }

    // Custom validation
    if (rules.validate && typeof rules.validate === "function") {
      const isValid = rules.validate(value);
      if (!isValid) {
        errors.push(`${key} failed custom validation`);
      }
    }
  }

  return {
    isValid: errors.length === 0,
    errors,
  };
}

// Usage
const userSchema = {
  name: { required: true, type: "string", minLength: 2 },
  email: {
    required: true,
    type: "string",
    validate: (value) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value),
  },
  age: { required: false, type: "number" },
};

const result = validateData(userData, userSchema);
```

#### Sanitization:

```javascript
function sanitizeString(str) {
  if (typeof str !== "string") return str;

  return str
    .trim() // Remove whitespace
    .replace(/[<>]/g, "") // Remove potential HTML
    .replace(/[^\w\s-]/gi, ""); // Keep only alphanumeric, spaces, hyphens
}

function sanitizeObject(obj, schema) {
  const sanitized = {};

  for (const [key, rules] of Object.entries(schema)) {
    if (obj.hasOwnProperty(key)) {
      let value = obj[key];

      if (rules.sanitize) {
        value = rules.sanitize(value);
      }

      sanitized[key] = value;
    }
  }

  return sanitized;
}
```

### 8. Data Persistence Patterns

#### Repository Pattern:

```javascript
class DataRepository {
  constructor(storageKey, storage = localStorage) {
    this.storageKey = storageKey;
    this.storage = storage;
  }

  // Get all items
  getAll() {
    try {
      const data = this.storage.getItem(this.storageKey);
      return data ? JSON.parse(data) : [];
    } catch (error) {
      console.error("Error loading data:", error);
      return [];
    }
  }

  // Get item by ID
  getById(id) {
    const items = this.getAll();
    return items.find((item) => item.id === id);
  }

  // Add new item
  add(item) {
    const items = this.getAll();
    const newItem = {
      ...item,
      id: this.generateId(),
      createdAt: new Date().toISOString(),
    };
    items.push(newItem);
    this.save(items);
    return newItem;
  }

  // Update existing item
  update(id, updates) {
    const items = this.getAll();
    const index = items.findIndex((item) => item.id === id);

    if (index !== -1) {
      items[index] = {
        ...items[index],
        ...updates,
        updatedAt: new Date().toISOString(),
      };
      this.save(items);
      return items[index];
    }

    return null;
  }

  // Delete item
  delete(id) {
    const items = this.getAll();
    const filteredItems = items.filter((item) => item.id !== id);
    this.save(filteredItems);
    return filteredItems.length < items.length;
  }

  // Query with conditions
  query(predicate) {
    const items = this.getAll();
    return items.filter(predicate);
  }

  // Save to storage
  save(items) {
    try {
      this.storage.setItem(this.storageKey, JSON.stringify(items));
      return true;
    } catch (error) {
      console.error("Error saving data:", error);
      return false;
    }
  }

  // Generate unique ID
  generateId() {
    return Date.now().toString(36) + Math.random().toString(36).substr(2);
  }

  // Clear all data
  clear() {
    this.storage.removeItem(this.storageKey);
  }
}

// Usage
const userRepo = new DataRepository("users");
const user = userRepo.add({
  name: "Nazriel Rahman Al'afath",
  email: "nazriel.rahman@email.com",
});
const allUsers = userRepo.getAll();
const activeUsers = userRepo.query((user) => user.active === true);
```

#### Observable Pattern for Data Changes:

```javascript
class ObservableData {
  constructor(initialData = {}) {
    this.data = initialData;
    this.observers = [];
  }

  // Subscribe to data changes
  subscribe(observer) {
    this.observers.push(observer);

    // Return unsubscribe function
    return () => {
      const index = this.observers.indexOf(observer);
      if (index > -1) {
        this.observers.splice(index, 1);
      }
    };
  }

  // Notify all observers
  notify(change) {
    this.observers.forEach((observer) => {
      try {
        observer(change);
      } catch (error) {
        console.error("Observer error:", error);
      }
    });
  }

  // Set data
  set(key, value) {
    const oldValue = this.data[key];
    this.data[key] = value;

    this.notify({
      type: "set",
      key,
      value,
      oldValue,
      data: { ...this.data },
    });
  }

  // Get data
  get(key) {
    return this.data[key];
  }

  // Delete data
  delete(key) {
    const oldValue = this.data[key];
    delete this.data[key];

    this.notify({
      type: "delete",
      key,
      oldValue,
      data: { ...this.data },
    });
  }

  // Update multiple properties
  update(updates) {
    const oldData = { ...this.data };
    Object.assign(this.data, updates);

    this.notify({
      type: "update",
      updates,
      oldData,
      data: { ...this.data },
    });
  }
}
```

## 🎯 Performance Considerations

### 1. **Storage Quotas and Limits**

```javascript
// Check storage quota (modern browsers)
if ("storage" in navigator && "estimate" in navigator.storage) {
  navigator.storage.estimate().then((estimate) => {
    console.log("Storage quota:", estimate.quota);
    console.log("Storage usage:", estimate.usage);
    console.log("Available:", estimate.quota - estimate.usage);
  });
}

// Handle storage quota exceeded
function handleStorageQuota(error) {
  if (error.name === "QuotaExceededError") {
    // Clear old data or ask user to free up space
    console.warn("Storage quota exceeded");
    // Implement cleanup strategy
  }
}
```

### 2. **Data Compression**

```javascript
// Simple string compression for storage
function compressData(data) {
  const jsonString = JSON.stringify(data);
  // Use LZ-string library or similar for real compression
  return btoa(jsonString); // Basic base64 encoding
}

function decompressData(compressedData) {
  try {
    const jsonString = atob(compressedData);
    return JSON.parse(jsonString);
  } catch (error) {
    console.error("Decompression failed:", error);
    return null;
  }
}
```

### 3. **Lazy Loading and Caching**

```javascript
class CachedRepository extends DataRepository {
  constructor(storageKey, cacheTimeout = 5 * 60 * 1000) {
    // 5 minutes
    super(storageKey);
    this.cache = null;
    this.cacheTimestamp = 0;
    this.cacheTimeout = cacheTimeout;
  }

  getAll() {
    const now = Date.now();

    // Return cached data if still valid
    if (this.cache && now - this.cacheTimestamp < this.cacheTimeout) {
      return this.cache;
    }

    // Load fresh data
    this.cache = super.getAll();
    this.cacheTimestamp = now;

    return this.cache;
  }

  // Invalidate cache on writes
  save(items) {
    const result = super.save(items);
    this.cache = null; // Invalidate cache
    return result;
  }
}
```

## 🔧 Best Practices

### 1. **Error Handling**

```javascript
// Comprehensive error handling
class SafeStorage {
  static set(key, value) {
    try {
      localStorage.setItem(key, JSON.stringify(value));
      return { success: true };
    } catch (error) {
      return {
        success: false,
        error: error.message,
        code: error.name,
      };
    }
  }

  static get(key, defaultValue = null) {
    try {
      const item = localStorage.getItem(key);
      return item ? JSON.parse(item) : defaultValue;
    } catch (error) {
      console.error("Storage get error:", error);
      return defaultValue;
    }
  }
}
```

### 2. **Data Migration**

```javascript
class DataMigrator {
  static migrate(storageKey, currentVersion) {
    const versionKey = `${storageKey}_version`;
    const storedVersion = localStorage.getItem(versionKey) || "1.0.0";

    if (storedVersion !== currentVersion) {
      console.log(`Migrating data from ${storedVersion} to ${currentVersion}`);

      // Perform migration based on version
      const migrationPath = this.getMigrationPath(
        storedVersion,
        currentVersion
      );

      for (const migration of migrationPath) {
        migration(storageKey);
      }

      localStorage.setItem(versionKey, currentVersion);
    }
  }

  static getMigrationPath(from, to) {
    // Return array of migration functions
    const migrations = {
      "1.0.0_to_1.1.0": (storageKey) => {
        // Migration logic
      },
    };

    // Build migration path
    return [];
  }
}
```

## 📝 Latihan Praktik

### 1. **Basic Storage Operations**

- Menyimpan dan mengambil data
- Mengelola multiple data types
- Error handling

### 2. **Data Manipulation**

- Array operations
- Object transformations
- Data filtering dan sorting

### 3. **Advanced Patterns**

- Repository pattern
- Observer pattern
- Data validation

### 4. **Real-world Applications**

- Todo list dengan persistence
- User preferences
- Shopping cart
- Form data auto-save

Pemahaman data handling yang baik akan membantu Anda membangun aplikasi web yang dapat menyimpan dan mengelola data pengguna secara efektif.
