# Data Flow

This document outlines the flow of data within the system, detailing how information is processed and transferred between different components. Understanding this flow is crucial for maintaining and scaling the application.

## 1. User Registration and Authentication

- **User Registration**:
  - **Input**: User provides `username`, `email`, and `password`.
  - **Process**:
    - The password is hashed.
    - A new record is created in the `users` table with `username`, `email`, `password_hash`, `created_at`, and `updated_at` fields.
  - **Output**: A new user account is created and stored in the `users` table.

- **User Authentication**:
  - **Input**: User provides `username` and `password`.
  - **Process**:
    - The provided password is hashed and compared with the stored `password_hash`.
    - If the hashes match, authentication is successful.
  - **Output**: Authentication status and user details are returned.

## 2. Group Creation and Management

- **Creating a Group**:
  - **Input**: User provides `group_name`.
  - **Process**:
    - A new record is created in the `groups` table with `name`, `created_at`, and `updated_at` fields.
  - **Output**: A new group is created and stored in the `groups` table.

- **Adding Users to a Group**:
  - **Input**: `group_id` and `user_id` are provided.
  - **Process**:
    - A new record is created in the `group_members` table with `group_id`, `user_id`, and `joined_at` fields.
  - **Output**: The user is added to the specified group.

## 3. Expense Creation and Management

- **Creating an Expense**:
  - **Input**: `amount`, `description`, `created_by`, and `group_id`.
  - **Process**:
    - A new record is created in the `expenses` table with the provided details and timestamps.
  - **Output**: A new expense is recorded in the `expenses` table.

- **Sharing an Expense**:
  - **Input**: `expense_id`, `user_id`, and `share`.
  - **Process**:
    - A new record is created in the `expense_shares` table with the provided details.
  - **Output**: The expense sharing details are recorded, indicating how much each user owes.

## 4. Data Synchronization

- **Updating Records**:
  - **Input**: Changes to user information, group details, or expenses.
  - **Process**:
    - Relevant records are updated in the `users`, `groups`, `expenses`, or `expense_shares` tables with new values and timestamps.
  - **Output**: Updated records reflect the most recent changes.

- **Fetching Data**:
  - **Input**: Requests for user profiles, group details, or expense summaries.
  - **Process**:
    - Relevant queries are executed against the `users`, `groups`, `expenses`, and `expense_shares` tables.
  - **Output**: Data is retrieved and sent back to the requesting component.

## 5. Example Data Flow

1. **User A** registers by providing `username`, `email`, and `password`.
   - Data is hashed and stored in the `users` table.

2. **User A** creates a new group named "Travel".
   - A new record is created in the `groups` table.

3. **User A** adds **User B** to the "Travel" group.
   - A new record is added to the `group_members` table.

4. **User A** creates an expense of $100 for "Hotel Stay".
   - A new record is created in the `expenses` table.

5. **User A** shares the expense with **User B**, each paying $50.
   - New records are created in the `expense_shares` table.

6. **User B** views their balance and sees they owe $50 for the "Hotel Stay".
   - Data is fetched from the `expenses` and `expense_shares` tables and presented to **User B**.



