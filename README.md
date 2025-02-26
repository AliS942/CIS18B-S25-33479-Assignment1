# CIS18B-S25-33479-Assignment1
How to run the program::
Install Java – Ensure Java is installed (java -version).
Clone Repository - git clone https://github.com/<your_username>/CIS18B-S25-33479-Assignment1.git    
Compile the Program - javac SimpleBankingSystem.java  
Run the Program - java SimpleBankingSystem  
Follow Menu Options – Create an account, deposit/withdraw money, check balance, or exit.


import java.util.Scanner;

// BankAccount class to manage account operations
class BankAccount {
    private String accountHolderName;
    private int accountNumber;
    private double balance;
    
    // Static variable to generate unique account numbers
    private static int accountCounter = 1000;
    
    // Constructor
    public BankAccount(String accountHolderName, double initialBalance) {
        this.accountHolderName = accountHolderName;
        this.accountNumber = accountCounter++;
        this.balance = initialBalance;
    }
    
    // Method to deposit money
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposit successful! New balance: $" + balance);
        } else {
            System.out.println("Invalid deposit amount. Please enter a positive number.");
        }
    }
    
    // Method to withdraw money
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawal successful! New balance: $" + balance);
        } else if (amount > balance) {
            System.out.println("Insufficient funds!");
        } else {
            System.out.println("Invalid withdrawal amount. Please enter a positive number.");
        }
    }
    
    // Method to check balance
    public double getBalance() {
        return balance;
    }
    
    // Method to display account details
    public void displayAccountDetails() {
        System.out.println("Account Holder: " + accountHolderName);
        System.out.println("Account Number: " + accountNumber);
        System.out.println("Current Balance: $" + balance);
    }
}

// Main class to handle user interactions
public class SimpleBankingSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        BankAccount userAccount = null;
        
        while (true) {
            // Display menu
            System.out.println("\nWelcome to Simple Bank System");
            System.out.println("1. Create Account");
            System.out.println("2. Deposit Money");
            System.out.println("3. Withdraw Money");
            System.out.println("4. Check Balance");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            
            try {
                int choice = Integer.parseInt(scanner.nextLine());
                
                switch (choice) {
                    case 1:
                        System.out.print("Enter account holder name: ");
                        String name = scanner.nextLine();
                        System.out.print("Enter initial deposit: ");
                        double initialDeposit = Double.parseDouble(scanner.nextLine());
                        
                        if (initialDeposit < 0) {
                            System.out.println("Initial deposit cannot be negative.");
                            break;
                        }
                        
                        userAccount = new BankAccount(name, initialDeposit);
                        System.out.println("Account created successfully!");
                        userAccount.displayAccountDetails();
                        break;
                    
                    case 2:
                        if (userAccount == null) {
                            System.out.println("Please create an account first.");
                            break;
                        }
                        System.out.print("Enter amount to deposit: ");
                        double depositAmount = Double.parseDouble(scanner.nextLine());
                        userAccount.deposit(depositAmount);
                        break;
                    
                    case 3:
                        if (userAccount == null) {
                            System.out.println("Please create an account first.");
                            break;
                        }
                        System.out.print("Enter amount to withdraw: ");
                        double withdrawAmount = Double.parseDouble(scanner.nextLine());
                        userAccount.withdraw(withdrawAmount);
                        break;
                    
                    case 4:
                        if (userAccount == null) {
                            System.out.println("Please create an account first.");
                            break;
                        }
                        System.out.println("Current balance: $" + userAccount.getBalance());
                        break;
                    
                    case 5:
                        System.out.println("Thank you for using Simple Bank System! Goodbye.");
                        scanner.close();
                        return;
                    
                    default:
                        System.out.println("Invalid choice. Please enter a number between 1 and 5.");
                }
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a valid number.");
            }
        }
    }
}
