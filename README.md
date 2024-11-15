

# ToDo Backend API

This project is a RESTful API for a ToDo application, with user authentication, token verification, and CRUD operations for task management.

## Features
- **User Authentication**: Users can sign up, log in, and authenticate via JSON Web Tokens (JWT).
- **Task Management**: Allows creation, viewing, updating, and deletion of tasks.
- **Token Verification**: Verifies token validity for secure access to protected routes.
- **RESTful Endpoints**: Organized API endpoints for task and user management.

## Tech Stack
- **Node.js**: Server-side runtime environment.
- **Express.js**: Web framework for handling routes and middleware.
- **MongoDB**: Database to store user and task data.
- **JWT**: Token-based authentication.


## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/asmitk991/backendTodo1.git
   cd backendTodo1
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Set up environment variables**:
   Create a `.env` file in the root directory with the following:
   ```plaintext
   PORT=5000
   MONGO_URI=<Your MongoDB URI>
   JWT_SECRET=<Your JWT secret>
   ```

4. **Start the server**:
   ```bash
   npm start
   ```
   The server will run at `http://localhost:5000`.

## API Endpoints

### General

#### Root Endpoint
- **URL**: `/`
- **Method**: `GET`
- **Description**: Returns a welcome message to confirm the server is running.
- **Response**:
  - `200 OK`: Returns "Hello from the server".

### Authentication

#### Signup
- **URL**: `/signup`
- **Method**: `POST`
- **Body**:
  ```json
  {
    "name": "Your Name",
    "email": "user@example.com",
    "password": "yourPassword"
  }
  ```
- **Description**: Creates a new user with hashed password storage.
- **Response**:
  - `201 Created`: User created successfully.
  - `500 Internal Server Error`: Error occurred while creating user.

#### Login
- **URL**: `/login`
- **Method**: `POST`
- **Body**:
  ```json
  {
    "email": "user@example.com",
    "password": "yourPassword"
  }
  ```
- **Description**: Authenticates a user, returning a JWT if credentials are valid.
- **Response**:
  - `200 OK`: Returns a JWT token.
  - `401 Unauthorized`: Invalid credentials.
  - `500 Internal Server Error`: Error during login.

#### Token Verification
- **URL**: `/verify-token`
- **Method**: `POST`
- **Body**:
  ```json
  {
    "token": "<JWT_TOKEN>"
  }
  ```
- **Description**: Verifies the validity of a JWT token.
- **Response**:
  - `200 OK`: Token is valid, returns `userId`.
  - `401 Unauthorized`: Token is invalid or not provided.

### Task Management (Protected Routes)
All task routes require authentication. Include `Authorization: Bearer <JWT_TOKEN>` in headers.

#### Fetch All Tasks
- **URL**: `/tasks`
- **Method**: `GET`
- **Headers**: `Authorization: Bearer <JWT_TOKEN>`
- **Description**: Fetches all tasks for the authenticated user.
- **Response**:
  - `200 OK`: Returns a list of tasks.
  - `401 Unauthorized`: Invalid token.

#### Create a New Task
- **URL**: `/tasks`
- **Method**: `POST`
- **Headers**: `Authorization: Bearer <JWT_TOKEN>`
- **Body**:
  ```json
  {
    "title": "Task title",
    "description": "Task description"
  }
  ```
- **Description**: Adds a new task for the authenticated user.
- **Response**:
  - `201 Created`: Task created successfully.
  - `400 Bad Request`: Invalid task data.

#### Update Task by ID
- **URL**: `/tasks/:id`
- **Method**: `PUT`
- **Headers**: `Authorization: Bearer <JWT_TOKEN>`
- **Body**:
  ```json
  {
    "title": "Updated title",
    "description": "Updated description"
  }
  ```
- **Description**: Updates the specified task.
- **Response**:
  - `200 OK`: Task updated.
  - `404 Not Found`: Task with specified ID not found.

#### Delete Task by ID
- **URL**: `/tasks/:id`
- **Method**: `DELETE`
- **Headers**: `Authorization: Bearer <JWT_TOKEN>`
- **Description**: Deletes the specified task.
- **Response**:
  - `200 OK`: Task deleted.
  - `404 Not Found`: Task with specified ID not found.



## Error Codes
- **200 OK**: Successful request.
- **201 Created**: Resource created.
- **400 Bad Request**: Invalid input.
- **401 Unauthorized**: Authentication required.
- **404 Not Found**: Resource not found.



