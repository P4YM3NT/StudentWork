# JavaScript Basics for Node.js Development

Welcome to the JavaScript Basics guide! This document is designed to help you learn the fundamental concepts of JavaScript in the context of Node.js. Each section includes explanations, code examples, and exercises to reinforce your learning. 

## Table of Contents
1. [Introduction](#introduction)
2. [Variables](#variables)
3. [Data Types](#data-types)
4. [Operators](#operators)
5. [Control Structures](#control-structures)
    - [If Statements](#if-statements)
    - [Switch Statements](#switch-statements)
6. [Loops](#loops)
7. [Functions](#functions)
8. [Objects](#objects)
9. [Arrays](#arrays)
10. [Modules and Exports](#modules-and-exports)

---

## 1. Introduction

In this guide, you'll cover the basics of JavaScript specifically for back-end development with Node.js. Basic concepts in JavaScript are universal, but we’ll skip aspects focused on the browser and DOM manipulation at the moment.

---

## 2. Variables

Variables store data values that we can use and manipulate in our code. There are 3 different types that can be used `var`, `let`, `const`.

#### 1. `var`
- **Scope**: Function-scoped, meaning it's only available within the function in which it's declared.
- **Reassignment**: Yes, you can reassign `var` variables.

#### 2. `let`
- **Scope**:  Block-scoped, which means it's limited to the block, statement, or expression where it’s defined.
- **Reassignment**: Yes, you can reassign `let` variables.

#### 3. `const`
- **Scope**:  Block-scoped, like `let`.
- **Reassignment**: No, `const` variables cannot be reassigned after their initial declaration. However, if a `const` variable points to an object, properties of that object can still be modified.

### Syntax
```javascript
// Declaring variables
let name = "John";      // Block-scoped
const age = 25;         // Block-scoped, immutable
var isActive = true;    // Function-scoped (legacy)
```

### Exercise

1. Create a variable called `companyName` and assign it a string value of your choice.
2. Declare a constant called `yearFounded` with a numeric value.
3. Try reassigning `yearFounded` and note what happens.
4. Declare a `let` variable named `companyLocation` and assign it a string value representing a city.
5. Inside an `if` block, try reassigning `companyLocation` to a different city and log the result both inside and outside the block.
6. Declare a `var` variable called `isPublic` and assign it a boolean value (`true` or `false`). Test its scope by logging it inside and outside a function.

### Example Code

<details>
  <summary>Click to see the solution</summary>

  ```javascript
  // Step 1
  let companyName = "Tech Solutions";

  // Step 2
  const yearFounded = 2020;

  // Step 3 - Attempting to reassign yearFounded
  // yearFounded = 2021; // This will throw an error: "Assignment to constant variable."

  // Step 4
  let companyLocation = "New York";

  if (true) {
      companyLocation = "San Francisco";
      console.log("Inside block:", companyLocation); // San Francisco
  }
  console.log("Outside block:", companyLocation); // San Francisco

  // Step 6
  function checkPublicStatus() {
      var isPublic = true;
      console.log("Inside function:", isPublic); // true
  }
  checkPublicStatus();
  console.log("Outside function:", isPublic); // ReferenceError: isPublic is not defined
```
</details>

---

## 3. Data Types

JavaScript has several data types that can be classified into two categories: **primitive** and **non-primitive**. Primitive types are immutable and include `strings`, `numbers`, `booleans`, `undefined`, `null`. Non-primitive types (also known as reference types) include objects and arrays.

#### Primitive Data Types

1. **String**
   - A sequence of characters used to represent text. Strings must be wrapped in quotes (`""` or `''`), and they can contain letters, numbers, spaces, and symbols.
   - Example: `"Hello, world!"`, `'1234'`

   ```javascript
   const greeting = "Hello, world!"; // string

2. **Number**
   - Used for any type of number, including integers and floating-point numbers.
   - Example: `42`, `3.14`, `-100`

   ```javascript
   const age = 30; // number
   const pi = 3.14; // floating-point number

3. **Boolean**
   - Represents a logical entity and can have only two values: true or false. Useful for conditional statements and logic.
   - Example: `true`, `false`

   ```javascript
   const isMember = true; // boolean

4. **Undefined**
   - A variable that has been declared but has not yet been assigned a value is automatically undefined.
   - Example: `undefined`

   ```javascript
   let score; // undefined

5. **Null**
   - Represents an explicitly empty or non-existent value. Unlike undefined, null is assigned intentionally.
   - Example: `null`

   ```javascript
   const emptyValue = null; // null

#### Non-Primitive Data Types

1. **Object**
   - An object is a collection of key-value pairs. It can store multiple values and more complex structures. Objects are a fundamental part of JavaScript, and we will cover them in greater detail later.
   
   ```javascript
   const person = { name: "Alice", age: 30 }; // Object

2. **Array**
   - An array is an ordered list of values. Each value (element) has a numeric index, starting at 0. Arrays are also a type of object.
     
   ```javascript
   const colors = ["red", "green", "blue"]; // Array

