
# Intro (Fast)API

This guide introduces FastAPI and covers the basics of building a simple RESTful API. You'll learn about HTTP methods, RESTful principles, and create an API for managing users stored in a list.

---

## Table of Contents

1. [Introduction to HTTP Methods](#introduction-to-http-methods)
2. [What is a RESTful API?](#what-is-a-restful-api)
3. [Setting Up FastAPI](#setting-up-fastapi)
4. [Building the User Management API](#building-the-user-management-api)
   - [Create a User](#create-a-user)
   - [Get All Users](#get-all-users)
   - [Get a Single User](#get-a-single-user)
   - [Modify a User](#modify-a-user)
   - [Delete a User](#delete-a-user)
5. [Running and Testing the API](#running-and-testing-the-api)

---

## 1. Introduction to HTTP Methods

HTTP methods are actions performed on resources via the web. In APIs, these methods define the kind of action that is to be performed on the server.

### Common HTTP Methods:
- **GET**: Retrieve information from the server (e.g., get user data).
- **POST**: Send data to the server to create a new resource (e.g., add a new user).
- **PUT**: Update an existing resource (e.g., modify user information).
- **DELETE**: Remove a resource from the server (e.g., delete a user).

---

## 2. What is a RESTful API?

A **RESTful API** (Representational State Transfer) follows a set of constraints for designing networked applications. It uses HTTP requests to perform CRUD (Create, Read, Update, Delete) operations and is based on these principles:

- **Stateless**: Each request from the client contains all the necessary information for the server to process it.
- **Uniform Interface**: Resources are identified using URIs (e.g., `/users/1`).
- **Representation of Resources**: Resources are typically represented in formats like JSON.

---

## 3. Setting Up FastAPI

### Install FastAPI and Uvicorn

To begin, install FastAPI and Uvicorn (an ASGI server to run FastAPI):
```bash
pip install fastapi uvicorn
```

Create a `main.py` file where we'll build the API.

---

## 4. Building the User Management API

### Step 1: Set Up Basic FastAPI App

First, create a FastAPI app:
```python
from fastapi import FastAPI, HTTPException

app = FastAPI()
```

### Step 2: Define a User Model

We'll use Python’s `pydantic` to define a data model for our users:
```python
from pydantic import BaseModel
from typing import Optional

class User(BaseModel):
    id: int
    name: str
    age: int
    email: str
    active: Optional[bool] = True
```

### Step 3: Create a List to Store Users

We'll store users in a list for simplicity:
```python
users = [
    {"id": 1, "name": "John Doe", "age": 30, "email": "johndoe@example.com", "active": True},
    {"id": 2, "name": "Alice Wonderland", "age": 25, "email": "alice@example.com", "active": True}
]
```

### Step 4: Create CRUD Operations

#### 4.1 Create a User (POST)
```python
@app.post("/users", response_model=User)
def create_user(user: User):
    users.append(user.dict())
    return user
```

This will allow you to send a `POST` request with user data to create a new user.

#### 4.2 Get All Users (GET)
```python
@app.get("/users", response_model=list[User])
def get_users():
    return users
```

This returns all the users in the list.

#### 4.3 Get a Single User by ID (GET)
```python
@app.get("/users/{user_id}", response_model=User)
def get_user(user_id: int):
    for user in users:
        if user["id"] == user_id:
            return user
    raise HTTPException(status_code=404, detail="User not found")
```

This retrieves a single user based on their `id`.

#### 4.4 Modify a User (PUT)
```python
@app.put("/users/{user_id}", response_model=User)
def update_user(user_id: int, updated_user: User):
    for index, user in enumerate(users):
        if user["id"] == user_id:
            users[index] = updated_user.dict()
            return updated_user
    raise HTTPException(status_code=404, detail="User not found")
```

This allows modification of a user's data using the `PUT` method.

#### 4.5 Delete a User (DELETE)
```python
@app.delete("/users/{user_id}")
def delete_user(user_id: int):
    for index, user in enumerate(users):
        if user["id"] == user_id:
            del users[index]
            return {"message": "User deleted successfully"}
    raise HTTPException(status_code=404, detail="User not found")
```

This removes a user from the list by their `id`.

---

## 5. Running and Testing the API

### Step 1: Run the Application

Run the FastAPI application with Uvicorn:
```bash
uvicorn main:app --reload
```

This starts the server at `http://127.0.0.1:8000`.

### Step 2: Test the Endpoints

1. **Get all users**: 
   ```
   GET http://127.0.0.1:8000/users
   ```

2. **Get a specific user**: 
   ```
   GET http://127.0.0.1:8000/users/1
   ```

3. **Create a new user**: 
   ```
   POST http://127.0.0.1:8000/users
   ```
   Example body (JSON):
   ```json
   {
       "id": 3,
       "name": "Bob Builder",
       "age": 35,
       "email": "bob@example.com",
       "active": true
   }
   ```

4. **Update a user**: 
   ```
   PUT http://127.0.0.1:8000/users/1
   ```
   Example body (JSON):
   ```json
   {
       "id": 1,
       "name": "John Smith",
       "age": 31,
       "email": "johnsmith@example.com",
       "active": true
   }
   ```

5. **Delete a user**: 
   ```
   DELETE http://127.0.0.1:8000/users/2
   ```

---

## Try it out

After you are done testing your code, add some comments to it. This would help other developers to get startet with it faster.