# Express + PostgreSQL REST API

A simple RESTful API built using **Express.js**, **TypeScript**, and **PostgreSQL**.  
This project demonstrates basic **CRUD operations**, **database initialization**, and a **custom request logger**.

---

## Features

- Express server with TypeScript
- PostgreSQL database connection using `pg`
- Automatic table creation on server start
- CRUD operations for **Users**
- CRUD operations for **Todos**
- User–Todo relationship (One-to-Many)
- Custom file-based request logger middleware
- Environment variable support using `dotenv`

---

## Tech Stack

- **Node.js**
- **Express**
- **TypeScript**
- **PostgreSQL**
- **pg**
- **dotenv**
- **fs (File System)**

---

## Database Schema

### Users Table

| Column     | Type                  |
| ---------- | --------------------- |
| id         | SERIAL (PK)           |
| name       | VARCHAR(100)          |
| email      | VARCHAR(150) (UNIQUE) |
| age        | INT                   |
| address    | TEXT                  |
| phone      | VARCHAR(20)           |
| created_at | TIMESTAMP             |
| updated_at | TIMESTAMP             |

---

### Todos Table

| Column      | Type                |
| ----------- | ------------------- |
| id          | SERIAL (PK)         |
| userid      | INT (FK → users.id) |
| title       | VARCHAR(200)        |
| description | TEXT                |
| completed   | BOOLEAN             |
| due_date    | DATE                |
| created_at  | TIMESTAMP           |
| updated_at  | TIMESTAMP           |

---

## Project Setup

### Install Dependencies

```bash
npm install
```

---

### Environment Variables

Create a `.env` file in the project root:

```env
CONNECTION_STRING=postgresql://username:password@localhost:5432/dbname
```

---

### Start the Server

```bash
npm run dev
```

Server will run on:

```
http://localhost:5000
```

---

## API Endpoints

### Users

| Method | Endpoint     | Description     |
| ------ | ------------ | --------------- |
| POST   | `/users`     | Create a user   |
| GET    | `/users`     | Get all users   |
| GET    | `/users/:id` | Get single user |
| PUT    | `/users/:id` | Update user     |
| DELETE | `/users/:id` | Delete user     |

---

### Todos

| Method | Endpoint          | Description     |
| ------ | ----------------- | --------------- |
| POST   | `/todos`          | Create todo     |
| GET    | `/todos`          | Get all todos   |
| GET    | `/todos/:id`      | Get single todo |
| GET    | `/todos/user/:id` | Todos of a user |
| PUT    | `/todos/:id`      | Update todo     |
| DELETE | `/todos/:id`      | Delete todo     |

---

## Logger Middleware

- Logs every request with:

  - Timestamp
  - HTTP Method
  - Request Path

- Stored in: `src/logger.txt`

Example log:

```
[2025-01-01T10:30:00.000Z] GET /users
```

---

## Error Handling

- 404 handler for unknown routes
- Database errors handled with `try-catch`
- Proper HTTP status codes used

---

## Notes

- Uses **parameterized queries** to prevent SQL injection
- PostgreSQL `ON DELETE CASCADE` is used for relational cleanup
- Logger middleware is applied globally
