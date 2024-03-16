# Bank-Account-Management-Application-console-application-
BANKING APPLICATION

package bankaccountapp;

import java.util.ArrayList;
import java.util.List;
import java.util.Random;

interface Account {
    void deposit(double amount);
    void withdraw(double amount);
    void transfer(Account destination, double amount);
    void showInfo();
    String getAccountNumber(); // Added method
}

class SavingsAccount implements Account {
    private String name;
    private String ssn;
    private double balance;
    private int safetyDepositBox;
    private int safetyDepositCode;
    private String accountNumber;

    public SavingsAccount(String name, String ssn, double initialDeposit) {
        this.name = name;
        this.ssn = ssn;
        this.balance = initialDeposit;
        this.safetyDepositBox = generateSafetyDepositBox();
        this.safetyDepositCode = generateSafetyDepositCode();
        this.accountNumber = generateAccountNumber();
    }

    @Override
    public void deposit(double amount) {
        balance += amount;
        System.out.println("Depositing $" + amount);
    }

    @Override
    public void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
            System.out.println("Withdrawing $" + amount);
        } else {
            System.out.println("Insufficient funds");
        }
    }

    @Override
    public void transfer(Account destination, double amount) {
        if (balance >= amount) {
            withdraw(amount);
            destination.deposit(amount);
            System.out.println("Transferring $" + amount + " to " + destination.getAccountNumber());
        } else {
            System.out.println("Insufficient funds for transfer");
        }
    }

    @Override
    public void showInfo() {
        System.out.println("Account Type: Savings");
        System.out.println("Name: " + name);
        System.out.println("SSN: " + ssn);
        System.out.println("Balance: $" + balance);
        System.out.println("Account Number: " + accountNumber);
        System.out.println("Safety Deposit Box Number: " + safetyDepositBox);
        System.out.println("Safety Deposit Box Code: " + safetyDepositCode);
    }

    private int generateSafetyDepositBox() {
        Random random = new Random();
        return 100 + random.nextInt(900);
    }

    private int generateSafetyDepositCode() {
        Random random = new Random();
        return 1000 + random.nextInt(9000);
    }

    private String generateAccountNumber() {
        return "1" + ssn.substring(ssn.length() - 2) + generateUniqueNumber() + generateRandomNumber();
    }

    private String generateUniqueNumber() {
        // Assuming some logic to generate a unique 5-digit number
        return "00000";
    }

    private String generateRandomNumber() {
        Random random = new Random();
        return String.format("%03d", random.nextInt(1000));
    }

    public String getAccountNumber() {
        return accountNumber;
    }
}

class CheckingAccount implements Account {
    private String name;
    private String ssn;
    private double balance;
    private String accountNumber;

    public CheckingAccount(String name, String ssn, double initialDeposit) {
        this.name = name;
        this.ssn = ssn;
        this.balance = initialDeposit;
        this.accountNumber = generateAccountNumber();
    }

    @Override
    public void deposit(double amount) {
        balance += amount;
        System.out.println("Depositing $" + amount);
    }

    @Override
    public void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
            System.out.println("Withdrawing $" + amount);
        } else {
            System.out.println("Insufficient funds");
        }
    }

    @Override
    public void transfer(Account destination, double amount) {
        if (balance >= amount) {
            withdraw(amount);
            destination.deposit(amount);
            System.out.println("Transferring $" + amount + " to " + destination.getAccountNumber());
        } else {
            System.out.println("Insufficient funds for transfer");
        }
    }

    @Override
    public void showInfo() {
        System.out.println("Account Type: Checking");
        System.out.println("Name: " + name);
        System.out.println("SSN: " + ssn);
        System.out.println("Balance: $" + balance);
        System.out.println("Account Number: " + accountNumber);
    }

    private String generateAccountNumber() {
        return "2" + ssn.substring(ssn.length() - 2) + generateUniqueNumber() + generateRandomNumber();
    }

    private String generateUniqueNumber() {
        // Assuming some logic to generate a unique 5-digit number
        return "00000";
    }

    private String generateRandomNumber() {
        Random random = new Random();
        return String.format("%03d", random.nextInt(1000));
    }

    public String getAccountNumber() {
        return accountNumber;
    }
}

public class BankApplication {
    public static void main(String[] args) {
        List<Account> accounts = new ArrayList<>();

    
        for (Account account : accounts) {
            account.deposit(500.0);
            account.withdraw(200.0);
            account.showInfo();
            System.out.println();
        }
    }
}

