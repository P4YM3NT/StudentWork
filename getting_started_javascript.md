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

<br>

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

<br>

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

<br>

#### Non-Primitive Data Types

1. **Object**
   - An object is a collection of key-value pairs. It can store multiple values and more complex structures. Objects are a fundamental part of JavaScript, and we will cover them in greater detail later.
   
   ```javascript
   const person = { name: "Alice", age: 30 }; // Object
   ```
2. **Array**
   - An array is an ordered list of values. Each value (element) has a numeric index, starting at 0. Arrays are also a type of object.
     
   ```javascript
   const colors = ["red", "green", "blue"]; // Array
   ```
   
### Exercise
If you don't know how to log the `type`, google it. If you can't find anything, click on the hint.

1. Create `variables` of each type: `string`, `number`, `boolean`, `undefined`, `null`, `object`, and `array`.
2. Log each `variable` to the console to observe its `type` and `value`.

<details>
  <summary>Click for a hint!</summary>

  ```javascript
  // to get the type of a variable, you can use the typeof operator.

  let test = 1;
  console.log(typeof test);

  ```
</details>

### Example Code

<details>
  <summary>Click to see the solution</summary>

  ```javascript
    // Example solution

    /* There isn't any right or wrong, you can declare the variables with every variable type ( var, let, const).
    *  Keep in mind that using var isn't recommended anymore.
    */
    const companyName = "Tech Solutions"; // String
    const companyAge = 10; // Number
    const isActive = true; // Boolean
    let companyRevenue; // Undefined
    const noValue = null; // Null
    const companyDetails = { name: "Tech Solutions", founded: 2010 }; // Object
    const departments = ["HR", "Engineering", "Sales"]; // Array

    // There isn't any right or wrong, you can log it at once like in the example or seperate the console.log for every variable.
    console.log(typeof companyName, typeof companyAge, typeof isActive, typeof companyRevenue, typeof noValue, typeof companyDetails, typeof departments);
  ```
</details>

---

<br>

## 4. Operators

Operators in JavaScript are used to perform various operations on variables and values. Here’s a quick guide to the most commonly used operators:

### Arithmetic Operators
Arithmetic operators are used to perform `mathematical` calculations.

1. **Addition (`+`)**: Adds two values.
   ```javascript
   let sum = 5 + 3; // Output: 8

2. **Substraction (`-`)**: Subtracts one value from another.
   ```javascript
   let difference = 10 - 4; // Output: 6

3. **Multiplication (`*`)**: Multiplies two values.
   ```javascript
   let product = 4 * 3; // Output: 12

4. **Division (`/`)**: Divides one value by another.
   ```javascript
   let quotient = 12 / 3; // Output: 4

5. **Modulus (`%`)**: Returns the remainder when one value is divided by another. Often used to check if a number is even or odd.
   ```javascript
   let remainder = 10 % 3; // Output: 1
   // 10 : 3 would be 3,33.... but modulo count the rest of the positive divison 9:3 = 3 / rest is 1 to get 10
   // 4 % 2 would be rest 0
   // 5 % 2 would be rest 1

### Assignment Operators
Assignment operators `assign` values to variables.

1. **Simple Assigment (`=`)**: Assigns a value to a variable.
   ```javascript
   let x = 10;

2. **Addition Assigment (`+=`)**: Adds a value to the variable.
   ```javascript
   x += 5; // Equivalent to x = x + 5; x is now 15

3. **Subtraction Assigment (`-=`)**: Subtracts a value from the variable.
   ```javascript
   x -= 3; // Equivalent to x = x - 3; x is now 12

4. **Multiplication Assigment (`*=`)**: Multiplies the variable by a value.
   ```javascript
   x *= 2; // Equivalent to x = x * 2; x is now 24

5. **Division Assigment (`/=`)**:  Divides the variable by a value.
   ```javascript
   x /= 6; // Equivalent to x = x / 6; x is now 4

### Comparison Operators
Comparison operators are used to compare values and return a boolean result `true` or `false`.

1. **Equal (`==`)**: Checks if two values are equal (type conversion is allowed).
   ```javascript
   console.log(5 == "5"); // Output: true

2. **Strict Equal (`===`)**: Checks if two values are equal and of the same type.
   ```javascript
   console.log(5 === "5"); // Output: false

3. **Not Equal (`!=`)**: Checks if two values are not equal.
   ```javascript
   console.log(5 != 3); // Output: true

4. **Strict Not Equal (`!==`)**: Checks if two values are not equal or not of the same type.
   ```javascript
   console.log(5 !== "5"); // true

5. **Greater Than (`>`)**: Checks if the left value is greater than the right.
   ```javascript
   console.log(10 > 5); // true

6. **Less Than (`<`)**: Checks if the left value is less than the right.
   ```javascript
   console.log(5 < 10); // true

7. **Greater Than or Equal (`>=`)**: Checks if the left value is greater than or equal to the right.
   ```javascript
   console.log(10 >= 10); // true

8. **Less Than or Equal (`<=`)**: Checks if the left value is less than or equal to the right.
   ```javascript
   console.log(5 <= 10); // true

### Logical Operators
Logical operators are used to combine multiple `boolean expressions`.

1. **AND (`&&`)**: Returns true if both expressions are true.
   ```javascript
   console.log(true && false); // false

2. **OR (`||`)**: Returns true if at least one expression is true.
   ```javascript
   console.log(true || false); // true

3. **NOT (`!`)**: Inverts the value of an expression.
   ```javascript
   console.log(!true); // false

<br>
   
### Exercise 1: Simple Arithmetic Operations
If you don't know how to log the `type`, google it. If you can't find anything, click on the hint.

1. Declare two `variables`, a and b, and assign them `numeric values` of your choice.
2. Perform and `log` the following operations using these variables above:
    - `Addition`
    - `Subtraction`
    - `Multiplication`
    - `Division`
    - `Modulus`
    

### Example Code

<details>
  <summary>Click to see the solution</summary>

  ```javascript
    // Example solution

    let a = 8;
    let b = 4;

    console.log(a + b); // Addition
    console.log(a - b); // Subtraction
    console.log(a * b); // Multiplication
    console.log(a / b); // Division
    console.log(a % b); // Modulus
  ```
</details>

<br>

### Exercise 2: Modulus and Odd/Even Check

1. Declare a `variable number` and assign it a `random` integer.
2. Use the `modulus` operator (%) to check if the number is `even` or `odd`.

    - `Addition`
    - `Subtraction`
    - `Multiplication`
    - `Division`
    - `Modulus`
3. Log whether the number is `Even` or `Odd`.    

### Example Code

<details>
  <summary>Click to see the solution</summary>

  ```javascript
    // Example solution

    let a = 8;
    let b = 4;

    console.log(a + b); // Addition
    console.log(a - b); // Subtraction
    console.log(a * b); // Multiplication
    console.log(a / b); // Division
    console.log(a % b); // Modulus
  ```
</details>

Exercise 2: Modulus and Odd/Even Check
Declare a variable number and assign it a random integer.
Use the modulus operator (%) to check if the number is even or odd.
Log whether the number is "Even" or "Odd".
Example Solution:

javascript
Code kopieren
let number = 17;

if (number % 2 === 0) {
    console.log("Even");
} else {
    console.log("Odd");
}

