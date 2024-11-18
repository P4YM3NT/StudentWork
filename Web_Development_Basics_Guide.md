
# Web Development Basics for New Trainees

## **1. Introduction to Web Development Basics**

### **1.1 What is HTML?**
HTML (Hypertext Markup Language) is the foundation of any webpage. It structures the content on a website.

#### **Basic HTML Syntax**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sample Page</title>
</head>
<body>
  <!-- Headings -->
  <h1>Main Heading</h1>
  <h2>Subheading</h2>

  <!-- Paragraphs -->
  <p>This is a paragraph of text.</p>

  <!-- Links -->
  <a href="https://example.com" target="_blank">Visit Example</a>

  <!-- Images -->
  <img src="image.jpg" alt="Sample Image">

  <!-- Lists -->
  <ul>
    <li>First Item</li>
    <li>Second Item</li>
  </ul>
</body>
</html>
```

### **1.2 What is CSS?**
CSS (Cascading Style Sheets) is used to style and layout websites. It controls the design, colors, spacing, and more.

#### **CSS Syntax**
```css
/* Styling the body */
body {
  font-family: Arial, sans-serif;
  background-color: #f0f0f0;
  margin: 0;
  padding: 0;
}

/* Styling headings */
h1 {
  color: blue;
}

/* Styling links */
a {
  color: darkblue;
  text-decoration: none;
}
```

### **1.3 Writing CSS**
CSS can be written in three main ways:
1. **Inline**: Directly within an HTML element.
   ```html
   <p style="color: red;">This is styled inline.</p>
   ```
2. **Internal**: Inside a `<style>` block in the HTML `<head>`.
   ```html
   <style>
     p {
       font-size: 16px;
     }
   </style>
   ```
3. **External**: In a separate `.css` file.
   ```html
   <link rel="stylesheet" href="styles.css">
   ```

### **1.4 The Box Model**
The box model is crucial for layout and spacing. Every HTML element is treated as a box with:
- **Content**: The text or image inside the box.
- **Padding**: Space between the content and the border.
- **Border**: The edge of the box.
- **Margin**: Space between the box and other elements.

---

## **2. JavaScript Basics**
JavaScript is used to make websites interactive. It can manipulate HTML and CSS dynamically.

#### **Example: Changing Text with JavaScript**
```html
<button onclick="changeText()">Click Me</button>
<p id="text">Original Text</p>

<script>
  function changeText() {
    document.getElementById("text").innerText = "Text Changed!";
  }
</script>
```

---

## **3. Vue 3 Basics**
Vue.js is a progressive JavaScript framework for building interactive web interfaces. It organizes code into reusable **components**.

### **3.1 Setting Up Vue 3**
To use Vue 3 in a project:
1. Install Vue via a CDN:
   ```html
   <script src="https://unpkg.com/vue@3"></script>
   ```
2. Or use a CLI tool like `npm` to set up a project:
   ```bash
   npm init vue@latest
   ```

---

## **4. Vue 3 Features**

### **4.1 Basic Component Structure**
```vue
<template>
  <div>
    <h1>{{ message }}</h1>
    <button @click="changeMessage">Click Me</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "Hello, Vue 3!"
    };
  },
  methods: {
    changeMessage() {
      this.message = "You clicked the button!";
    }
  }
};
</script>

<style>
h1 {
  color: green;
}
</style>
```

### **4.2 Composition API**
Vue 3 introduced the **Composition API** for better reusability and flexibility.

#### **Using `setup`**
The `setup` function is where all logic resides in the Composition API.
```vue
<template>
  <div>
    <h1>{{ counter }}</h1>
    <button @click="increment">Increase</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const counter = ref(0);

    function increment() {
      counter.value++;
    }

    return { counter, increment };
  }
};
</script>
```

- **`ref`**: Creates reactive variables (for primitive values like numbers and strings).
- **`reactive`**: Creates reactive objects or arrays.

### **4.3 Computed Properties**
`computed` is used for values derived from reactive data.
```vue
<template>
  <p>Base: {{ base }}</p>
  <p>Double: {{ double }}</p>
</template>

<script>
import { ref, computed } from 'vue';

export default {
  setup() {
    const base = ref(5);
    const double = computed(() => base.value * 2);

    return { base, double };
  }
};
</script>
```

### **4.4 Event Handling**
Vue uses the `@` directive to bind events.
```vue
<template>
  <button @click="handleClick">Click Me</button>
</template>

<script>
export default {
  methods: {
    handleClick() {
      console.log("Button was clicked!");
    }
  }
};
</script>
```

### **4.5 Conditional Rendering**
Conditionally render elements using `v-if` or `v-else`.
```vue
<template>
  <div v-if="isLoggedIn">Welcome back!</div>
  <div v-else>Please log in.</div>
</template>

<script>
export default {
  data() {
    return {
      isLoggedIn: false
    };
  }
};
</script>
```

### **4.6 Lists and Loops**
Use `v-for` to iterate over arrays.
```vue
<template>
  <ul>
    <li v-for="item in items" :key="item.id">{{ item.name }}</li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { id: 1, name: "Item 1" },
        { id: 2, name: "Item 2" }
      ]
    };
  }
};
</script>
```

### **4.7 Styling in Vue**
You can style Vue components using scoped styles to isolate styles to a specific component.
```vue
<template>
  <div class="box">Styled Box</div>
</template>

<style scoped>
.box {
  background-color: lightblue;
  padding: 20px;
  border: 1px solid blue;
}
</style>
```

---

## **5. Next Steps**
1. Practice building small projects combining HTML, CSS, JavaScript, and Vue 3.
2. Explore Vue 3’s advanced features like directives, plugins, and Vue Router.
3. Learn about state management using Vuex or Pinia.

---

This guide provides a solid foundation for mastering modern web development.
