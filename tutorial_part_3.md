
# Tutorial: Part 3 – Creating a RESTful API with Express.js and PostgreSQL

In this section, we will set up a backend using **Express.js** and connect it to a **PostgreSQL** database. We will also explore how to create and handle RESTful API endpoints. This will serve as the foundation for integrating the backend with our Vue.js frontend in the future.

---

## 1. Setting Up a Node.js Project

### 1.1. Initialize a New Node.js Project
Create a new folder for your backend project and initialize it using npm:

```bash
mkdir backend && cd backend
npm init -y
```

The `-y` flag automatically accepts the default settings. This will create a `package.json` file in your project directory.

### 1.2. Installing Dependencies
We need to install **Express** for our server and **pg** (node-postgres) to interact with our PostgreSQL database:

```bash
npm install express pg
```

- **express**: A minimal and flexible Node.js web application framework.
- **pg**: A PostgreSQL client for Node.js.

---

## 2. Setting Up an Express.js Server

### 2.1. Creating a `server.js` File
Create a new file called `server.js` in your project directory and add the following code:

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.use(express.json()); // Middleware to parse JSON requests

app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

### 2.2. Running the Server
You can run your server using the following command:

```bash
node server.js
```

Open your browser and go to `http://localhost:3000`. You should see "Hello, World!" displayed on the page.

---

## 3. Connecting to PostgreSQL

### 3.1. Setting Up the Database
If you are using Docker, make sure your PostgreSQL container is running. If you haven’t set up PostgreSQL yet, refer back to Part 1 for instructions on how to do this with Docker.

### 3.2. Creating a Database Connection
Update your `server.js` file to include the PostgreSQL connection:

```javascript
const { Pool } = require('pg');

const pool = new Pool({
  user: 'postgres',
  host: 'localhost',
  database: 'my-database',
  password: 'password',
  port: 5432,
});

pool.connect((err) => {
  if (err) {
    console.error('Database connection error', err.stack);
  } else {
    console.log('Database connected successfully');
  }
});
```

Replace `user`, `password`, and `database` with your PostgreSQL credentials.

---

## 4. Creating RESTful API Endpoints

### 4.1. Creating a Basic Route to Fetch Data
Let's create a route to fetch data from our PostgreSQL database. For this example, we'll assume you have a table called `users`.

```javascript
app.get('/users', async (req, res) => {
  try {
    const result = await pool.query('SELECT * FROM users');
    res.json(result.rows);
  } catch (err) {
    console.error(err);
    res.status(500).send('Error fetching data from the database');
  }
});
```

### 4.2. Creating a Route to Add Data
We can also create a route to add new users to our database:

```javascript
app.post('/users', async (req, res) => {
  const { name, email } = req.body;
  try {
    const result = await pool.query(
      'INSERT INTO users (name, email) VALUES ($1, $2) RETURNING *',
      [name, email]
    );
    res.status(201).json(result.rows[0]);
  } catch (err) {
    console.error(err);
    res.status(500).send('Error adding data to the database');
  }
});
```

Make sure to use `express.json()` middleware to parse JSON request bodies.

### 4.3. Creating a Route to Update Data
Here's how to create a route to update an existing user:

```javascript
app.put('/users/:id', async (req, res) => {
  const { id } = req.params;
  const { name, email } = req.body;
  try {
    const result = await pool.query(
      'UPDATE users SET name = $1, email = $2 WHERE id = $3 RETURNING *',
      [name, email, id]
    );
    if (result.rows.length === 0) {
      return res.status(404).send('User not found');
    }
    res.json(result.rows[0]);
  } catch (err) {
    console.error(err);
    res.status(500).send('Error updating data in the database');
  }
});
```

### 4.4. Creating a Route to Delete Data
Finally, let's create a route to delete a user:

```javascript
app.delete('/users/:id', async (req, res) => {
  const { id } = req.params;
  try {
    const result = await pool.query('DELETE FROM users WHERE id = $1 RETURNING *', [id]);
    if (result.rows.length === 0) {
      return res.status(404).send('User not found');
    }
    res.send('User deleted successfully');
  } catch (err) {
    console.error(err);
    res.status(500).send('Error deleting data from the database');
  }
});
```

---

## 5. Testing Your API with Postman or cURL
You can use **Postman** or **cURL** to test your API endpoints:

- **Postman**: A popular tool for testing APIs. You can send GET, POST, PUT, and DELETE requests easily.
- **cURL**: A command-line tool for making HTTP requests.

Example cURL command to test the `/users` endpoint:

```bash
curl -X GET http://localhost:3000/users
```

---

## 6. Summary
In Part 3, you have:
- Set up an Express.js server.
- Connected the server to a PostgreSQL database.
- Created RESTful API endpoints to interact with the database.
- Learned how to handle data fetching, adding, updating, and deleting.

In the next part, we will integrate this backend with the Vue.js frontend to create a full-stack web application. Let me know if you have any questions or need further assistance!
