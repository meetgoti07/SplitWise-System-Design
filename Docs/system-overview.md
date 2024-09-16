# Splitwise System Overview

## Introduction

Splitwise is a popular expense-sharing application that simplifies the process of splitting bills and tracking shared expenses among friends, roommates, or colleagues. This system allows users to add expenses, track debts, and settle payments in a simple and transparent manner.

This document provides an overview of the system design for a simplified version of Splitwise, focusing on key components, their interactions, and how the system handles core functionalities like expense tracking, debt management, and group management.

---

## Problem Statement

When people share expenses, such as during group activities or living arrangements, it can be difficult to keep track of who owes what. Splitwise solves this problem by providing a centralized platform where users can easily:
- Add expenses.
- Track how much they owe or are owed.
- Settle debts.

---

## Key Features

The system design includes the following major features:

1. **Expense Sharing**:
   - Users can add expenses and share them among individuals or within groups.
   - Expenses can be split equally or unequally based on user preferences.

2. **Debt Management**:
   - The system calculates how much each user owes and provides a detailed breakdown of outstanding balances.
   - Users can view individual debts as well as overall balances within groups.

3. **Group Management**:
   - Users can create and join groups to simplify expense sharing between multiple people.
   - Group expenses are automatically split between all members, making it easy to manage group activities like trips or shared living.

4. **Notifications**:
   - Users are notified when a new expense is added, when they owe money, or when a debt has been settled.
   - Notifications help ensure users are always up to date on their balances.

5. **Debt Settlement**:
   - Users can settle debts, either partially or fully, and the system will update balances accordingly.

---

## System Components

The system is divided into several key components, each responsible for handling a specific part of the application:

### 1. **User Management**
   - Users can sign up, log in, and manage their profiles.
   - Each user is identified uniquely within the system, allowing them to track their expenses and group memberships.

### 2. **Expense Management**
   - The core functionality of the system is adding and tracking expenses.
   - Users can specify:
     - The total amount.
     - The payer.
     - Participants (who shares the expense).
   - Expenses can be split equally or customized to fit specific scenarios (e.g., different amounts for different people).

### 3. **Debt Management**
   - The system tracks how much each user owes and is owed, both at an individual level and within groups.
   - Debts can be simplified using algorithms to minimize the number of transactions required to settle all debts.

### 4. **Group Management**
   - Users can create and manage groups.
   - Groups allow for easy management of shared expenses between multiple users (e.g., for trips or shared apartments).
   - Group expenses are visible to all members.

### 5. **Notifications**
   - Users are notified when an expense is added or updated, when they owe money, and when debts are settled.
   - Notifications keep users informed about the status of their expenses and balances.

### 6. **Settlements**
   - Users can settle debts by making payments (outside the system) and marking those debts as settled.
   - The system will adjust balances accordingly, updating all relevant users.

---

## Architecture Overview

The Splitwise system consists of three main layers:
1. **Frontend**: The user interface where users interact with the system, add expenses, and view balances.
2. **Backend**: The core logic of the system, responsible for processing expenses, updating balances, and managing groups.
3. **Database**: Stores user data, expenses, group information, and balances. The database handles persistent storage and is optimized for fast queries.

A detailed architecture diagram can be found in the [architecture-diagram.md](./architecture-diagram.md).

---

## Workflow

### Adding an Expense:
1. User inputs expense details (amount, payer, participants).
2. The system calculates how the expense is split and updates balances.
3. A notification is sent to all involved users.

### Viewing Balances:
1. A user requests to view their balance.
2. The system retrieves the user's balance data from the database.
3. The user sees a breakdown of how much they owe and are owed.

### Settling a Debt:
1. A user marks a debt as settled.
2. The system updates balances for both the payer and recipient.
3. A notification is sent to confirm the settlement.

---


