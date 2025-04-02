# Bank Management System

## Description
This is a simple Bank Management System implemented in Python using MySQL as the database. It provides functionality to create, view, update, and delete bank accounts while handling deposits and withdrawals.
The system follows an OOP-based structure and includes:
Database Abstraction Layer for managing MySQL operations.
Error Handling and Logging for debugging and tracking operations.

## Features
Create Account: Add a new account with a unique account number, name, and initial balance.
View Accounts: Display all bank accounts in a tabular format.
Deposit Money: Add funds to an account.
Withdraw Money: Deduct funds from an account (if sufficient balance exists).
Update Balance: Modify the balance of an account.
Delete Account: Remove an account from the database.
Logging: Errors and important actions are logged for debugging.

## Requirements
Python 3.x
MySQL Server
MySQL Connector for Python (mysql-connector-python)
Install MySQL Connector
Run the following command:
pip install mysql-connector-python

## Setup Instructions

1. Configure Database Connection

Modify the Database class inside bank_system.py to match your MySQL credentials:

class Database:
    def __init__(self, host="localhost", user="root", password="password", database="bank"):

Update host, user, password, and database accordingly.

2. Create the MySQL Database
Login to MySQL and create the database:

CREATE DATABASE bank;
The program will automatically create the accounts table if it does not exist.

4. Run the Program
Execute the script:
python bank_system.py


## Usage

### Menu Options:

When the program runs, it will display:

=== Banking System ===
1. Create Account
2. View Accounts
3. Deposit Money
4. Withdraw Money
5. Update Balance
6. Delete Account
7. Exit

Choose an option and follow the prompts.


## Example Transactions:

Creating an Account

Enter Account Number: 1001
Enter Account Holder Name: John Doe
Enter Initial Balance: 5000

Depositing Money

Enter Account Number: 1001
Enter Amount to Deposit: 2000
Successfully deposited 2000. New balance: 7000

Withdrawing Money

Enter Account Number: 1001
Enter Amount to Withdraw: 3000
Successfully withdrew 3000. New balance: 4000

## Logging
The program logs actions and errors in the console, for example:
2025-04-02 12:00:00 - INFO - Account created successfully!
2025-04-02 12:05:00 - ERROR - Invalid input! Please enter numeric values where required.

## Future Enhancements
Add User Authentication
Implement Transaction History
Create a Graphical User Interface (GUI)

Author
Developed by Bloom
