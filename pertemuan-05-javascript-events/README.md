# PERTEMUAN 5: JAVASCRIPT EVENTS - Komunikasi User-Computer 🎭

## 🎭 **Filosofi Events: Bahasa Komunikasi Digital**

Events dalam JavaScript adalah seperti **bahasa isyarat universal** antara user dan komputer. Setiap klik, hover, scroll, atau keyboard press adalah **pesan** yang dikirim user kepada aplikasi, dan JavaScript bertugas **menerjemahkan dan merespons** pesan tersebut.

### **Analogi: Events sebagai Percakapan**

```
User Action → Event → JavaScript Handler → Application Response
     ↓           ↓           ↓                    ↓
   "Klik"    'click'    handleClick()        "Tampilkan popup"
   "Ketik"   'input'    handleInput()        "Validasi form"
   "Scroll"  'scroll'   handleScroll()       "Load more content"
```

## 🎯 **Event System - Arsitektur Komunikasi**

### **Event Flow: Perjalanan Event dalam DOM**

**Analogi: Berita di Kantor Berlantai**

```javascript
// Event Flow: Capturing → Target → Bubbling
document.addEventListener(
  "click",
  function (e) {
    console.log("Document level (Capturing)");
  },
  true
); // true = capturing phase

document.body.addEventListener("click", function (e) {
  console.log("Body level");
});

document.querySelector(".card").addEventListener("click", function (e) {
  console.log("Card level (Target)");
});

document.querySelector(".button").addEventListener("click", function (e) {
  console.log("Button clicked (Target)");
  // e.stopPropagation(); // Hentikan bubbling
});

/*
Urutan eksekusi:
1. Document (Capturing) ← Dari atas ke bawah
2. Body (Capturing)
3. Card (Capturing)
4. Button (Target) ← Elemen yang diklik
5. Card (Bubbling) ← Dari bawah ke atas
6. Body (Bubbling)
7. Document (Bubbling)
*/
```

### **Event Object - Paket Informasi**

```javascript
function handleEvent(event) {
  console.log("=== EVENT INFORMATION ===");
  console.log("Event type:", event.type); // 'click', 'keydown', etc.
  console.log("Target element:", event.target); // Element yang di-klik
  console.log("Current target:", event.currentTarget); // Element dengan listener
  console.log("Mouse position:", event.clientX, event.clientY);
  console.log("Key pressed:", event.key); // Untuk keyboard events
  console.log("Ctrl key held:", event.ctrlKey); // Boolean
  console.log("Shift key held:", event.shiftKey); // Boolean
  console.log("Alt key held:", event.altKey); // Boolean

  // Prevent default browser behavior
  event.preventDefault();

  // Stop event from bubbling up
  event.stopPropagation();
}
```

## 🎨 **Event Types - Kategori Komunikasi**

### **1. Mouse Events - Interaksi Pointer**

```javascript
// Mouse Event Types dan Use Cases
const element = document.getElementById("interactive-card");

// Click Events
element.addEventListener("click", function (e) {
  console.log("Single click - Primary action");
  // Use case: Button actions, navigation, selection
});

element.addEventListener("dblclick", function (e) {
  console.log("Double click - Secondary action");
  // Use case: Edit mode, full screen, quick actions
});

element.addEventListener("contextmenu", function (e) {
  e.preventDefault(); // Prevent default right-click menu
  console.log("Right click - Context menu");
  // Use case: Custom context menus, alternative actions
});

// Mouse Movement
element.addEventListener("mouseenter", function (e) {
  console.log("Mouse entered - Show tooltip/preview");
  this.style.transform = "scale(1.05)";
  // Use case: Hover effects, tooltips, previews
});

element.addEventListener("mouseleave", function (e) {
  console.log("Mouse left - Hide tooltip");
  this.style.transform = "scale(1)";
  // Use case: Clean up hover effects
});

element.addEventListener("mousemove", function (e) {
  // Use case: Drag operations, cursor tracking
  const rect = this.getBoundingClientRect();
  const x = e.clientX - rect.left;
  const y = e.clientY - rect.top;

  // Create parallax effect
  this.style.background = `radial-gradient(circle at ${x}px ${y}px, rgba(79, 172, 254, 0.3), transparent)`;
});

// Mouse Button States
element.addEventListener("mousedown", function (e) {
  console.log("Mouse button pressed");
  this.classList.add("pressed");
  // Use case: Start drag operation, button press feedback
});

element.addEventListener("mouseup", function (e) {
  console.log("Mouse button released");
  this.classList.remove("pressed");
  // Use case: End drag operation, button release feedback
});
```

