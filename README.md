class Account:
    def __init__(self, account_number, account_holder, pin, balance=0):
        self.account_number = account_number
        self.account_holder = account_holder
        self.pin = pin
        self.balance = balance
        self.transactions = []

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            self.transactions.append(f"Deposited: ${amount}")
            print(f"${amount} deposited successfully.")
        else:
            print("Invalid deposit amount.")

    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            self.balance -= amount
            self.transactions.append(f"Withdrew: ${amount}")
            print(f"${amount} withdrawn successfully.")
        else:
            print("Insufficient balance or invalid withdrawal amount.")

    def check_balance(self):
        print(f"Current balance: ${self.balance}")
        return self.balance

    def view_transactions(self):
        print("Transaction History:")
        for transaction in self.transactions:
            print(transaction)


class ATM:
    def __init__(self):
        self.accounts = {}

    def create_account(self, account_number, account_holder, pin):
        if account_number in self.accounts:
            print("Account number already exists.")
        else:
            self.accounts[account_number] = Account(account_number, account_holder, pin)
            print(f"Account created successfully for {account_holder}.")

    def authenticate_user(self, account_number, pin):
        account = self.accounts.get(account_number)
        if account and account.pin == pin:
            return account
        else:
            print("Authentication failed. Invalid account number or PIN.")
            return None

    def run(self):
        while True:
            print("\n--- Welcome to the ATM ---")
            print("1. Create Account")
            print("2. Access Account")
            print("3. Exit")
            choice = input("Enter your choice: ")

            if choice == '1':
                self.handle_create_account()
            elif choice == '2':
                self.handle_access_account()
            elif choice == '3':
                print("Thank you for using the ATM. Goodbye!")
                break
            else:
                print("Invalid choice. Please try again.")

    def handle_create_account(self):
        account_number = input("Enter new account number: ")
        account_holder = input("Enter account holder name: ")
        pin = input("Enter new PIN: ")
        self.create_account(account_number, account_holder, pin)

    def handle_access_account(self):
        account_number = input("Enter your account number: ")
        pin = input("Enter your PIN: ")
        account = self.authenticate_user(account_number, pin)
        
        if account:
            while True:
                print("\n--- Account Menu ---")
                print("1. Check Balance")
                print("2. Deposit")
                print("3. Withdraw")
                print("4. View Transactions")
                print("5. Logout")
                choice = input("Enter your choice: ")

                if choice == '1':
                    account.check_balance()
                elif choice == '2':
                    amount = float(input("Enter deposit amount: "))
                    account.deposit(amount)
                elif choice == '3':
                    amount = float(input("Enter withdrawal amount: "))
                    account.withdraw(amount)
                elif choice == '4':
                    account.view_transactions()
                elif choice == '5':
                    print("Logging out...")
                    break
                else:
                    print("Invalid choice. Please try again.")


if __name__ == "__main__":
    atm = ATM()
    atm.run()








