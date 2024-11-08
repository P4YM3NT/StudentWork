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

In this guide, you'll cover the basics of JavaScript specifically for back-end development with Node.js. Basic concepts in JavaScript are universal, but we’ll skip aspects focused on the browser and DOM manipulation.

---

### Variables

Variables store data values that we can use and manipulate in our code.

#### Syntax
```javascript
// Declaring variables
let name = "John";      // Block-scoped
const age = 25;         // Block-scoped, immutable
var isActive = true;    // Function-scoped (legacy)