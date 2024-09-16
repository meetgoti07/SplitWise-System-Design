


# API Design

This document outlines the API design for the system, including endpoints for user management, group management, expense management, and expense sharing. Each endpoint includes details on its functionality, request parameters, and response format.





## Endpoints

### 1. User Management

#### 1.1. Register User

- **Endpoint**: `/users/register`
- **Method**: `POST`
- **Description**: Registers a new user.
- **Request Body**:
  ```json
  {
    "username": "string",
    "email": "string",
    "password": "string"
  }
  ```
- **Response**:
  - **Success (201 Created)**:
    ```json
    {
      "id": "integer",
      "username": "string",
      "email": "string",
      "created_at": "string",
      "updated_at": "string"
    }
    ```
  - **Error (400 Bad Request)**:
    ```json
    {
      "error": "string"
    }
    ```

#### 1.2. Authenticate User

- **Endpoint**: `/users/authenticate`
- **Method**: `POST`
- **Description**: Authenticates a user and returns a token.
- **Request Body**:
  ```json
  {
    "username": "string",
    "password": "string"
  }
  ```
- **Response**:
  - **Success (200 OK)**:
    ```json
    {
      "token": "string"
    }
    ```
  - **Error (401 Unauthorized)**:
    ```json
    {
      "error": "string"
    }
    ```

### 2. Group Management

#### 2.1. Create Group

- **Endpoint**: `/groups`
- **Method**: `POST`
- **Description**: Creates a new group.
- **Request Body**:
  ```json
  {
    "name": "string"
  }
  ```
- **Response**:
  - **Success (201 Created)**:
    ```json
    {
      "id": "integer",
      "name": "string",
      "created_at": "string",
      "updated_at": "string"
    }
    ```
  - **Error (400 Bad Request)**:
    ```json
    {
      "error": "string"
    }
    ```

#### 2.2. Add User to Group

- **Endpoint**: `/groups/{group_id}/members`
- **Method**: `POST`
- **Description**: Adds a user to a group.
- **Request Body**:
  ```json
  {
    "user_id": "integer"
  }
  ```
- **Response**:
  - **Success (200 OK)**:
    ```json
    {
      "message": "User added to group"
    }
    ```
  - **Error (400 Bad Request)**:
    ```json
    {
      "error": "string"
    }
    ```

### 3. Expense Management

#### 3.1. Create Expense

- **Endpoint**: `/expenses`
- **Method**: `POST`
- **Description**: Creates a new expense.
- **Request Body**:
  ```json
  {
    "amount": "decimal",
    "description": "string",
    "created_by": "integer",
    "group_id": "integer"
  }
  ```
- **Response**:
  - **Success (201 Created)**:
    ```json
    {
      "id": "integer",
      "amount": "decimal",
      "description": "string",
      "created_by": "integer",
      "group_id": "integer",
      "created_at": "string",
      "updated_at": "string"
    }
    ```
  - **Error (400 Bad Request)**:
    ```json
    {
      "error": "string"
    }
    ```

#### 3.2. Get Expense

- **Endpoint**: `/expenses/{expense_id}`
- **Method**: `GET`
- **Description**: Retrieves details of a specific expense.
- **Response**:
  - **Success (200 OK)**:
    ```json
    {
      "id": "integer",
      "amount": "decimal",
      "description": "string",
      "created_by": "integer",
      "group_id": "integer",
      "created_at": "string",
      "updated_at": "string"
    }
    ```
  - **Error (404 Not Found)**:
    ```json
    {
      "error": "string"
    }
    ```

### 4. Expense Sharing

#### 4.1. Share Expense

- **Endpoint**: `/expenses/{expense_id}/shares`
- **Method**: `POST`
- **Description**: Shares an expense among users.
- **Request Body**:
  ```json
  {
    "user_id": "integer",
    "share": "decimal"
  }
  ```
- **Response**:
  - **Success (200 OK)**:
    ```json
    {
      "message": "Expense shared successfully"
    }
    ```
  - **Error (400 Bad Request)**:
    ```json
    {
      "error": "string"
    }
    ```

#### 4.2. Get Expense Shares

- **Endpoint**: `/expenses/{expense_id}/shares`
- **Method**: `GET`
- **Description**: Retrieves the sharing details of a specific expense.
- **Response**:
  - **Success (200 OK)**:
    ```json
    {
      "shares": [
        {
          "user_id": "integer",
          "share": "decimal"
        }
      ]
    }
    ```
  - **Error (404 Not Found)**:
    ```json
    {
      "error": "string"
    }
    ```

## Error Handling

All endpoints follow a standard error handling format. Common HTTP status codes include:

- **400 Bad Request**: Invalid input or missing parameters.
- **401 Unauthorized**: Invalid or missing authentication token.
- **404 Not Found**: Requested resource does not exist.
- **500 Internal Server Error**: Unexpected server error.

## Rate Limiting

To ensure fair use of the API, rate limiting is implemented. Each user is allowed a maximum of 1000 requests per hour. Exceeding this limit will result in a `429 Too Many Requests` response.