### **2. Keyboard Events - Input Text dan Shortcuts**

```javascript
// Keyboard Event Types
const inputField = document.getElementById("search-input");

// Key Press Events
inputField.addEventListener("keydown", function (e) {
  console.log("Key pressed down:", e.key);

  // Handle special keys
  if (e.key === "Enter") {
    console.log("Enter pressed - Submit form or execute search");
    performSearch();
  }

  if (e.key === "Escape") {
    console.log("Escape pressed - Cancel operation");
    clearSearch();
  }

  // Keyboard shortcuts
  if (e.ctrlKey && e.key === "s") {
    e.preventDefault(); // Prevent browser save dialog
    console.log("Ctrl+S - Save data");
    saveData();
  }

  if (e.ctrlKey && e.key === "z") {
    e.preventDefault();
    console.log("Ctrl+Z - Undo operation");
    undoLastAction();
  }
});

inputField.addEventListener("keyup", function (e) {
  console.log("Key released:", e.key);
  // Use case: Real-time search, input validation
});

inputField.addEventListener("input", function (e) {
  console.log("Input value changed:", e.target.value);

  // Real-time validation
  validateInput(e.target.value);

  // Real-time search suggestions
  showSearchSuggestions(e.target.value);
});

// Advanced keyboard handling
document.addEventListener("keydown", function (e) {
  // Global keyboard shortcuts
  const shortcuts = {
    F1: () => showHelp(),
    F11: () => toggleFullscreen(),
    "/": () => focusSearch(),
    "?": () => showKeyboardShortcuts(),
  };

  if (shortcuts[e.key]) {
    e.preventDefault();
    shortcuts[e.key]();
  }

  // Navigation shortcuts
  if (e.altKey) {
    switch (e.key) {
      case "1":
        switchToTab(1);
        break;
      case "2":
        switchToTab(2);
        break;
      case "3":
        switchToTab(3);
        break;
    }
  }
});
```

### **3. Form Events - Data Input Management**

```javascript
const form = document.getElementById("student-form");
const nameInput = document.getElementById("name");
const emailInput = document.getElementById("email");

// Form Submission
form.addEventListener("submit", function (e) {
  e.preventDefault(); // Prevent page reload
  console.log("Form submitted");

  // Collect form data
  const formData = new FormData(this);
  const data = Object.fromEntries(formData.entries());

  // Validate data
  if (validateFormData(data)) {
    submitData(data);
  } else {
    showValidationErrors();
  }
});

// Input Field Events
nameInput.addEventListener("focus", function (e) {
  console.log("Name field focused");
  this.parentElement.classList.add("focused");
  // Use case: Highlight active field, show hints
});

nameInput.addEventListener("blur", function (e) {
  console.log("Name field lost focus");
  this.parentElement.classList.remove("focused");

  // Validate field when user leaves
  validateField(this);
});

emailInput.addEventListener("change", function (e) {
  console.log("Email field value changed");
  // Use case: Validation after user completes input

  if (this.value) {
    validateEmail(this.value);
  }
});

// Real-time input handling
nameInput.addEventListener("input", function (e) {
  const value = e.target.value;

  // Character limit feedback
  const maxLength = 50;
  const remaining = maxLength - value.length;

  const counter = document.getElementById("name-counter");
  counter.textContent = `${remaining} characters remaining`;

  if (remaining < 10) {
    counter.classList.add("warning");
  } else {
    counter.classList.remove("warning");
  }
});

// Select dropdown events
const majorSelect = document.getElementById("major");
majorSelect.addEventListener("change", function (e) {
  console.log("Major selected:", e.target.value);

  // Dynamic form updates based on selection
  updateFormFields(e.target.value);
});
```

### **4. Window dan Document Events - Aplikasi Lifecycle**

