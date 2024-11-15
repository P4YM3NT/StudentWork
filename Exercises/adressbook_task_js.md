# JavaScript Final Project: Interactive Address Book

Welcome to the final project of this JavaScript basics course! 🎉 This worksheet will guide you through creating an interactive **Address Book** that you can use in the console. This will test your understanding of JavaScript variables, conditions, loops, and functions. Good luck!

---

## 📝 Task Overview

Your task is to build a simple Address Book program that works through the console. It should allow the user to:

1. **Add new contacts** with a name, address, and phone number.
2. **Delete contacts** by name.
3. **View all contacts** in the address book.

---

## 🔄 Step-by-Step Instructions

To make this easier, let’s break down the task into smaller steps.

### Step 1: Set up the Address Book array

1. Create an empty array called `addressBook`. This will store each contact as an object.

### Step 2: Create a function to add a new contact

1. Write a function `addContact(name, address, phone)` that takes in three arguments (name, address, and phone number).
2. Inside the function, create an object with these details and add it to the `addressBook` array.

### Step 3: Create a function to view all contacts

1. Write a function `viewContacts()` that loops through the `addressBook` array and logs each contact’s details to the console.

### Step 4: Create a function to delete a contact

1. Write a function `deleteContact(name)` that searches for a contact by name.
2. If found, remove that contact from the `addressBook` array. If not found, display a message saying that the contact doesn’t exist.

### Step 5: Make it interactive

1. Use a suitable library to make the program interactive so that the user can enter text into the console and the program uses it.

---

## 💡 Helpful Tips

<details>
<summary>Click to reveal tips!</summary>

1. **Use arrays and objects together**: Store each contact as an object with `name`, `address`, and `phone` properties.
2. **Loop for viewing contacts**: A simple `for` loop or `forEach` method can help to display all contacts.
3. **Array methods**: Use methods like `.push()` to add, and `.splice()` to delete from the array.
4. **Finding items**: The `.findIndex()` method can help locate a contact by name.
5. **Testing**: After each function, test it in the console to ensure it works as expected.

</details>

---

## ✅ Example Solution

<details>
<summary>Click to reveal the solution</summary>

Here’s an example of how your code might look:

```javascript
var prompt = require('prompt-sync')();

// Initialize an empty address book array
const addressBook = [];

// Function to add a new contact
function addContact(name, address, phone) {
    const contact = { name, address, phone };
    addressBook.push(contact);
    console.log(`${name} has been added to the address book.`);
}

// Function to view all contacts
function viewContacts() {
    if (addressBook.length === 0) {
        console.log("The address book is empty.");
    } else {
        console.log("Address Book:");
        addressBook.forEach((contact, index) => {
            console.log(`${index + 1}. ${contact.name} - Address: ${contact.address}, Phone: ${contact.phone}`);
        });
    }
}

// Function to delete a contact by name
function deleteContact(name) {
    const index = addressBook.findIndex(contact => contact.name.toLowerCase() === name.toLowerCase());
    if (index !== -1) {
        addressBook.splice(index, 1);
        console.log(`${name} has been removed from the address book.`);
    } else {
        console.log(`${name} was not found in the address book.`);
    }
}

// Main interactive function
function addressBookConsole() {
    let action;
    while (action !== "quit") {
        action = prompt("Choose an action: add, view, delete, or quit: ").toLowerCase();
        
        switch (action) {
            case "add":
                const name = prompt("Enter name:");
                const address = prompt("Enter address:");
                const phone = prompt("Enter phone number:");
                addContact(name, address, phone);
                break;
            case "view":
                viewContacts();
                break;
            case "delete":
                const deleteName = prompt("Enter the name of the contact to delete:");
                deleteContact(deleteName);
                break;
            case "quit":
                console.log("Exiting the Address Book.");
                break;
            default:
                console.log("Invalid action. Please choose add, view, delete, or quit.");
        }
    }
}

// Start the program
addressBookConsole();
