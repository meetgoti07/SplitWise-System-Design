# Splitwise System Design

## Overview
This repository documents the system design for a simplified version of **Splitwise**, a popular expense-sharing application. The focus of this design is to ensure efficient debt management between users, scalability to support a growing user base, and consistency in handling financial transactions.

This system design is conceptual and does not include any implementation code. It aims to provide a comprehensive overview of the architecture, database, and key design considerations.

---

## Key Features

1. **Expense Sharing**: Users can share expenses between individuals or within groups.
2. **Debt Management**: Track individual debts and simplify group expenses through debt minimization algorithms.
3. **Group Management**: Users can create and manage groups, allowing shared expenses to be automatically split.
4. **Notifications**: Users receive notifications when expenses are added or when they owe money.
5. **Balance Sheet**: Provides a summary of how much each user owes or is owed.
6. **Settlement of Debts**: Users can settle debts, and the system updates balances accordingly.

---

## High-Level Architecture

The system is designed to handle user interactions efficiently and ensure smooth operation through the following key components:

- **Frontend**: 
  - The user interface where users can interact with the application. It includes features for:
    - **Inputting Expenses**: Users can enter details of expenses and split them among group members.
    - **Viewing Balances**: Users can check their current balance and see how much they owe or are owed.
    - **Managing Groups**: Users can create, join, and manage expense-sharing groups.

- **Backend**: 
  - The core logic of the system responsible for:
    - **Expense Creation**: Processes and stores details of new expenses submitted by users.
    - **Balance Calculation**: Computes the balances for each user and ensures they are up-to-date.
    - **Debt Settlement**: Handles the calculation of payments needed to settle debts between users within groups.

- **Database**: 
  - The data storage layer where essential information is kept, including:
    - **User Data**: User profiles, credentials, and preferences.
    - **Expenses**: Details of all expenses recorded in the system.
    - **Groups**: Information about user groups and their members.



---

## System Components

### 1. **User Management**
   - Users can register, log in, and manage profiles.
   - Each user is uniquely identified and can be part of multiple groups.
   
### 2. **Expense Management**
   - Users can add expenses, specifying amounts, participants, and expense details.
   - The system calculates the amount owed by each participant.

### 3. **Debt Simplification**
   - When multiple debts exist between members of a group, the system attempts to minimize the total number of transactions required for settlement.

### 4. **Group Management**
   - Users can create and join groups for shared expenses.
   - Each group has its own ledger, tracking expenses between group members.

### 5. **Notifications**
   - Users are notified when new expenses are added or when they owe money.
   - Notification systems include email or push notifications.

---

## Database Design

The database design focuses on efficient storage and retrieval of user data, expenses, and debts.

### Key Entities:
1. **Users**: Stores user profile information.
2. **Expenses**: Stores details about each expense, including the total amount, the payer, and participants.
3. **Groups**: Defines groups of users who share expenses.
4. **Transactions**: Logs individual debts between users and tracks settled amounts.

Database schema can be found in the [Database Schema Document](./Docs/database-schema.md).

---

## API Design

This section outlines the key API endpoints for managing expenses, users, and groups.

### Key Endpoints:
- **POST /expenses**: Add a new expense, specifying the amount, payer, and participants.
- **GET /balances/{user_id}**: Get the current balance of a user, showing how much they owe and are owed.
- **POST /groups**: Create a new group.
- **POST /settlements**: Record a settlement between users.

More details about API design can be found in the [API Design Document](./Docs/api-design.md).

---

## Scalability and Optimization

As Splitwise scales, it is essential to handle an increasing number of users and transactions. The system uses techniques such as:
1. **Database Indexing**: Optimize queries on users, groups, and expenses.
2. **Sharding**: Split data across multiple databases to handle high volumes of transactions.
3. **Caching**: Frequently accessed data (e.g., balances) can be cached to reduce database load.
4. **Eventual Consistency**: For some non-critical operations, eventual consistency can be used to improve performance.

Further details can be found in the [Scalability Document](./Docs/scalability.md).


---

## Future Considerations

1. **Advanced Debt Simplification**: Implement more complex algorithms for minimizing debt transactions in large groups.
2. **Internationalization**: Support for multiple currencies and conversion between them.
3. **Fraud Prevention**: Implement safeguards to prevent fraudulent expense submissions or settlements.
4. **Blockchain for Settlements**: Explore the use of blockchain for immutable transaction records.

---

## How to Navigate the Repository

1. **Docs Folder**: Contains detailed system design documents.
2. **README.md**: You are here.

---

## Conclusion

This repository provides a conceptual system design for Splitwise, with a focus on efficient debt management, group expense tracking, and scalability. While no code is included, the design documents and diagrams should provide a clear understanding of how such a system could be built.

Feel free to explore the documentation and diagrams for more in-depth details on each component of the system!
