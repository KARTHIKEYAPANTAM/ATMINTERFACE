import java.util.ArrayList;
import java.util.Scanner;

public class ATMinter {
    public static Scanner sc = new Scanner(System.in);
    public static ArrayList<String> list = new ArrayList<>();
    public static int balance = 1000;

    public static void main(String[] args) {
        System.out.println("---------------**Login!**---------------");
        login();
    }

    public static void login() {
        System.out.print("Enter username: ");
        String username = sc.next();
        System.out.print("Enter PIN: ");
        int pin = sc.nextInt();

        if (username.equals("Karthik") && pin == 8255) {
            System.out.println("Logged in");
            showOptions();
        } else {
            System.out.println("Invalid username or PIN. Try again.");
            login();
        }
    }

    public static void showOptions() {
        System.out.println("----------------------------------------");
        System.out.println("1) Transaction History");
        System.out.println("2) Withdraw");
        System.out.println("3) Deposit");
        System.out.println("4) Transfer");
        System.out.println("5) Quit");
        System.out.print("Choose an action: ");
        int choice = sc.nextInt();
        System.out.println();

        switch (choice) {
            case 1:
                showTransactionHistory();
                break;
            case 2:
                withdraw();
                break;
            case 3:
                deposit();
                break;
            case 4:
                transfer();
                break;
            case 5:
                quit();
                break;
            default:
                System.out.println("Invalid choice. Try again.");
                showOptions();
        }
    }

    public static void showTransactionHistory() {
        System.out.println("----------Transaction History!----------");
        for (String transaction : list) {
            System.out.println(transaction);
        }
        System.out.println();
        showOptions();
    }

    public static void withdraw() {
        System.out.print("Enter amount to be withdrawn: ");
        int amount = sc.nextInt();

        if (amount > 0 && amount <= balance) {
            balance -= amount;
            list.add(amount + " rupees withdrawn.");
            System.out.println("Transaction successful. Current balance is " + balance);
        } else {
            System.out.println("Invalid amount. Try again.");
        }
        System.out.println();
        showOptions();
    }

    public static void deposit() {
        System.out.print("Enter amount to be deposited: ");
        int amount = sc.nextInt();

        if (amount > 0) {
            balance += amount;
            list.add(amount + " rupees deposited.");
            System.out.println("Transaction successful. Current balance is " + balance);
        } else {
            System.out.println("Invalid amount. Try again.");
        }
        System.out.println();
        showOptions();
    }

    public static void transfer() {
        System.out.print("Enter recipient's username: ");
        String recipient = sc.next();
        System.out.print("Enter amount to be transferred: ");
        int amount = sc.nextInt();

        if (amount > 0 && amount <= balance) {
            balance -= amount;
            list.add(amount + " rupees transferred to account " + recipient);
            System.out.println(amount + " rupees sent to " + recipient);
            System.out.println("Transaction successful. Current balance is " + balance);
        } else {
            System.out.println("Invalid amount. Try again.");
        }
        System.out.println();
        showOptions();
    }

    public static void quit() {
        System.out.print("Do you want to exit? (Yes/No): ");
        String response = sc.next();

        if (response.equalsIgnoreCase("Yes")) {
            System.out.println("---------------Logged out---------------");
            System.exit(0);
        } else {
            System.out.println();
            showOptions();
        }
    }
}