```javascript
// Page Load Events
window.addEventListener("load", function () {
  console.log("Page fully loaded (including images)");
  // Use case: Initialize heavy components, start animations
  initializeApp();
});

document.addEventListener("DOMContentLoaded", function () {
  console.log("DOM fully loaded and parsed");
  // Use case: Initialize JavaScript, bind events
  setupEventListeners();
});

// Before page unload
window.addEventListener("beforeunload", function (e) {
  console.log("User trying to leave page");

  // Check if there are unsaved changes
  if (hasUnsavedChanges()) {
    e.preventDefault();
    e.returnValue = ""; // Show browser confirmation dialog
    return "You have unsaved changes. Are you sure you want to leave?";
  }
});

// Page visibility (user switches tabs)
document.addEventListener("visibilitychange", function () {
  if (document.hidden) {
    console.log("Page hidden - Pause activities");
    pauseAnimations();
    pauseAutoSave();
  } else {
    console.log("Page visible - Resume activities");
    resumeAnimations();
    resumeAutoSave();
  }
});

// Scroll events
let scrollTimeout;
window.addEventListener("scroll", function () {
  // Throttle scroll events for performance
  if (scrollTimeout) {
    clearTimeout(scrollTimeout);
  }

  scrollTimeout = setTimeout(() => {
    const scrollTop = window.pageYOffset || document.documentElement.scrollTop;
    const windowHeight = window.innerHeight;
    const documentHeight = document.documentElement.scrollHeight;

    // Scroll progress
    const scrollProgress = (scrollTop / (documentHeight - windowHeight)) * 100;
    updateScrollProgress(scrollProgress);

    // Lazy loading
    checkLazyImages();

    // Infinite scroll
    if (scrollTop + windowHeight >= documentHeight - 100) {
      loadMoreContent();
    }
  }, 100);
});

// Resize events
window.addEventListener("resize", function () {
  console.log("Window resized:", window.innerWidth, "x", window.innerHeight);

  // Update responsive components
  updateResponsiveLayout();

  // Recalculate positions
  repositionElements();
});
```

## 🛠️ **Advanced Event Patterns**

### **1. Event Delegation - Efisiensi untuk Dynamic Content**

```javascript
// Problem: Event listeners untuk elemen yang belum ada
// Solution: Event delegation pada parent element

const studentsContainer = document.getElementById("students-container");

// Single event listener untuk semua student cards
studentsContainer.addEventListener("click", function (e) {
  const target = e.target;
  const card = target.closest(".student-card");

  if (!card) return; // Click bukan pada student card

  // Handle different button types
  if (target.classList.contains("btn-edit")) {
    editStudent(card.dataset.studentId);
  } else if (target.classList.contains("btn-delete")) {
    deleteStudent(card.dataset.studentId);
  } else if (target.classList.contains("btn-view")) {
    viewStudent(card.dataset.studentId);
  } else if (target.classList.contains("btn-favorite")) {
    toggleFavorite(card.dataset.studentId);
  }

  // Handle card click (not on buttons)
  if (
    target === card ||
    (card.contains(target) && !target.classList.contains("btn"))
  ) {
    showStudentDetails(card.dataset.studentId);
  }
});

// Dynamic content - events akan otomatis bekerja
function addNewStudent(studentData) {
  const card = createStudentCard(studentData);
  studentsContainer.appendChild(card); // Events sudah ter-handle oleh delegation
}
```

### **2. Custom Events - Inter-Component Communication**

```javascript
// Create custom events untuk modular architecture
class StudentManager {
  constructor() {
    this.setupEventListeners();
  }

  setupEventListeners() {
    // Listen for custom events
    document.addEventListener(
      "studentAdded",
      this.handleStudentAdded.bind(this)
    );
    document.addEventListener(
      "studentUpdated",
      this.handleStudentUpdated.bind(this)
    );
    document.addEventListener(
      "studentDeleted",
      this.handleStudentDeleted.bind(this)
    );
  }

  addStudent(studentData) {
    // Add student logic...

    // Dispatch custom event
    const event = new CustomEvent("studentAdded", {
      detail: {
        student: studentData,
        timestamp: new Date(),
        source: "StudentManager",
      },
      bubbles: true,
    });

    document.dispatchEvent(event);
  }

  handleStudentAdded(e) {
    console.log("Student added:", e.detail.student);

    // Update UI
    this.updateStudentCount();
    this.showNotification(`${e.detail.student.name} berhasil ditambahkan!`);

    // Analytics
    this.trackEvent("student_added", e.detail.student);
  }
}

// Other components can listen to the same events
class StatisticsPanel {
  constructor() {
    document.addEventListener("studentAdded", () => this.updateStats());
    document.addEventListener("studentDeleted", () => this.updateStats());
  }

  updateStats() {
    // Update statistics display
  }
}
```

### **3. Event Throttling dan Debouncing**

