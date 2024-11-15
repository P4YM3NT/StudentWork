# JavaScript Project: Enhanced Interactive Address Book

Welcome to the advanced version of your JavaScript Address Book project! This project will take the basic address book you previously created and add more functionality to make it persistent and feature-rich. The goal is to deepen your understanding of JavaScript concepts, including **search functions**, **editing entries**, and **JSON** handling. 

---

## 📝 Task Overview

Your task is to build an enhanced Address Book program that works through the console. In this version, the address book will allow the user to:

1. **Edit contact details** for existing entries.
2. **Search contacts** by name or phone number.
3. **Save contacts** to a JSON file to make them persistent.
4. **Load contacts** from the JSON file when the program starts.

---

## 🔄 Step-by-Step Instructions

To make this easier, let’s break down the tasks into smaller steps.

### Step 1: Set Up the Project

1. Create a new file called `addressBook.js` (or extend the file from the previous adress book).
2. Install the necessary dependencies:
3. In `addressBook.js`, import the required modules

<details>
<summary>Click to get help for which libraries to use</summary>

- `prompt-sync` for user input.
- `fs` (built-in Node.js module) for reading and writing files.

</details>

### Step 2: Initialize the Address Book
1. Define an empty array `addressBook` to store contact information.
2. Write a function `loadAddressBook()` that reads from a file called `contacts.json` and loads the contact data into `addressBook`. Make sure to check if the file exists before trying to read it.

### Step 3: Save the Address Book
1. Write a function `saveAddressBook()` that saves the `addressBook` array to `contacts.json` as a JSON file.
2. Call this function after every operation (adding, editing, or deleting contacts) to ensure the data is always up-to-date.

### Step 4: Edit a Contact
1. Create a function `editContact()` that allows the user to update an existing contact's name, address, and phone number.
2. If the contact is found, prompt the user for the new values and update the contact in the addressBook.
3. After editing, save the updated address book by calling `saveAddressBook()`.

### Step 5: Search for a Contact
1. Write a function `searchContacts()` that allows the user to search for a contact by name or phone number.
2. If matching contacts are found, display them; if no match is found, show a message saying so.

### Final Task: Test the Program
1. Test all the features (add, view, delete, edit, search) to ensure they work as expected.
2. Make sure the contacts are saved to and loaded from the contacts.json file.
3. Debug any issues you encounter during testing.

---

## ✅ Example Solution

<details>
<summary>Click to reveal the solution</summary>

Here’s an example of how your code might look:

```javascript
const prompt = require('prompt-sync')();
const fs = require('fs');

// Path for the JSON file
const filePath = './addressBook.json';

// Initialize the address book array
let addressBook = [];

// Load contacts from the JSON file if it exists
function loadContacts() {
    if (fs.existsSync(filePath)) {
        const data = fs.readFileSync(filePath);
        addressBook = JSON.parse(data);
    }
}

// Save contacts to the JSON file
function saveContacts() {
    fs.writeFileSync(filePath, JSON.stringify(addressBook, null, 2));
    console.log("Contacts saved to file.");
}

// Function to add a new contact
function addContact(name, address, phone) {
    const contact = { name, address, phone };
    addressBook.push(contact);
    saveContacts();
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
        saveContacts();
        console.log(`${name} has been removed from the address book.`);
    } else {
        console.log(`${name} was not found in the address book.`);
    }
}

// Function to edit a contact's details
function editContact(name, newDetails) {
    const contact = addressBook.find(contact => contact.name.toLowerCase() === name.toLowerCase());
    if (contact) {
        Object.assign(contact, newDetails);
        saveContacts();
        console.log(`${name}'s details have been updated.`);
    } else {
        console.log(`${name} was not found in the address book.`);
    }
}

// Function to search contacts by name or phone
function searchContact(query) {
    query = query.toLowerCase();
    const results = addressBook.filter(contact =>
        contact.name.toLowerCase().includes(query) || 
        contact.phone.includes(query)
    );
    if (results.length > 0) {
        results.forEach(contact => {
            console.log(`Found: ${contact.name} - Address: ${contact.address}, Phone: ${contact.phone}`);
        });
    } else {
        console.log("No matching contacts found.");
    }
}

// Main interactive function
function addressBookConsole() {
    loadContacts();
    let action;
    while (action !== "quit") {
        action = prompt("Choose an action: add, view, delete, edit, search, or quit").toLowerCase();
        
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
            case "edit":
                const editName = prompt("Enter the name of the contact to edit:");
                const newAddress = prompt("Enter new address (leave blank to keep current):");
                const newPhone = prompt("Enter new phone number (leave blank to keep current):");
                const newDetails = {};
                if (newAddress) newDetails.address = newAddress;
                if (newPhone) newDetails.phone = newPhone;
                editContact(editName, newDetails);
                break;
            case "search":
                const query = prompt("Enter name or phone to search:");
                searchContact(query);
                break;
            case "quit":
                console.log("Exiting the Address Book.");
                break;
            default:
                console.log("Invalid action. Please choose add, view, delete, edit, search, or quit.");
        }
    }
}

// Start the program
addressBookConsole();
```
</details>

---

## 📚 Additional Challenges

1. Add Sorting: Sort the contacts by name before displaying them in viewContacts.
2. Add Validation: Ensure that phone numbers and names are in the correct format before adding or editing contacts.
3. Group Contacts by Initial: Group and display contacts alphabetically by their first initial.

## Happy coding! 🎉