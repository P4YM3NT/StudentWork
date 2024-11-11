# JavaScript Basics for Node.js Development

Welcome to the JavaScript Basics guide! This document is designed to help you learn the fundamental concepts of JavaScript in the context of Node.js. Each section includes explanations, code examples, and exercises to reinforce your learning. 

## Table of Contents
1. [Introduction](#Introduction)
2. [Variables](##Variables)
3. [Data Types](#Data-Types)
4. [Operators](#Operators)
5. [Control Structures](#Control-Structures)
    - [If Statements](#if-statements)
    - [Switch Statements](#switch-statements)
6. [Loops](#loops)
7. [Functions](#Functions)
8. [Objects](#Objects)
9. [Arrays](#Arrays)
10. [Modules and Exports](#modules-and-exports)

---

## 1. Introduction

In this guide, you'll cover the basics of JavaScript specifically for back-end development with Node.js. Basic concepts in JavaScript are universal, but we’ll skip aspects focused on the browser and DOM manipulation at the moment.

---

## Prerequisit

#### Print

In JavaScript, `console.log` is a method used to print or output information to the browser's console or local terminal (nodejs). It’s very helpful for `debugging`, as it lets developers check the values of variables, test expressions, and track the flow of a `program`.

#### How to Use console.log

To use `console.log`, simply call it with the information you want to display. For example:

```javascript
console.log("Hello, World!")
```

This line will print `Hello, World!` to the console.

You can also print variables and set a string infront of it for better understanding.

```javascript
let age = 18;

// print variables only
console.log(age);

//print variables with a string infront.
console.log("My Age is: ", age);
```

Keep in mind to set a comma after the string, otherwise it would generate an error.

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

## 3. Data-Types

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

<br>

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

<br>

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

<br>

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

--- 

## 5. Control Structures

Control structures allow us to control the flow of a program. By using them, we can decide which code should be executed based on conditions or repeat actions under specific circumstances.

There are several types of control structures:

1. Conditional Statements (`if`, `else if`, `else`, `switch`)
2. Loops ( `for`, `while`, `do...while`)

### Conditional Statements

Conditional statements allow us to execute code only when certain conditions are true.

#### 1. If Statement

The `if` statement checks a `condition`, and if the condition is `true`, it executes the code inside the block. If the condition is `false`, it skips to the `next` part of the code.

#### Syntax

```javascript
if (condition) {
    // Code to execute if condition is true
}
```

#### Example

```javascript
let age = 20;
if (age >= 18) {
    console.log("Adult");
} else {
    console.log("Minor");
}
```
#### 2. If...Else Statement

The `if...else` statement provides an alternative action if the initial condition is `false`.

#### Syntax

```javascript
if (condition) {
    // Code to execute if condition is true
} else {
    // Code to execute if condition is false
}
```
#### Example

```javascript
let temperature = -5;
if (temperature > 0) {
    console.log("Above freezing");
} else {
    console.log("Below freezing");
}
```

#### 3. If...Else If...Else Statement

With `if...else if...else`, we can check multiple conditions in sequence. Once a condition is `true`, it will execute the corresponding block and ignore the rest.

#### Syntax

```javascript
if (condition) {
    // Code to execute if condition is true
} else if (secondCondition) {
    // Code to execute if condition is false and secondCondition is true
} else if (thirdCondition) {
    // Code to execute if condition and secondCondition are false, but thirdCondition is true
} else {
    // Code to execute if all previous conditions are false
}
```

#### Example

```javascript
let temperature = 30;

if (temperature > 30) {
    console.log("It's hot outside.");
} else if (temperature >= 20 && temperature <= 30) {
    console.log("The weather is warm.");
} else if (temperature >= 10 && temperature < 20) {
    console.log("It's a bit chilly.");
} else {
    console.log("It's cold outside.");
}
```

<br>

### 2. The Switch Statement

The `switch` statement is useful when you have `multiple` possible values for a variable and want to execute different code based on each `value`.

#### Syntax

```javascript
switch (expression) {
    case value1:
        // Code for value1
        break;
    case value2:
        // Code for value2
        break;
    // Add more cases as needed
    default:
        // Code if none of the cases match
}
```

#### Example
```javascript
let day = "Monday";

switch (day) {
    case "Monday":
        console.log("Start of the work week!");
        break;
    case "Friday":
        console.log("Almost the weekend!");
        break;
    case "Saturday":
    case "Sunday":
        console.log("It's the weekend!");
        break;
    default:
        console.log("It's a regular weekday.");
}
```

In this example, if `day` is `"Monday"`, it will print "Start of the work week!" The `break` keyword prevents the execution from moving to the next case. The `default` case runs if none of the other cases match.

<br>

### 3. Loops

`Loops` let us execute a block of code multiple times until a specific `condition` is met.

#### For Loop

The `for` loop is ideal when you know the exact number of iterations you want.

#### Syntax
```javascript
for (initialization; condition; increment) {
    // Code to repeat
}
```

Increment is the `part` that changes the loop variable `each` time the loop runs. 

#### Example
```javascript
for (let i = 0; i < 5; i++) {
    console.log(i); // Outputs numbers from 0 to 4
}
```

As we have learned before, the `++` operator will increment `i` by 1.

<br>

#### While Loop

The `while` loop is useful when you `don’t` know the exact number of repetitions but need to loop until a condition becomes false.

#### Syntax
```javascript
while (condition) {
    // Code to repeat
}
```

#### Example
```javascript
let count = 0;
while (count < 3) {
    console.log("Count is:", count);
    count++;
}
```
<br>

#### Do...While Loop

The `do...while` loop guarantees the code runs at least `once`, as it checks the condition after executing the block.

#### Syntax
```javascript
do {
    // Code to execute at least once
} while (condition);
```

#### Example
```javascript
let number = 5;
do {
    console.log("Number is:", number);
    number--;
} while (number > 0);
```
<br>

### Exercises

1. Write an if statement to check if a number is positive, negative, or zero.
2. Write a switch statement to categorize a day as a "Weekday" or "Weekend".
3. Use a for loop to print numbers from 1 to 10.
4. Create a while loop that prints "Hello" 5 times.

### Example Code

<details>
  <summary>Click to see the solution</summary>

  ```javascript
    // Example solution

    // Exercise 1
    let number = -3;

    if (number > 0) {
    console.log("Positive");
    } else if (number < 0) {
        console.log("Negative");
    } else {
        console.log("Zero");
    }

    //Exercise 2
    let day = "Saturday";

    switch (day) {
        case "Monday":
        case "Tuesday":
        case "Wednesday":
        case "Thursday":
        case "Friday":
            console.log("Weekday");
            break;
        case "Saturday":
        case "Sunday":
            console.log("Weekend");
            break;
        default:
            console.log("Invalid day");
    }

    //Exercise 3
    for (let i = 1; i <= 10; i++) {
        console.log(i);
    }

    //Exercise 4
    let count = 0;

    while (count < 5) {
        console.log("Hello");
        count++;
    }    
  ```
</details>

---

## 6. Functions

In JavaScript, a `function` is a reusable block of code that performs a specific `task` or calculates a value. Functions allow you to organize your code, `reduce` repetition, and make it easier to `understand` and `maintain`.

### Anatomy of a Function

A basic function has these components:

1. `Function keyword`: This signals the start of a function.
2. `Name`: This identifies the function so it can be called elsewhere in your code.
3. `Parameters`: Variables listed inside parentheses after the function name. They act as placeholders for values that will be passed to the function when it is called.
4. `Function body`: This is enclosed in curly braces { } and contains the code that runs when the function is called.
5. `Return statement (optional)`: This specifies the output or result of the function. When the function is called, it will return this value.

### Syntax

Here is the general syntax for defining a function in JavaScript:

```javascript
function greet(name) {
    // Code to execute comes here
    let result = name;

    return result; // Optional: sends back a value
}
```

- `greet`: The name of the function.
- `name`: Parameter Value passed into the function, used within its code. You can name parameters however you like.
- `return`: (Optional) Sends back a value to where the function was called.

### Calling a function

To use (or “call”) the function, you write the function name followed by parentheses, including any arguments that match the parameters.

```javascript
console.log(greet("Luca")); // Outputs: Hello, Luca!
```

### Types of Functions

In JavaScript, there are several ways to define functions:

1. Function Declarations:
```javascript
function greet(name) {
    let result = name;

    return result;
}
```

- Use Case: Use function declarations when you don’t need to store the function in a variable and want the function to be available throughout the scope.
- Named Functions: Function declarations must have a name, which makes them ideal for functions that need to be called multiple times.
- Not for Dynamic Assignments: Function declarations cannot be assigned to variables or passed around like function expressions, so they are better when the function's primary role is to be invoked by name.

2. Function Expressions:
```javascript
const greeting = function(name) {
    let result = name;

    return result;
}
```

- Use Case: Use function expressions when you need to store a function in a variable, pass it as an argument, or return it from another function.
- Flexible Invocation: Since they are stored in variables, function expressions can be invoked only after they are assigned to a variable, unlike function declarations that can be used before they are defined.
- Can Be Assigned to Variables or Objects: You can store function expressions in variables, arrays, or even objects for later use.

3. Arrow Functions (ES6):
```javascript
const greeting = (name) => {
    let result = name;

    return result;
}
```

- Arrow Functions are `nameless functions`, they should be used when it's not neccessary to use the function again. ( You need a name to call a function )
- Use arrow functions for short, single-use functions, especially in callbacks (.map(), .filter(), ...), where you don’t need a named function.
- You don't need to safe them in a const like in the example.

### Exercise

1. Write a function called square that takes a number as an argument and returns the square of that number.
2. Write it as an Arrow Function (ES6)
3. Print both functions with the parameter `5`

### Example Code

<details>
  <summary>Click to see the solution</summary>

  ```javascript
    // Example solution

    // Exercise 1
    function square(num1) {
        let result = num1 * num1
        console.log("Function Declaration", result)

        return result;
    }

    //Exercise 2
    const square = (num1) => {
        let result = num1 * num1
        console.log("Arrow Function", result)

        return result;
    }
  ```
</details>

---

## 7. Objects

In JavaScript, **objects** are collections of related data organized as key-value pairs. They are powerful because they allow us to represent real-world entities with properties and values. Objects can store not only values (like numbers and strings) but also functions, making them flexible and central in JavaScript programming.

### Structure of an Object

An object is defined with curly braces `{ }`, and each property inside consists of:

- **Key**: The name of the property (e.g., `brand`, `model`, `year`).
- **Value**: The value assigned to the property, which could be any data type (e.g., strings, numbers, or even functions).

### Example

Here’s an example of an object representing a car:

```javascript
const car = {
    brand: "Toyota",
    model: "Corolla",
    year: 2020
};
```

- **Keys**: `brand`, `model`, and `year`
- **Values**: `"Toyota"`, `"Corolla"`, and `2020`

### Accessing Object Properties

To access the values of an object, we use either **dot notation** (`car.brand`) or **bracket notation** (`car["brand"]`).

```javascript
console.log(car.brand);  // Outputs: Toyota
console.log(car["year"]); // Outputs: 2020
```

### Adding and Deleting Properties

#### 1. Inserting (or Adding) Properties
To insert a new key-value pair into an object, you can use:

- **Dot notation**: `object.key = value`
- **Bracket notation**: `object["key"] = value`

#### 2. Deleting Properties
To delete a property, use the `delete` keyword:

- `delete object.key`
- `delete object["key"]`

#### Example of Adding and Deleting Properties

```javascript
const user = {
    name: "Alice",
    age: 25,
    isStudent: true
};

// Adding a new property
user.country = "Germany"; // Dot notation
user["hobby"] = "Reading"; // Bracket notation

console.log(user);
// Output: { name: "Alice", age: 25, isStudent: true, country: "Germany", hobby: "Reading" }

// Deleting a property
delete user.hobby; // Removes the 'hobby' property
delete user["country"]; // Removes the 'country' property

console.log(user);
// Output: { name: "Alice", age: 25, isStudent: true }
```

### Exercise

Let's put this into practice by creating a `user` object and writing a function to print each property.

1. Create an object called `user` with the properties `name`, `age`, and `isStudent`.
2. Write a function to print each property of the `user` object.

### Example Code

<details>
  <summary>Click to see the solution</summary>

  ```javascript
    // Example solution

    // Step 1: Create the user object
    const user = {
        name: "Alice",
        age: 25,
        isStudent: true
    };
    
    // Step 2: Write a function to print each property
    function printUserProperties(obj) {
        for (let key in obj) {
            console.log(`${key}: ${obj[key]}`);
        }
    }
    
    printUserProperties(user);
    
    /* Expected output:
    * name: Alice
    * age: 25
    * isStudent: true
    */
  ```
</details>

---

## 8. Arrays

Arrays are ordered collections of values that allow us to store multiple values in a single variable. They are a core part of JavaScript and are especially useful when dealing with lists of data, such as lists of names, numbers, or objects. Each item in an array has a specific position, known as its index, which starts at `0`.

### Description

An array in JavaScript can store any data type, including strings, numbers, objects, and even other arrays (nested arrays). Arrays are flexible and provide many built-in methods to manipulate and access the stored values. 

Arrays are particularly useful when we need to:

- Organize and manage data in a structured way.
- Access specific elements by their index.
- Iterate over a set of values, such as through loops.

### Syntax

To create an array, we use square brackets `[ ]` and list the values inside, separated by commas.

```javascript
const arrayName = [value1, value2, value3, ...];
```

- Index: Each value in the array has an index, starting at 0 for the first element.
- Length: The number of elements in an array is known as its length, accessed using arrayName.length.

### Example

Here’s an example of an array containing a list of fruits:

```javascript
const fruits = ["apple", "banana", "cherry"];

console.log(fruits[0]);  // Outputs: apple
console.log(fruits[1]);  // Outputs: banana
console.log(fruits[2]);  // Outputs: cherry

// Array values: "apple", "banana", "cherry"
// Indexes: 0, 1, 2
// Accessing elements: We use the index to access elements in the array, such as fruits[0] for "apple".
```

### Exercises

Let’s put this into practice by working with your favorite colors:

1. Create an array of your favorite colors.
2. Write a loop to print each color in the array.

### Example Code

<details>
    <summary>Click to see the solution</summary>
    
```javascript
// Step 1: Create an array of favorite colors
const favoriteColors = ["blue", "green", "purple"];

// Step 2: Use a loop to print each color
for (let i = 0; i < favoriteColors.length; i++) {
    console.log(favoriteColors[i]);
}

// Expected output:
// blue
// green
// purple    
```
</details>

---

## 9. Advanced Loops: forEach, map, and More

### ForEach

#### Description

forEach is an array method that executes a provided function once for each array element, in the original order. It’s typically used when you need to perform an operation on each item without modifying the array itself.

#### Syntax

```javascript
array.forEach(function(element, index, array) {
  // Code to be executed for each element
});
```

- `element`: The current element being processed in the array.
- `index` (optional): The index of the current element.
- `array` (optional): The array that forEach was called on.

#### Example
```javascript
const numbers = [1, 2, 3, 4, 5];

numbers.forEach(function(number) {
  console.log(number * 2); // Output: 2, 4, 6, 8, 10
});

```
In this example, forEach loops over each element in the numbers array and logs its double to the console.

<br>

### Map 

#### Description

map is another array method that creates a new array populated with the results of calling a provided function on every element in the calling array. It's useful when you want to transform or modify data in an array without changing the original array.

#### Syntax

```javascript
const newArray = array.map(function(element, index, array) {
  // Return the transformed element for the new array
  return transformedElement;
});
```

- `element`: The current element being processed in the array.
- `index` (optional): The index of the current element.
- `array` (optional): The array that map was called on.
- Return value: A new array with the results of applying the function to each element.

#### Example

```javascript
const numbers = [1, 2, 3, 4, 5];

const doubledNumbers = numbers.map(function(number) {
  return number * 2; // Transforms each number into its double
});

console.log(doubledNumbers); // Output: [2, 4, 6, 8, 10]
```
Here, map creates a new array where each number from the original array is doubled, leaving the original array unchanged.


### Exercises


1. Create an array of strings representing different fruits. Use forEach to print each fruit in uppercase letters.
2. Given an array of numbers, use map to create a new array where each number is squared (e.g., [1, 2, 3] becomes [1, 4, 9]).
3. Create an array of numbers. Use forEach to print both the index and value of each element in the format: Index: 0, Value: 1.
4. Given an array of objects representing books (each with a title and author property), use map to create a new array containing only the titles of the books.

### Example Code

<details>
    <summary>Click to see the solution</summary>

```javascript

//Exercise 1
const fruits = ["apple", "banana", "cherry", "date", "elderberry"];

fruits.forEach(function(fruit) {
  console.log(fruit.toUpperCase());
});

//Exercise 2
const numbers = [1, 2, 3, 4, 5];

const squaredNumbers = numbers.map(function(number) {
  return number * number;
});

console.log(squaredNumbers);

//Exercise 3

const numbers = [10, 20, 30, 40, 50];

numbers.forEach(function(number, index) {
  console.log(`Index: ${index}, Value: ${number}`);
});

//Exercise 4
const books = [
  { title: "The Great Gatsby", author: "F. Scott Fitzgerald" },
  { title: "1984", author: "George Orwell" },
  { title: "To Kill a Mockingbird", author: "Harper Lee" },
  { title: "Pride and Prejudice", author: "Jane Austen" }
];

const bookTitles = books.map(function(book) {
  return book.title;
});

console.log(bookTitles);
```
    
</details>

---

### Next Chapter: Create an Adressbook