```javascript
// Throttling - Limit execution frequency
function throttle(func, delay) {
  let timeoutId;
  let lastExecTime = 0;

  return function (...args) {
    const currentTime = Date.now();

    if (currentTime - lastExecTime > delay) {
      func.apply(this, args);
      lastExecTime = currentTime;
    }
  };
}

// Debouncing - Delay execution until activity stops
function debounce(func, delay) {
  let timeoutId;

  return function (...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => func.apply(this, args), delay);
  };
}

// Usage examples
const searchInput = document.getElementById("search");

// Throttled scroll (max 10 times per second)
window.addEventListener(
  "scroll",
  throttle(function () {
    updateScrollIndicator();
  }, 100)
);

// Debounced search (wait 300ms after user stops typing)
searchInput.addEventListener(
  "input",
  debounce(function (e) {
    performSearch(e.target.value);
  }, 300)
);

// Throttled mouse move (for performance)
document.addEventListener(
  "mousemove",
  throttle(function (e) {
    updateCursorEffect(e.clientX, e.clientY);
  }, 16)
); // ~60fps
```

## 🎨 **Real-world Event Implementations**

### **Interactive Profile Application**

```javascript
class InteractiveProfile {
  constructor() {
    this.init();
    this.setupEventListeners();
  }

  setupEventListeners() {
    // Profile image hover effect
    const profileImg = document.getElementById("profile-image");
    profileImg.addEventListener("mouseenter", this.showImageActions.bind(this));
    profileImg.addEventListener("mouseleave", this.hideImageActions.bind(this));

    // Keyboard shortcuts
    document.addEventListener(
      "keydown",
      this.handleKeyboardShortcuts.bind(this)
    );

    // Form auto-save
    const form = document.getElementById("profile-form");
    form.addEventListener("input", debounce(this.autoSave.bind(this), 1000));

    // Skill level interactions
    const skillBars = document.querySelectorAll(".skill-bar");
    skillBars.forEach((bar) => {
      bar.addEventListener("click", this.adjustSkillLevel.bind(this));
    });

    // Theme switcher
    const themeToggle = document.getElementById("theme-toggle");
    themeToggle.addEventListener("change", this.switchTheme.bind(this));

    // Notification system
    document.addEventListener("notification", this.showNotification.bind(this));
  }

  showImageActions(e) {
    const actions = document.createElement("div");
    actions.className = "image-actions";
    actions.innerHTML = `
      <button class="btn btn-sm btn-primary">Change</button>
      <button class="btn btn-sm btn-secondary">Remove</button>
    `;

    e.target.parentElement.appendChild(actions);

    // Handle action buttons
    actions.addEventListener("click", (event) => {
      if (event.target.textContent === "Change") {
        this.changeProfileImage();
      } else if (event.target.textContent === "Remove") {
        this.removeProfileImage();
      }
    });
  }

  hideImageActions(e) {
    const actions = e.target.parentElement.querySelector(".image-actions");
    if (actions) {
      actions.remove();
    }
  }

  handleKeyboardShortcuts(e) {
    const shortcuts = {
      e: () => this.enableEditMode(),
      s: () => this.saveProfile(),
      Escape: () => this.cancelEdit(),
      h: () => this.showHelp(),
    };

    if (e.ctrlKey && shortcuts[e.key]) {
      e.preventDefault();
      shortcuts[e.key]();
    }
  }

  autoSave() {
    const formData = new FormData(document.getElementById("profile-form"));
    const data = Object.fromEntries(formData.entries());

    // Save to localStorage
    localStorage.setItem("profileDraft", JSON.stringify(data));

    // Show auto-save indicator
    this.showAutoSaveIndicator();
  }

  adjustSkillLevel(e) {
    const skillBar = e.currentTarget;
    const rect = skillBar.getBoundingClientRect();
    const clickX = e.clientX - rect.left;
    const percentage = (clickX / rect.width) * 100;

    const progressBar = skillBar.querySelector(".progress-bar");
    progressBar.style.width = percentage + "%";

    // Update skill value
    const skillName = skillBar.dataset.skill;
    this.updateSkillValue(skillName, Math.round(percentage));
  }

  switchTheme(e) {
    const isDark = e.target.checked;
    document.body.classList.toggle("dark-theme", isDark);

    // Save theme preference
    localStorage.setItem("theme", isDark ? "dark" : "light");

    // Dispatch theme change event
    const event = new CustomEvent("themeChanged", {
      detail: { theme: isDark ? "dark" : "light" },
    });
    document.dispatchEvent(event);
  }

  showNotification(e) {
    const { message, type = "info", duration = 3000 } = e.detail;

    const notification = document.createElement("div");
    notification.className = `notification ${type}`;
    notification.textContent = message;

    document.body.appendChild(notification);

    // Auto remove
    setTimeout(() => {
      notification.remove();
    }, duration);
  }
}

// Initialize interactive profile
document.addEventListener("DOMContentLoaded", () => {
  new InteractiveProfile();
});
```

