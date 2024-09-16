# Database Schema for Splitwise System

## Introduction

The database schema for Splitwise is designed to manage users, expenses, groups, and transactions efficiently. This document provides an overview of the database tables, their relationships, and the key attributes that support the core functionalities of the application.

---

## Database Tables

### 1. **Users**

**Table Name:** `Users`

| Column Name | Data Type   | Constraints                  | Description                          |
|-------------|-------------|------------------------------|--------------------------------------|
| `UserID`    | INT         | PRIMARY KEY, AUTO_INCREMENT   | Unique identifier for each user.     |
| `Username`  | VARCHAR(255)| UNIQUE, NOT NULL              | Username of the user.                |
| `Email`     | VARCHAR(255)| UNIQUE, NOT NULL              | Email address of the user.           |
| `PasswordHash`| VARCHAR(255)| NOT NULL                      | Hashed password for authentication.  |
| `CreatedAt` | TIMESTAMP   | DEFAULT CURRENT_TIMESTAMP     | Timestamp when the user was created. |
| `UpdatedAt` | TIMESTAMP   | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP | Timestamp when the user details were last updated. |

---

### 2. **Groups**

**Table Name:** `Groups`

| Column Name | Data Type   | Constraints                  | Description                          |
|-------------|-------------|------------------------------|--------------------------------------|
| `GroupID`   | INT         | PRIMARY KEY, AUTO_INCREMENT   | Unique identifier for each group.    |
| `GroupName` | VARCHAR(255)| NOT NULL                      | Name of the group.                  |
| `CreatedAt` | TIMESTAMP   | DEFAULT CURRENT_TIMESTAMP     | Timestamp when the group was created.|
| `UpdatedAt` | TIMESTAMP   | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP | Timestamp when the group details were last updated. |

---

### 3. **GroupMembers**

**Table Name:** `GroupMembers`

| Column Name | Data Type   | Constraints                  | Description                          |
|-------------|-------------|------------------------------|--------------------------------------|
| `GroupID`   | INT         | FOREIGN KEY (`Groups.GroupID`), NOT NULL | Identifier for the group.            |
| `UserID`    | INT         | FOREIGN KEY (`Users.UserID`), NOT NULL  | Identifier for the user.             |
| `JoinedAt`  | TIMESTAMP   | DEFAULT CURRENT_TIMESTAMP     | Timestamp when the user joined the group. |
| PRIMARY KEY (`GroupID`, `UserID`) |   |                               | Composite primary key.                |

---

### 4. **Expenses**

**Table Name:** `Expenses`

| Column Name  | Data Type   | Constraints                  | Description                          |
|--------------|-------------|------------------------------|--------------------------------------|
| `ExpenseID`  | INT         | PRIMARY KEY, AUTO_INCREMENT   | Unique identifier for each expense.  |
| `Amount`     | DECIMAL(10,2)| NOT NULL                      | Total amount of the expense.         |
| `Description`| TEXT        | NULL                         | Description of the expense.          |
| `CreatedBy`  | INT         | FOREIGN KEY (`Users.UserID`), NOT NULL  | Identifier for the user who created the expense. |
| `GroupID`    | INT         | FOREIGN KEY (`Groups.GroupID`), NULL | Identifier for the group (if applicable). |
| `CreatedAt`  | TIMESTAMP   | DEFAULT CURRENT_TIMESTAMP     | Timestamp when the expense was created. |
| `UpdatedAt`  | TIMESTAMP   | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP | Timestamp when the expense details were last updated. |

---

### 5. **ExpenseShares**

**Table Name:** `ExpenseShares`

| Column Name | Data Type   | Constraints                  | Description                          |
|-------------|-------------|------------------------------|--------------------------------------|
| `ExpenseID` | INT         | FOREIGN KEY (`Expenses.ExpenseID`), NOT NULL | Identifier for the expense.          |
| `UserID`    | INT         | FOREIGN KEY (`Users.UserID`), NOT NULL  | Identifier for the user.             |
| `Share`     | DECIMAL(10,2)| NOT NULL                      | Amount that the user owes for the expense. |
| PRIMARY KEY (`ExpenseID`, `UserID`) |   |                               | Composite primary key.                |

---

## Relationships

1. **Users** can be members of multiple **Groups**, and each **Group** can have multiple **Users**. This relationship is managed by the `GroupMembers` table.
2. **Users** can create multiple **Expenses**, which can be shared among multiple **Users** in a **Group**. The `Expenses` table tracks the creator and the group associated with each expense.
3. **Expenses** are shared among users, with each share amount tracked in the `ExpenseShares` table.

---

## Schema Diagram

A visual representation of the database schema can be found in the attached [database-schema-diagram.png](./database-schema-diagram.png). This diagram illustrates the tables, their columns, and the relationships between them.

---

## Conclusion

This document provides an overview of the database schema used for the Splitwise system. The schema is designed to efficiently handle user management, expense tracking, and group management, ensuring that the system can scale and operate effectively as the user base grows.

