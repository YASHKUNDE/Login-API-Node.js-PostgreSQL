# Login API — Node.js & PostgreSQL

> A simple Login & Registration REST API built using **Node.js**, **Express.js**, and **PostgreSQL**.  
> Provides user registration, login authentication, mobile number search, and user listing. *(2024)*

---

## Table of Contents

- [Technologies Used](#technologies-used)
- [Project Structure](#project-structure)
- [Database Configuration](#database-configuration)
- [Installation](#installation)
- [API Endpoints](#api-endpoints)
- [Validation](#validation)
- [Features](#features)
- [Future Improvements](#future-improvements)

---

## Technologies Used

| Technology | Purpose |
|---|---|
| Node.js | Runtime environment |
| Express.js | Web framework |
| PostgreSQL | Database |
| express-validator | Input validation |
| body-parser | Parse incoming request bodies |

---

## Project Structure

```
Login API/
│
├── db.js           # PostgreSQL connection pool
├── index.js        # Main server & route definitions
├── package.json    # Project metadata & dependencies
└── node_modules/   # Installed packages
```

---

## Database Configuration

**Database Name:** `login`

**`db.js`**
```js
const { Pool } = require('pg');

const pool = new Pool({
  user: 'postgres',
  host: 'localhost',
  database: 'login',
  password: '123456',
  port: 5432
});

module.exports = pool;
```

> **Note:** Do not commit real credentials to version control. Use environment variables (`.env`) in production.

### Create Table

Run the following SQL in PostgreSQL before starting the server:

```sql
CREATE TABLE login (
  id     SERIAL PRIMARY KEY,
  users  VARCHAR(100),
  email  VARCHAR(100),
  mobile VARCHAR(20),
  pass   VARCHAR(100)
);
```

---

## Installation

**1. Clone the project**
```bash
git clone <repository-url>
```

**2. Navigate into the project folder**
```bash
cd "Login API"
```

**3. Install dependencies**
```bash
npm install
```

**4. Start the server**
```bash
node index.js
```

Server runs on: **`http://localhost:5000`**

---

## API Endpoints

### 1. Home
```http
GET /
```
**Response**
```html
<h1>Login JS API</h1>
```

---

### 2. Get All Users
```http
GET /users
```
**Response**
```json
{
  "status": "200",
  "message": "Users Found Successfully",
  "users": []
}
```

---

### 3. Register User
```http
POST /reg
```
**Request Body**
```json
{
  "users": "Suyash",
  "email": "suyash@gmail.com",
  "mobile": "9876543210",
  "pass": "123456"
}
```
**Success Response**
```json
{
  "status": "200",
  "message": "Register Saved Successfully"
}
```
**Error Response**
```json
{
  "message": "User already exists with this email"
}
```

---

### 4. Login User
```http
POST /login
```
**Request Body**
```json
{
  "email": "suyash@gmail.com",
  "pass": "123456"
}
```
**Success Response**
```json
{
  "status": "200",
  "message": "Login successful",
  "user": {
    "email": "suyash@gmail.com",
    "pass": "123456",
    "id": 1
  }
}
```
**Error Response**
```json
{
  "message": "Invalid email or password"
}
```

---

### 5. Search User by Mobile Number
```http
POST /mobileid
```
**Request Body**
```json
{
  "id": "9876543210"
}
```
**Success Response**
```json
{
  "status": "200",
  "message": "success",
  "data": []
}
```
**Error Response**
```json
{
  "status": "400",
  "message": "no data found"
}
```

---

## Validation

Input validation is handled using **express-validator**:

- Mobile number format validation
- Required field validation
- Duplicate email checking on registration

---

## Features

- User Registration
- User Login with credential check
- PostgreSQL database integration
- RESTful JSON responses
- Mobile number search
- Input validation
- CORS enabled

---

## Future Improvements

- JWT Authentication
- Password hashing with bcrypt
- Role-based authentication
- Refresh tokens
- Email verification
- Forgot password feature

---

## Author

Developed using Node.js and PostgreSQL — **2024**