## 🎓 **Best Practices dan Performance**

### **1. Memory Management**

```javascript
class ComponentWithEvents {
  constructor() {
    this.eventListeners = [];
    this.boundMethods = {};
    this.setupEvents();
  }

  setupEvents() {
    // Bind methods once to avoid memory leaks
    this.boundMethods.handleClick = this.handleClick.bind(this);
    this.boundMethods.handleKeydown = this.handleKeydown.bind(this);

    // Track all event listeners for cleanup
    this.addEventListener(document, "click", this.boundMethods.handleClick);
    this.addEventListener(window, "keydown", this.boundMethods.handleKeydown);
  }

  addEventListener(element, event, handler) {
    element.addEventListener(event, handler);
    this.eventListeners.push({ element, event, handler });
  }

  destroy() {
    // Clean up all event listeners
    this.eventListeners.forEach(({ element, event, handler }) => {
      element.removeEventListener(event, handler);
    });
    this.eventListeners = [];
    this.boundMethods = {};
  }
}
```

### **2. Performance Optimization**

```javascript
// Use passive listeners for better scroll performance
window.addEventListener("scroll", handleScroll, { passive: true });

// Use capture phase strategically
document.addEventListener("click", handleGlobalClick, { capture: true });

// Remove event listeners when not needed
const controller = new AbortController();
element.addEventListener("click", handler, { signal: controller.signal });
// Later: controller.abort(); // Removes all listeners with this signal
```

## 🌟 **Kesimpulan Filosofis**

Events adalah **jantung interaktivitas web**. Memahami event system berarti memahami:

1. **User Psychology** - Bagaimana user berinteraksi dengan interface
2. **Application Flow** - Bagaimana data mengalir berdasarkan user actions
3. **Performance Impact** - Bagaimana event handling mempengaruhi responsiveness
4. **Architecture Patterns** - Bagaimana membangun aplikasi yang scalable

**Philosophy**: "Good event handling is invisible to users but creates the magic that makes applications feel alive and responsive."

Events mengajarkan kita bahwa **programming is conversation** - antara user dan machine, antara components, antara present state dan future possibilities. 🎭✨

---

## 📁 **File Praktikum dalam Folder**

1. `01-basic-events.html` - Event dasar (click, hover, keyboard)
2. `02-form-events.html` - Form submission dan input validation dengan feedback Indonesia
3. `03-keyboard-events.html` - Keyboard shortcuts dan accessibility
4. `04-mouse-events.html` - Mouse interactions yang kompleks
5. `05-event-delegation.html` - Menangani dynamic content dengan efisien
6. `06-event-prevention.html` - preventDefault dan stopPropagation strategies
7. `studi-kasus-interactive-gallery.html` - Galeri foto interaktif dengan nama Indonesia

## 🎯 **Tujuan Pembelajaran**

Membuat halaman web yang responsif terhadap interaksi pengguna dengan JavaScript Events, memahami event flow, dan mengimplementasikan pattern-pattern advanced untuk aplikasi yang performant dan user-friendly.
// Keyboard events
element.addEventListener('keydown', handler);
element.addEventListener('keyup', handler);
element.addEventListener('keypress', handler); // Deprecated

// Detecting specific keys
function handleKeyDown(event) {
if (event.key === 'Enter') {
// Handle Enter key
}
if (event.ctrlKey && event.key === 's') {
event.preventDefault(); // Prevent browser save
// Handle Ctrl+S
}
}

````

