# C-Programming-ATM-Machine
This C program simulates an ATM machine, allowing users to choose between savings or checking accounts, make deposits, withdraw funds, and view transaction history. It accurately stores transaction data, demonstrating basic file handling, user input processing, and data management in a simple banking system.




#include <stdio.h>
#include <string.h>

#define MAX_TRANSACTIONS 100

typedef struct {
char type[10];
int amount;
} Transaction;



void printWelcomeScreen() {
printf("======================================\n");
printf("=                                    =\n");
printf("=                                    =\n");
printf("=                                    =\n");
printf("=         Welcome to Abdul's ATM     =\n");
printf("=                                    =\n");
printf("=                                    =\n");
printf("=                                    =\n");
printf("======================================\n");
}



void printMainMenu() {
printf("======================================\n");
printf("=  What would you like to do today   =\n");
printf("=                                    =\n");
printf("=   1. Withdraw                      =\n");
printf("=   2. Deposit                       =\n");
printf("=   3. Check Balance                 =\n");
printf("=   4. Change PIN                    =\n");
printf("=   5. View Transaction History      =\n");
printf("=   6. Sign out                      =\n");
printf("=                                    =\n");
printf("======================================\n");
}



void printAccountMenu() {
printf("======================================\n");
printf("=  Select Account Type               =\n");
printf("=                                    =\n");
printf("=   1. Savings                       =\n");
printf("=   2. Checking                      =\n");
printf("=                                    =\n");
printf("======================================\n");
}



void printTransactionHistory(Transaction transactions[], int transactionCount) {
printf("======================================\n");
printf("=        Transaction History         =\n");
for (int i = 0; i < transactionCount; i++) {
printf("=  %s: %d\n", transactions[i].type, transactions[i].amount);
}
printf("======================================\n");
}



int main() {
int pin;
int options;
int withdraw;
int amount = 1000; 
int deposit;
int pin_attempts = 3; 
int new_pin;
int account_type;
Transaction transactions[MAX_TRANSACTIONS];
int transactionCount = 0;

printWelcomeScreen();

while (pin_attempts > 0) {
printf("Enter your pin: ");
scanf("%d", &pin);

if (pin == 1234) {
printAccountMenu();
printf("Enter the number for account type: ");
scanf("%d", &account_type);

do {
printMainMenu();
printf("Enter the number option you'd like: ");
scanf("%d", &options);

switch (options) {
case 1:
printf("Enter the amount to withdraw: ");
scanf("%d", &withdraw);
if (withdraw > amount) {
printf("Not enough balance to withdraw!\n");
} else {
amount -= withdraw;
printf("You have withdrawn %d. Your new balance is %d.\n", withdraw, amount);
strcpy(transactions[transactionCount].type, "Withdraw");
transactions[transactionCount].amount = withdraw;
transactionCount++;
}
break;

case 2:
printf("Enter the amount to deposit: ");
scanf("%d", &deposit);
amount += deposit;
printf("You have deposited %d. Your new balance is %d.\n", deposit, amount);
strcpy(transactions[transactionCount].type, "Deposit");
transactions[transactionCount].amount = deposit;
transactionCount++;
break;

case 3:
printf("Your balance is %d.\n", amount);
break;

case 4:
printf("Enter your new PIN: ");
scanf("%d", &new_pin);
pin = new_pin;
printf("Your PIN has been changed successfully.\n");
break;

case 5:
printTransactionHistory(transactions, transactionCount);
break;

case 6:
printf("Thank you for using Abdul's ATM. Goodbye!\n");
break;

default:
printf("You did not select one of the valid options!\n");
break;		
}
} while (options != 6);
break; 
} else {
pin_attempts--;
if (pin_attempts > 0) {
printf("Incorrect pin. %d tries left.\n", pin_attempts);
} else {
printf("Incorrect pin. No tries left. Exiting.\n");
}
}
}

return 0;
}
