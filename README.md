# BANK-MANAGEMENT-
A simple, console-based Bank Management System written in modern C++ that demonstrates core OOP concepts, basic persistence (file/JSON-like), and common banking workflows (create account, deposit, withdraw, transfer, close account, and mini-statement). Great for beginners practicing C++, data structures, and clean code.
#include <stdio.h>
#include <string.h>

#define MAX 100

struct Account {
    int acc_no;
    char name[50];
    float balance;
};

struct Account accounts[MAX];
int count = 0;

void createAccount() {
    if (count >= MAX) {
        printf("Account limit reached.\n");
        return;
    }

    printf("Enter Account Number: ");
    scanf("%d", &accounts[count].acc_no);
    printf("Enter Name: ");
    scanf(" %[^\n]", accounts[count].name);
    printf("Enter Initial Balance: ");
    scanf("%f", &accounts[count].balance);

    printf("Account created successfully!\n");
    count++;
}

void displayAccounts() {
    if (count == 0) {
        printf("No accounts to display.\n");
        return;
    }

    for (int i = 0; i < count; i++) {
        printf("\nAccount No: %d\nName: %s\nBalance: %.2f\n", accounts[i].acc_no, accounts[i].name, accounts[i].balance);
    }
}

void depositMoney() {
    int acc_no;
    float amount;
    printf("Enter Account Number: ");
    scanf("%d", &acc_no);

    for (int i = 0; i < count; i++) {
        if (accounts[i].acc_no == acc_no) {
            printf("Enter Amount to Deposit: ");
            scanf("%f", &amount);
            accounts[i].balance += amount;
            printf("Deposit Successful!\n");
            return;
        }
    }

    printf("Account not found.\n");
}

void withdrawMoney() {
    int acc_no;
    float amount;
    printf("Enter Account Number: ");
    scanf("%d", &acc_no);

    for (int i = 0; i < count; i++) {
        if (accounts[i].acc_no == acc_no) {
            printf("Enter Amount to Withdraw: ");
            scanf("%f", &amount);

            if (amount > accounts[i].balance) {
                printf("Insufficient Balance!\n");
            } else {
                accounts[i].balance -= amount;
                printf("Withdrawal Successful!\n");
            }
            return;
        }
    }

    printf("Account not found.\n");
}

int main() {
    int choice;

    do {
        printf("\n=== Simple Bank System ===\n");
        printf("1. Create Account\n");
        printf("2. Display Accounts\n");
        printf("3. Deposit Money\n");
        printf("4. Withdraw Money\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: createAccount(); break;
            case 2: displayAccounts(); break;
            case 3: depositMoney(); break;
            case 4: withdrawMoney(); break;
            case 5: printf("Exiting...\n"); break;
            default: printf("Invalid choice. Try again.\n");
        }

    } while (choice != 5);

    return 0;
}