#### Form Events:
```javascript
// Form events
form.addEventListener('submit', handler);
input.addEventListener('input', handler);    // Real-time changes
input.addEventListener('change', handler);   // After losing focus
input.addEventListener('focus', handler);
input.addEventListener('blur', handler);
select.addEventListener('change', handler);
````

#### Window Events:

```javascript
// Window events
window.addEventListener("load", handler); // All resources loaded
window.addEventListener("DOMContentLoaded", handler); // DOM ready
window.addEventListener("resize", handler);
window.addEventListener("scroll", handler);
window.addEventListener("beforeunload", handler);
```

### 4. Event Object

#### Properties Event Object:

```javascript
function handleEvent(event) {
  // Target and current target
  console.log(event.target); // Element that triggered event
  console.log(event.currentTarget); // Element with event listener

  // Event type and timing
  console.log(event.type); // Event type (click, keydown, etc.)
  console.log(event.timeStamp); // When event occurred

  // Mouse position
  console.log(event.clientX, event.clientY); // Relative to viewport
  console.log(event.pageX, event.pageY); // Relative to document
  console.log(event.screenX, event.screenY); // Relative to screen

  // Keyboard modifiers
  console.log(event.ctrlKey); // Ctrl key pressed
  console.log(event.shiftKey); // Shift key pressed
  console.log(event.altKey); // Alt key pressed
  console.log(event.metaKey); // Meta key (Cmd/Windows key)

  // Keyboard specific
  console.log(event.key); // Key value
  console.log(event.code); // Physical key code
  console.log(event.keyCode); // Deprecated
}
```

#### Event Methods:

```javascript
function handleEvent(event) {
  // Prevent default browser behavior
  event.preventDefault();

  // Stop event from propagating
  event.stopPropagation();

  // Stop other listeners on same element
  event.stopImmediatePropagation();
}
```

### 5. Event Delegation

#### Konsep Event Delegation:

Event delegation adalah teknik menangani events pada parent element untuk child elements yang mungkin ditambahkan secara dinamis.

```javascript
// Instead of adding listeners to each button
const buttons = document.querySelectorAll(".button");
buttons.forEach((button) => {
  button.addEventListener("click", handleClick);
});

// Use event delegation on parent
const container = document.getElementById("button-container");
container.addEventListener("click", function (event) {
  if (event.target.matches(".button")) {
    handleClick(event);
  }
});
```

#### Keuntungan Event Delegation:

- **Performance**: Fewer event listeners
- **Dynamic elements**: Works with elements added later
- **Memory efficiency**: Less memory usage
- **Easier management**: Centralized event handling

### 6. Custom Events

#### Membuat Custom Events:

```javascript
// Creating custom events
const customEvent = new CustomEvent("myCustomEvent", {
  detail: {
    message: "Hello from custom event!",
    timestamp: Date.now(),
  },
  bubbles: true,
  cancelable: true,
});

// Dispatching custom event
element.dispatchEvent(customEvent);

// Listening for custom event
element.addEventListener("myCustomEvent", function (event) {
  console.log(event.detail.message);
});
```

#### Event Constructor Options:

```javascript
const event = new CustomEvent("eventName", {
  detail: {}, // Custom data
  bubbles: false, // Should bubble up
  cancelable: false, // Can be cancelled
  composed: false, // Cross shadow DOM boundary
});
```

### 7. Advanced Event Concepts

#### Event Throttling:

```javascript
function throttle(func, delay) {
  let timeoutId;
  let lastExecTime = 0;

  return function (...args) {
    const currentTime = Date.now();

    if (currentTime - lastExecTime > delay) {
      func.apply(this, args);
      lastExecTime = currentTime;
    } else {
      clearTimeout(timeoutId);
      timeoutId = setTimeout(() => {
        func.apply(this, args);
        lastExecTime = Date.now();
      }, delay - (currentTime - lastExecTime));
    }
  };
}

// Usage
const throttledScroll = throttle(function () {
  console.log("Scroll event");
}, 100);

window.addEventListener("scroll", throttledScroll);
```

#### Event Debouncing:

```javascript
function debounce(func, delay) {
  let timeoutId;

  return function (...args) {
    clearTimeout(timeoutId);

    timeoutId = setTimeout(() => {
      func.apply(this, args);
    }, delay);
  };
}

// Usage
const debouncedInput = debounce(function (event) {
  console.log("Input value:", event.target.value);
}, 300);

input.addEventListener("input", debouncedInput);
```

### 8. Drag and Drop API

#### Drag Events:

```javascript
// Make element draggable
element.draggable = true;

// Drag events on draggable element
element.addEventListener("dragstart", function (event) {
  event.dataTransfer.setData("text/plain", "data to transfer");
});

element.addEventListener("drag", function (event) {
  // During drag
});

