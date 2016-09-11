/**
* This program simulates a simple ATM environment.
* ATM supports deposits, withdrawals and balance inquiries.
* 
* @version 0.1
*
*/


import java.text.NumberFormat; // Helps with formatting doubles as currency
import java.util.Scanner; // Will be used to get input from the user
/**
 * 
 * @author mgichuhi
 *
 */
public class ATM {  //main class for the 
	
	public static void main(String[] args) {
	
		// Create and instantiate two Account objects

		Account savings = new Account();
		savings.setType("Savings");
		savings.setBalance(0.00);
		savings.setRate(2.00);
		int withdrawals = 0;
		int deposits = 0;
		double depo_amounts = 0;
		double withdraw_amounts = 0;

		NumberFormat formatter = NumberFormat.getCurrencyInstance(); // Creates the formatter object for currency
		Scanner sc = new Scanner(System.in); // Creates the sc object to read user input

		boolean session = true; // This variable will break the (while) loop when false

		while (session) {

			// Present the user with a menu of 4 options

			System.out.print("========================\n"
							 +"ATM Menu: \n \n"
							 + "1. Deposit Money \n"
							 + "2. Withdraw Money \n"
							 + "3. Check Account Balance\n"
							 + "4. Quit \n"
							 + "========================\n"
							 + "\nEnter selection: ");

			int selection = sc.nextInt(); // assign the user's input to the selection variable

			// This switch block will handle one of five selections and deal with them appropriately

			switch (selection) {

				// case 1 handles the depositing of money

				case 1:
					//System.out.print("Enter (1) for Savings or (2) for Checking: ");
					System.out.print("Enter (1) for Savings Account:: ");
					int depAccount = sc.nextInt(); // Keeps track of which account to deposit money to

					if (depAccount == 1) {
						if (deposits < 4 ){
							if (depo_amounts < 150000){
								System.out.println("\nYour current Savings balance is: " + formatter.format(savings.getBalance()) + "\n");
		
								System.out.println("How much money would you like to deposit?");
								double deposit = sc.nextDouble();
								//Track if instance of deposit is 40K
								if (deposit <40000){
								savings.deposit(deposit);
								
								depo_amounts += deposit;// for checking deposit amounts in the day
								deposits += 1; // increment the number of deposits
								
								System.out.println("\nYour Savings balance is now: " + formatter.format(savings.getBalance()) + "\n");
								}else {System.out.println("\n You can't deposit more than 40K per transaction \n"); break;}
							}else {System.out.println("\n You have deposited maximum amounts of Money for today \n"); break;}
						}
						else {
							System.out.println("\n You have reached the maximum number of deposists per sesion ..  kwaheri \n");
							break;
							}
						}

					

					else if (depAccount != 1) {
						
						System.out.println("\n Invalid entry Good Bye!!! \n");
						
						break;

						}

					break;

				

				// case 2 handles the withdrawal of money	

				case 2:
					//System.out.print("\nEnter (1) for Savings or (2) for Checking: ");
					System.out.print("\nEnter (1) for Savings : ");
					int witAccount = sc.nextInt(); // Keeps track of which account to withdraw from savings account

					if (witAccount == 1) {
						if (withdrawals < 3){
						if (withdraw_amounts <= 50000){
						System.out.println("\nYour current Savings balance is: " + formatter.format(savings.getBalance()) + "\n");

						System.out.println("How much money would you like to withdraw?");
						double withdraw = sc.nextDouble();
						if (withdraw <= 20000){
						savings.withdraw(withdraw);
						withdraw_amounts += withdraw;
						withdrawals += 1;
						System.out.println("\nYour Savings balance is now: " + formatter.format(savings.getBalance()) + "\n");
						}else {System.out.println("\n You can not withdraw more than 20K Per trans \n "); break;}
						}else {System.out.println("\n You can not withdraw more than 50K in a day \n "); break;}
						}else{System.out.println("\n Reached Maximum number of withdrawals \n "); break;}
							

					}

					else if (witAccount != 1) {
						System.out.println("\n Invalid entry Good Bye!!!  \n");
						break;
					}

					break;

				// case 3 simply outputs the balances of both Checking and Savings accounts	
				
				case 3:
				
					System.out.println("Savings Balance: " + formatter.format(savings.getBalance()) + "\n");
					
					break;

				// case 4 breaks out of the (while) loop when the user is finished using the ATM

				case 4:
					session = false;
					
					break;

			}				 	
			

		}

		System.out.println("\nThank you for banking with us!\n");

	}

}


class Account {

	// Here we declare some variables that a typical bank account will have

	String type;
	double balance;
	double rate;

	// The following methods are a combination of getter/setter methods as well
	// as two special deposit() and withdraw() methods

	void setType(String accType) {
		
		type = accType;
	}

	void setBalance(double accBal) {
		
		balance = accBal;
	}

	void setRate(double accRate) {
		
		rate = accRate;
	}

	void deposit(double dep) {
		
		balance += dep; // Take the Account object's balance and add to it the current deposit
	}

	void withdraw(double wit) {
		
		balance -= wit; // Take the Account object's balance and subtract from it the current withdrawal
	}


	String getType() {
		
		return type;
	}

	double getBalance() {
		
		return balance;
	}

	double getRate() {
		
		return rate;
	}

}
