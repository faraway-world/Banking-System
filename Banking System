import mysql.connector
import logging

# Configure logging
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s - %(message)s')

class Database:
    def __init__(self, host="localhost", user="root", password="password", database="bank"):
        self.connection = mysql.connector.connect(host=host, user=user, password=password, database=database)
        self.cursor = self.connection.cursor()
        self.create_table()

    def create_table(self):
        self.cursor.execute('''
        CREATE TABLE IF NOT EXISTS accounts (
            account_no INT PRIMARY KEY,
            name VARCHAR(50),
            balance DECIMAL(10, 2)
        )''')
        self.connection.commit()

    def execute(self, query, values=None, fetch=False):
        try:
            self.cursor.execute(query, values or ())
            if fetch:
                return self.cursor.fetchall()
            self.connection.commit()
        except mysql.connector.Error as err:
            logging.error(f"Database error: {err}")
            return None

    def close(self):
        self.cursor.close()
        self.connection.close()

class BankSystem:
    def __init__(self):
        self.db = Database()

    def create_account(self):
        try:
            account_no = int(input("Enter Account Number: "))
            name = input("Enter Account Holder Name: ")
            balance = float(input("Enter Initial Balance: "))
            
            self.db.execute("INSERT INTO accounts (account_no, name, balance) VALUES (%s, %s, %s)",
                            (account_no, name, balance))
            logging.info("Account created successfully!")
        except ValueError:
            logging.error("Invalid input! Please enter numeric values where required.")

    def view_accounts(self):
        records = self.db.execute("SELECT * FROM accounts", fetch=True)
        if records:
            print("Account No | Name        | Balance")
            print("----------------------------------")
            for row in records:
                print(f"{row[0]:<10} | {row[1]:<10} | {row[2]:<10.2f}")
        else:
            logging.info("No accounts found.")

    def deposit_money(self):
        try:
            account_no = int(input("Enter Account Number: "))
            amount = float(input("Enter Amount to Deposit: "))
            
            result = self.db.execute("SELECT balance FROM accounts WHERE account_no = %s", (account_no,), fetch=True)
            if result:
                new_balance = result[0][0] + amount
                self.db.execute("UPDATE accounts SET balance = %s WHERE account_no = %s", (new_balance, account_no))
                logging.info(f"Successfully deposited {amount:.2f}. New balance: {new_balance:.2f}")
            else:
                logging.warning("Account not found.")
        except ValueError:
            logging.error("Invalid input! Please enter a valid amount.")

    def withdraw_money(self):
        try:
            account_no = int(input("Enter Account Number: "))
            amount = float(input("Enter Amount to Withdraw: "))
            
            result = self.db.execute("SELECT balance FROM accounts WHERE account_no = %s", (account_no,), fetch=True)
            if result:
                if result[0][0] >= amount:
                    new_balance = result[0][0] - amount
                    self.db.execute("UPDATE accounts SET balance = %s WHERE account_no = %s", (new_balance, account_no))
                    logging.info(f"Successfully withdrew {amount:.2f}. New balance: {new_balance:.2f}")
                else:
                    logging.warning("Insufficient balance.")
            else:
                logging.warning("Account not found.")
        except ValueError:
            logging.error("Invalid input! Please enter a valid amount.")

    def update_balance(self):
        try:
            account_no = int(input("Enter Account Number: "))
            new_balance = float(input("Enter New Balance: "))
            
            self.db.execute("UPDATE accounts SET balance = %s WHERE account_no = %s", (new_balance, account_no))
            if self.db.cursor.rowcount > 0:
                logging.info("Balance updated successfully!")
            else:
                logging.warning("Account not found.")
        except ValueError:
            logging.error("Invalid input! Please enter numeric values.")

    def delete_account(self):
        try:
            account_no = int(input("Enter Account Number to Delete: "))
            self.db.execute("DELETE FROM accounts WHERE account_no = %s", (account_no,))
            if self.db.cursor.rowcount > 0:
                logging.info("Account deleted successfully!")
            else:
                logging.warning("Account not found.")
        except ValueError:
            logging.error("Invalid input! Please enter a valid account number.")

    def run(self):
        while True:
            print("\n=== Banking System ===")
            print("1. Create Account")
            print("2. View Accounts")
            print("3. Deposit Money")
            print("4. Withdraw Money")
            print("5. Update Balance")
            print("6. Delete Account")
            print("7. Exit")
            choice = input("Enter your choice: ")
            
            actions = {
                '1': self.create_account,
                '2': self.view_accounts,
                '3': self.deposit_money,
                '4': self.withdraw_money,
                '5': self.update_balance,
                '6': self.delete_account
            }
            
            if choice in actions:
                actions[choice]()
            elif choice == '7':
                logging.info("Exiting program. Goodbye!")
                break
            else:
                logging.warning("Invalid choice. Please try again.")
        
        self.db.close()

if __name__ == "__main__":
    bank_system = BankSystem()
    bank_system.run()