element.addEventListener("dragend", function (event) {
  // Drag finished
});
```

#### Drop Events:

```javascript
// Drop zone events
dropZone.addEventListener("dragover", function (event) {
  event.preventDefault(); // Allow drop
});

dropZone.addEventListener("dragenter", function (event) {
  event.preventDefault();
  dropZone.classList.add("drag-over");
});

dropZone.addEventListener("dragleave", function (event) {
  dropZone.classList.remove("drag-over");
});

dropZone.addEventListener("drop", function (event) {
  event.preventDefault();
  const data = event.dataTransfer.getData("text/plain");
  // Handle dropped data
});
```

### 9. Touch Events (Mobile)

#### Touch Event Types:

```javascript
// Touch events
element.addEventListener("touchstart", handleTouch);
element.addEventListener("touchmove", handleTouch);
element.addEventListener("touchend", handleTouch);
element.addEventListener("touchcancel", handleTouch);

function handleTouch(event) {
  event.preventDefault(); // Prevent scrolling

  // Touch points
  const touches = event.touches; // Current touches
  const changedTouches = event.changedTouches; // Changed touches

  for (let i = 0; i < touches.length; i++) {
    const touch = touches[i];
    console.log(touch.clientX, touch.clientY);
  }
}
```

#### Gesture Recognition:

```javascript
let startX, startY, startTime;

element.addEventListener("touchstart", function (event) {
  const touch = event.touches[0];
  startX = touch.clientX;
  startY = touch.clientY;
  startTime = Date.now();
});

element.addEventListener("touchend", function (event) {
  const touch = event.changedTouches[0];
  const endX = touch.clientX;
  const endY = touch.clientY;
  const endTime = Date.now();

  const deltaX = endX - startX;
  const deltaY = endY - startY;
  const deltaTime = endTime - startTime;

  // Detect swipe
  if (Math.abs(deltaX) > 50 && deltaTime < 300) {
    if (deltaX > 0) {
      console.log("Swipe right");
    } else {
      console.log("Swipe left");
    }
  }
});
```

### 10. Performance Optimization

#### Passive Event Listeners:

```javascript
// Passive listeners for better performance
element.addEventListener("scroll", handler, { passive: true });
element.addEventListener("touchstart", handler, { passive: true });
```

#### Event Listener Management:

```javascript
class EventManager {
  constructor() {
    this.listeners = new Map();
  }

  add(element, event, handler, options = {}) {
    const key = `${element}-${event}`;

    if (!this.listeners.has(key)) {
      this.listeners.set(key, []);
    }

    this.listeners.get(key).push({ handler, options });
    element.addEventListener(event, handler, options);
  }

  remove(element, event, handler) {
    const key = `${element}-${event}`;
    const listeners = this.listeners.get(key);

    if (listeners) {
      const index = listeners.findIndex((l) => l.handler === handler);
      if (index > -1) {
        listeners.splice(index, 1);
        element.removeEventListener(event, handler);
      }
    }
  }

  removeAll(element) {
    for (const [key, listeners] of this.listeners) {
      if (key.startsWith(element.toString())) {
        listeners.forEach(({ handler, options }) => {
          const event = key.split("-")[1];
          element.removeEventListener(event, handler);
        });
        this.listeners.delete(key);
      }
    }
  }
}
```

## 🎯 Design Patterns for Events

### 1. Observer Pattern

```javascript
class EventEmitter {
  constructor() {
    this.events = {};
  }

  on(event, listener) {
    if (!this.events[event]) {
      this.events[event] = [];
    }
    this.events[event].push(listener);
  }

  off(event, listenerToRemove) {
    if (!this.events[event]) return;

    this.events[event] = this.events[event].filter(
      (listener) => listener !== listenerToRemove
    );
  }

  emit(event, data) {
    if (!this.events[event]) return;

    this.events[event].forEach((listener) => listener(data));
  }
}
```

### 2. Command Pattern

```javascript
class Command {
  constructor(execute, undo) {
    this.execute = execute;
    this.undo = undo;
  }
}

class CommandManager {
  constructor() {
    this.history = [];
    this.currentIndex = -1;
  }

  execute(command) {
    // Remove any commands after current index
    this.history = this.history.slice(0, this.currentIndex + 1);

    // Add and execute new command
    this.history.push(command);
    this.currentIndex++;
    command.execute();
  }

  undo() {
    if (this.currentIndex >= 0) {
      const command = this.history[this.currentIndex];
      command.undo();
      this.currentIndex--;
    }
  }

