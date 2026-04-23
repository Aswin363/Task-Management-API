# Task-Management-API
Production-like Task Management API using Flask

## 1. Overview

The Task Management API is a production-style backend system built using Flask. It provides secure user authentication, role-based authorization, and complete task lifecycle management. The application follows modular architecture principles and demonstrates real-world backend development practices, including testing, documentation, and scalable design.

This project is designed to simulate how enterprise systems manage users, tasks, and permissions in a controlled and secure environment.

---

## 2. Objectives

The primary goals of this project are:

* To build a RESTful API using Flask
* To implement secure authentication using JWT
* To enforce role-based access control (RBAC)
* To design relational database models with proper associations
* To support pagination and filtering for scalable data access
* To implement unit testing using pytest
* To structure the project in a modular and maintainable way

---

## 3. Key Features

### 3.1 Authentication and Authorization

* User registration and login functionality
* JWT-based authentication system
* Secure password hashing using Werkzeug
* Role-based access control (Admin and User roles)

### 3.2 Task Management

* Create, read, update, and delete tasks
* Assign tasks to specific users
* Track task ownership and assignment separately
* Maintain task status, priority, and due dates

### 3.3 Role-Based Access Control

* Admin users can:

  * Create tasks
  * Assign tasks
  * Update all task fields
  * Delete tasks
* Regular users can:

  * View assigned tasks
  * Update only task status

### 3.4 API Features

* RESTful API design
* JSON-based request and response handling
* Swagger documentation using Flask-RESTX
* Pagination and filtering support

### 3.5 Testing

* Unit tests implemented using pytest
* Covers authentication and task operations
* Ensures API reliability and correctness

---

## 4. Technology Stack

* Programming Language: Python 3.11
* Framework: Flask
* ORM: SQLAlchemy
* Authentication: Flask-JWT-Extended
* API Documentation: Flask-RESTX (Swagger)
* Database: SQLite (development)
* Testing: pytest

---

## 5. Project Structure

```text
task_manager_api/
│
├── app/
│   ├── __init__.py        # Application factory
│   ├── auth.py            # Authentication endpoints
│   ├── tasks.py           # Task management endpoints
│   ├── models.py          # Database models
│   ├── extensions.py      # DB, JWT, and API initialization
│   ├── config.py          # Configuration classes
│   └── utils.py           # Helper functions and decorators
│
├── instance/
│   └── task_management.db # SQLite database file
│
├── tests/
│   ├── test_auth.py
│   ├── test_tasks.py
│   └── conftest.py
│
├── .env                   # Environment variables
├── requirements.txt
├── run.py
└── README.md
```

---

## 6. Database Design

The system consists of two main entities:

### User

* Stores user credentials and role
* Supports authentication and authorization

### Task

* Stores task details
* Contains two foreign keys:

  * created_by_id (task creator)
  * assigned_to_id (task assignee)

### Relationships

* One user can create multiple tasks
* One user can be assigned multiple tasks
* Each task references the User table twice

---

## 7. API Endpoints

### Authentication

* POST /api/auth/register
  Register a new user

* POST /api/auth/login
  Authenticate user and return JWT token

### Tasks

* GET /api/tasks
  Retrieve tasks with pagination and filtering

* POST /api/tasks
  Create a new task (Admin only)

* GET /api/tasks/{task_id}
  Retrieve a specific task

* PUT /api/tasks/{task_id}
  Update task details

* DELETE /api/tasks/{task_id}
  Delete a task (Admin only)

* PATCH /api/tasks/{task_id}/assign
  Assign a task to a user (Admin only)

---

## 8. Authentication Flow

1. User registers an account

2. User logs in using credentials

3. Server returns a JWT token

4. Token is included in request headers:

   Authorization: Bearer <token>

5. Protected endpoints validate the token before processing

---

## 9. Pagination and Filtering

The API supports query parameters:

* page: page number
* per_page: items per page
* status: filter by task status
* priority: filter by priority
* search: search by task title

Example:

GET /api/tasks?page=1&status=pending

---

## 10. Running the Project Locally

### Step 1: Create Virtual Environment

python -m venv venv
venv\Scripts\activate

### Step 2: Install Dependencies

pip install -r requirements.txt

### Step 3: Configure Environment

Create a .env file:

FLASK_ENV=development
SECRET_KEY=your_secret
JWT_SECRET_KEY=your_jwt_secret
DATABASE_URL=sqlite:///task.db

### Step 4: Run the Application

python app.py

### Step 5: Access API Documentation

http://127.0.0.1:5000/docs

---

## 11. Testing

Run tests using pytest:

pytest

Example test cases include:

* User registration
* User login
* Task creation (admin)
* Unauthorized access validation
* Task retrieval

---

## 12. Security Considerations

* Passwords are stored as hashes
* JWT tokens secure API endpoints
* Role-based access prevents unauthorized actions
* Input validation is applied to API requests

---

## 13. Future Enhancements

* PostgreSQL integration for production
* Deployment using Docker or cloud platforms
* Frontend integration (React or Angular)
* Email notifications for task updates
* Role hierarchy and permissions expansion

---

## 14. Conclusion

This project demonstrates a complete backend system with authentication, authorization, database relationships, and API design. It reflects production-level practices and can be extended into a full-scale application.

---

## 15. Author

Developed as part of backend system design and API development practice.
