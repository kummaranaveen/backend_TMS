# Task Management System

This project is a Task Management System built using Django and Django REST Framework. It allows users to manage tasks, including creating, updating, listing, and deleting tasks. The system also includes user authentication using JWT (JSON Web Tokens).

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
  - [User Registration](#user-registration)
  - [User Login](#user-login)
  - [User Logout](#user-logout)
  - [Create Task](#create-task)
  - [List Tasks](#list-tasks)
  - [Update Task](#update-task)
  - [Delete Task](#delete-task)
- [Examples](#examples)
  - [User Registration](#user-registration-example)
  - [User Login](#user-login-example)
  - [Create Task](#create-task-example)
  - [List Tasks](#list-tasks-example)
  - [Update Task](#update-task-example)
  - [Delete Task](#delete-task-example)

## Prerequisites

Before you begin, ensure you have met the following requirements:

- Python 3.8 or higher
- Django 5.1.3 or higher
- MySQL or any other supported database
- `pip` for installing Python packages

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/task-management.git
   cd task-management
   ```

2. Create a virtual environment and activate it:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

3. Install the required packages:
   ```bash
   pip install -r requirements.txt
   ```

## Configuration

1. Set up your database configuration in `task_management/settings.py`:
   ```python
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.mysql',
           'NAME': 'task_management_db',
           'USER': 'root',
           'PASSWORD': 'admin',
           'HOST': 'localhost',
           'PORT': '3306',
       }
   }
   ```

2. Apply migrations to create the database schema:
   ```bash
   python manage.py migrate
   ```

## Running the Application

1. Start the Django development server:
   ```bash
   python manage.py runserver
   ```

2. The application should now be running at `http://127.0.0.1:8000/`.

## API Endpoints

### User Registration

- **URL**: `/api/register/`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "username": "your_username",
    "password": "your_password",
    "email": "your_email@example.com"
  }
  ```
- **Response**:
  ```json
  {
    "username": "your_username",
    "email": "your_email@example.com"
  }
  ```

### User Login

- **URL**: `/api/login/`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "username": "your_username",
    "password": "your_password"
  }
  ```
- **Response**:
  ```json
  {
    "refresh": "your_refresh_token",
    "access": "your_access_token"
  }
  ```

### User Logout

- **URL**: `/api/logout/`
- **Method**: `POST`
- **Request Body**:
  ```json
  {}
  ```
- **Response**:
  ```json
  {
    "message": "Logged out successfully!"
  }
  ```

### Create Task

- **URL**: `/api/tasks/`
- **Method**: `POST`
- **Headers**:
  ```json
  {
    "Authorization": "Bearer your_access_token"
  }
  ```
- **Request Body**:
  ```json
  {
    "title": "Task Title",
    "description": "Task Description",
    "priority": "medium",
    "status": "in-progress",
    "deadline": "2024-12-31"
  }
  ```
- **Response**:
  ```json
  {
    "id": 1,
    "title": "Task Title",
    "description": "Task Description",
    "priority": "medium",
    "status": "in-progress",
    "deadline": "2024-12-31",
    "created_at": "2024-11-22T12:34:56Z",
    "updated_at": "2024-11-22T12:34:56Z"
  }
  ```

### List Tasks

- **URL**: `/api/tasks/list/`
- **Method**: `GET`
- **Headers**:
  ```json
  {
    "Authorization": "Bearer your_access_token"
  }
  ```
- **Query Parameters**:
  - `status`: Filter by task status (e.g., `yet-to-start`, `in-progress`, `completed`, `hold`)
  - `priority`: Filter by task priority (e.g., `low`, `medium`, `high`)
  - `description`: Filter by task description (partial match)
  - `title`: Filter by task title (partial match)
  - `start_date`: Filter tasks with deadlines greater than or equal to this date
  - `end_date`: Filter tasks with deadlines less than or equal to this date
- **Response**:
  ```json
  [
    {
      "id": 1,
      "title": "Task Title",
      "description": "Task Description",
      "priority": "medium",
      "status": "in-progress",
      "deadline": "2024-12-31",
      "created_at": "2024-11-22T12:34:56Z",
      "updated_at": "2024-11-22T12:34:56Z"
    },
    ...
  ]
  ```

### Update Task

- **URL**: `/api/tasks/{task_id}/`
- **Method**: `PUT`
- **Headers**:
  ```json
  {
    "Authorization": "Bearer your_access_token"
  }
  ```
- **Request Body**:
  ```json
  {
    "title": "Updated Task Title",
    "description": "Updated Task Description",
    "priority": "high",
    "status": "completed",
    "deadline": "2024-12-31"
  }
  ```
- **Response**:
  ```json
  {
    "id": 1,
    "title": "Updated Task Title",
    "description": "Updated Task Description",
    "priority": "high",
    "status": "completed",
    "deadline": "2024-12-31",
    "created_at": "2024-11-22T12:34:56Z",
    "updated_at": "2024-11-22T12:34:56Z"
  }
  ```

### Delete Task

- **URL**: `/api/tasks/delete/{task_id}/`
- **Method**: `DELETE`
- **Headers**:
  ```json
  {
    "Authorization": "Bearer your_access_token"
  }
  ```
- **Response**:
  ```json
  {}
  ```

## Examples

### User Registration Example

**Request**:
```bash
curl -X POST http://127.0.0.1:8000/api/register/ -H "Content-Type: application/json" -d '{"username": "testuser", "password": "testpassword", "email": "test@example.com"}'
```

**Response**:
```json
{
  "username": "testuser",
  "email": "test@example.com"
}
```

### User Login Example

**Request**:
```bash
curl -X POST http://127.0.0.1:8000/api/login/ -H "Content-Type: application/json" -d '{"username": "testuser", "password": "testpassword"}'
```

**Response**:
```json
{
  "refresh": "your_refresh_token",
  "access": "your_access_token"
}
```

### Create Task Example

**Request**:
```bash
curl -X POST http://127.0.0.1:8000/api/tasks/ -H "Authorization: Bearer your_access_token" -H "Content-Type: application/json" -d '{"title": "New Task", "description": "Task Description", "priority": "medium", "status": "in-progress", "deadline": "2024-12-31"}'
```

**Response**:
```json
{
  "id": 1,
  "title": "New Task",
  "description": "Task Description",
  "priority": "medium",
  "status": "in-progress",
  "deadline": "2024-12-31",
  "created_at": "2024-11-22T12:34:56Z",
  "updated_at": "2024-11-22T12:34:56Z"
}
```

### List Tasks Example

**Request**:
```bash
curl -X GET http://127.0.0.1:8000/api/tasks/list/ -H "Authorization: Bearer your_access_token"
```

**Response**:
```json
[
  {
    "id": 1,
    "title": "New Task",
    "description": "Task Description",
    "priority": "medium",
    "status": "in-progress",
    "deadline": "2024-12-31",
    "created_at": "2024-11-22T12:34:56Z",
    "updated_at": "2024-11-22T12:34:56Z"
  },
  ...
]
```

### Update Task Example

**Request**:
```bash
curl -X PUT http://127.0.0.1:8000/api/tasks/1/ -H "Authorization: Bearer your_access_token" -H "Content-Type: application/json" -d '{"title": "Updated Task", "description": "Updated Description", "priority": "high", "status": "completed", "deadline": "2024-12-31"}'
```

**Response**:
```json
{
  "id": 1,
  "title": "Updated Task",
  "description": "Updated Description",
  "priority": "high",
  "status": "completed",
  "deadline": "2024-12-31",
  "created_at": "2024-11-22T12:34:56Z",
  "updated_at": "2024-11-22T12:34:56Z"
}
```

### Delete Task Example

**Request**:
```bash
curl -X DELETE http://127.0.0.1:8000/api/tasks/delete/1/ -H "Authorization: Bearer your_access_token"
```

**Response**:
```json
{}
```

## Conclusion

This README provides a comprehensive guide to setting up, configuring, and using the Task Management System. Follow the instructions to get the project up and running, and use the API endpoints to manage tasks and user authentication.