  redo() {
    if (this.currentIndex < this.history.length - 1) {
      this.currentIndex++;
      const command = this.history[this.currentIndex];
      command.execute();
    }
  }
}
```

### 3. State Machine

```javascript
class StateMachine {
  constructor(initialState, transitions) {
    this.state = initialState;
    this.transitions = transitions;
  }

  trigger(event) {
    const transition = this.transitions[this.state]?.[event];

    if (transition) {
      if (transition.guard && !transition.guard()) {
        return false; // Transition blocked by guard
      }

      if (transition.action) {
        transition.action();
      }

      this.state = transition.to;
      return true;
    }

    return false; // No valid transition
  }
}

// Usage example
const calculator = new StateMachine("idle", {
  idle: {
    number: { to: "number", action: () => console.log("Number entered") },
    operator: { to: "operator", action: () => console.log("Operator entered") },
  },
  number: {
    number: { to: "number", action: () => console.log("Continue number") },
    operator: {
      to: "operator",
      action: () => console.log("Operator after number"),
    },
    equals: { to: "result", action: () => console.log("Calculate result") },
  },
});
```

## 🔧 Best Practices

### 1. **Event Naming Conventions**

```javascript
// Use descriptive names
button.addEventListener("click", handleSubmitButtonClick);
form.addEventListener("submit", handleUserRegistrationSubmit);

// Use namespacing for custom events
element.dispatchEvent(new CustomEvent("app:user:login"));
element.dispatchEvent(new CustomEvent("ui:modal:open"));
```

### 2. **Error Handling in Events**

```javascript
function safeEventHandler(handler) {
  return function (event) {
    try {
      handler.call(this, event);
    } catch (error) {
      console.error("Event handler error:", error);
      // Optionally report to error tracking service
    }
  };
}

button.addEventListener("click", safeEventHandler(handleClick));
```

### 3. **Memory Management**

```javascript
// Always remove event listeners when elements are removed
function createComponent() {
  const element = document.createElement("div");

  function handleClick() {
    // Handle click
  }

  element.addEventListener("click", handleClick);

  // Cleanup function
  function destroy() {
    element.removeEventListener("click", handleClick);
    element.remove();
  }

  return { element, destroy };
}
```

### 4. **Accessibility Considerations**

```javascript
// Support both mouse and keyboard events
element.addEventListener("click", handleActivation);
element.addEventListener("keydown", function (event) {
  if (event.key === "Enter" || event.key === " ") {
    event.preventDefault();
    handleActivation(event);
  }
});

// Provide proper ARIA attributes
element.setAttribute("role", "button");
element.setAttribute("aria-label", "Close dialog");
element.setAttribute("tabindex", "0");
```

## 📖 Debugging Events

### 1. **Event Debugging Techniques**

```javascript
// Log all events on an element
function debugEvents(element) {
  const originalAddEventListener = element.addEventListener;

  element.addEventListener = function (type, listener, options) {
    console.log(`Adding ${type} listener:`, listener);
    return originalAddEventListener.call(this, type, listener, options);
  };
}

// Monitor event propagation
function monitorEvent(event) {
  console.group(`Event: ${event.type}`);
  console.log("Target:", event.target);
  console.log("Current Target:", event.currentTarget);
  console.log("Phase:", event.eventPhase);
  console.log("Bubbles:", event.bubbles);
  console.groupEnd();
}
```

### 2. **Browser DevTools**

```javascript
// Use console.trace() to see call stack
function handleClick(event) {
  console.trace("Click handler called");
}

// Use performance.mark() for timing
function handleScroll() {
  performance.mark("scroll-start");
  // Handle scroll
  performance.mark("scroll-end");
  performance.measure("scroll-duration", "scroll-start", "scroll-end");
}
```

## 📝 Latihan Praktik

### 1. **Basic Event Handling**

- Click events
- Form validation
- Keyboard shortcuts
- Mouse interactions

### 2. **Advanced Interactions**

- Drag and drop
- Touch gestures
- Custom events
- Event delegation

### 3. **Performance Optimization**

- Event throttling
- Event debouncing
- Passive listeners
- Memory management

### 4. **Real-world Applications**

- Interactive calculators
- Image galleries
- Form wizards
- Game controls

Event-driven programming adalah fundamental dalam pengembangan web modern. Memahami konsep ini akan membantu Anda membuat aplikasi web yang responsif dan interaktif.
