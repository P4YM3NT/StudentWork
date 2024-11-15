
# Building a RESTful API with Node.js and Express

In this guide, we'll explore the fundamentals of RESTful APIs, CRUD operations, and essential components for structuring your API using Node.js and Express. By the end, you'll create a simple Address Book API where users can add, find, edit, and delete entries. We’ll also cover how to use **Postman** to test the API.

---

## Table of Contents

1. [Introduction to RESTful APIs](#introduction-to-restful-apis)
2. [CRUD Operations](#crud-operations)
3. [Setting Up with Express](#setting-up-with-express)
4. [Using Postman for Testing](#using-postman-for-testing)
5. [Routes](#routes)
6. [Services](#services)
7. [Utils](#utils)
8. [Putting It All Together](#putting-it-all-together)
9. [Exercises](#exercises)

---

### 1. Introduction to RESTful APIs

A **RESTful API** (Representational State Transfer) is an architectural style for designing networked applications. It uses HTTP requests to access and manipulate data through commonly used methods like **GET**, **POST**, **PUT**, and **DELETE**. These APIs are stateless, meaning each request from a client to a server must contain all the information needed to understand and process the request.

#### Why RESTful APIs?

RESTful APIs are widely used because they:
- Are easy to understand and scalable
- Separate client and server logic
- Allow for multiple types of clients (e.g., mobile, web) to interact with the same API

For more details on REST, check out the [official documentation](https://restfulapi.net/).

---

### 2. CRUD Operations

CRUD operations are the four basic operations you can perform on any data:

- **C**reate: Add new data (e.g., adding a new entry in our address book).
- **R**ead: Retrieve existing data (e.g., finding an entry by name).
- **U**pdate: Modify existing data (e.g., changing the address or phone number).
- **D**elete: Remove data (e.g., deleting an entry).

In our Address Book API, we'll implement each CRUD operation. We’ll create functions to manage these actions using Express.

---

### 3. Setting Up with Express

To get started, initialize a new Node.js project and install Express.

```bash
mkdir address-book-api
cd address-book-api
npm init -y
npm install express
```

Then, create a simple `index.js` file to set up your server.

```javascript
// index.js
const express = require('express');
const app = express();
const PORT = 3000;

app.use(express.json());

app.listen(PORT, () => {
    console.log(`Server running on http://localhost:${PORT}`);
});
```

#### Task 1
1. Set up a new project and initialize Express as shown above.
2. Run the server with `node index.js` and verify it's working.

---

### 4. Using Postman for Testing

[Postman](https://www.postman.com/) is a popular tool used to test APIs. You can send different types of requests (e.g., **GET**, **POST**, **PUT**, **DELETE**) to your API endpoints and view the responses.

1. **Download Postman** and open it.
2. **Create a new request**:
    - Choose the HTTP method (GET, POST, PUT, DELETE).
    - Enter the request URL (e.g., `http://localhost:3000/address-book`).
    - Add headers and body data (for POST and PUT requests).
3. **Send the request** and view the response to verify that your API is working correctly.

---

### 5. Routes

**Routes** handle HTTP requests to specific endpoints. They define the paths users will use to interact with the API.

#### Organizing Routes in a Dedicated Folder

It’s good practice to organize your routes in a separate `routes` folder. This will make the codebase cleaner, especially as the project grows.

Create the following file structure:

```plaintext
address-book-api/
├── index.js
├── routes/
│   ├── index.js          // main routes entry point
│   └── addressBook.js    // address book routes
```

1. **index.js**: This is the main entry point that loads all the routes.
2. **addressBook.js**: This file defines the specific routes for the address book.

#### Setting up the Route Files

In `routes/addressBook.js`, define your address book routes:

```javascript
// routes/addressBook.js
const express = require('express');
const router = express.Router();

// Define the routes
router.get('/', (req, res) => {
    res.send("Fetching all entries");
});

router.post('/', (req, res) => {
    res.send("Creating a new entry");
});

router.get('/:id', (req, res) => {
    res.send(`Fetching entry with ID: ${req.params.id}`);
});

router.put('/:id', (req, res) => {
    res.send(`Updating entry with ID: ${req.params.id}`);
});

router.delete('/:id', (req, res) => {
    res.send(`Deleting entry with ID: ${req.params.id}`);
});

module.exports = router;
```

In `routes/index.js`, load the `addressBook` routes:

```javascript
// routes/index.js
const express = require('express');
const addressBookRoutes = require('./addressBook');

const router = express.Router();

router.use('/address-book', addressBookRoutes);

module.exports = router;
```

Finally, update `index.js` to use these routes:

```javascript
// index.js
const express = require('express');
const app = express();
const routes = require('./routes');
const PORT = 3000;

app.use(express.json());
app.use(routes);

app.listen(PORT, () => {
    console.log(`Server running on http://localhost:${PORT}`);
});
```

#### Task 2
1. Create the `routes` folder and files as outlined.
2. Add the routes in `addressBook.js` and test each route in Postman.

---

### 6. Services

Services are used to handle business logic separate from the route handlers. In our project, we can use a `services` folder to manage address book data.

Create a file `addressService.js` in a `services` directory and define CRUD operations:

```javascript
// services/addressService.js
let addressBook = [];

const addEntry = (entry) => {
    addressBook.push(entry);
    return entry;
};

const getEntryById = (id) => {
    return addressBook.find(entry => entry.id === id);
};

// Implement other CRUD operations here...

module.exports = { addEntry, getEntryById /* other functions */ };
```

You can import and use these functions in your route files, keeping route logic clean and manageable.

#### Task 3
1. Implement and test `addEntry` and `getEntryById` in `addressService.js`.
2. Connect the service functions to the corresponding routes in `addressBook.js`.

---

### 7. Utils

Utility functions help keep your code clean by handling common tasks, such as validation and formatting.

In a `utils` folder, create a `validateEntry.js` utility to check if an address entry is valid.

```javascript
// utils/validateEntry.js
const validateEntry = (entry) => {
    const { name, address, number } = entry;
    if (!name || !address || !number) {
        return false;
    }
    return true;
};

module.exports = validateEntry;
```

#### Task 4
1. Create a `validateEntry` utility and use it in the `POST /address-book` route to check for valid input.

---

### 8. Putting It All Together

Now that we've covered each part, let’s put everything together for the Address Book API.

1. **Initialize the Express server.**
2. **Organize routes in a dedicated `routes` folder.**
3. **Set up services to handle CRUD operations for the address book.**
4. **Add utility functions for validation.**

Your final structure should look something like this:

```plaintext
address-book-api/
├── index.js
├── routes/
│   ├── index.js
│   └── addressBook.js
├── services/
│   └── addressService.js
├── utils/
│   └── validateEntry.js
├── package.json
```

---

### Documentation Links

- [Express Documentation](https://expressjs.com/)
- [Postman Download](https://www.postman.com/)

---

Happy coding! 🎉