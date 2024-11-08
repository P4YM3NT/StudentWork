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

### Introduction

In this guide, you'll cover the basics of JavaScript specifically for back-end development with Node.js. Basic concepts in JavaScript are universal, but we’ll skip aspects focused on the browser and DOM manipulation at the moment.

---

### Variables

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

#### Syntax
```javascript
// Declaring variables
let name = "John";      // Block-scoped
const age = 25;         // Block-scoped, immutable
var isActive = true;    // Function-scoped (legacy)
