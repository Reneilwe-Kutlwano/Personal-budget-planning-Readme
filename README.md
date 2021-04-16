# Personal-budget-planning-Readme
using System;
using System.Globalization;

namespace PersonalBudgetPlanning
{

    class PersonalBudgetPlanning
    {
        
        //Driver class
        static void Main(string[] args)
        {
            //Obtaining user input.
            Console.WriteLine("************************************USER EXPENSES**************************************");
            Console.Write("Please enter your gross monthly income before deductions :");
            double monthlyIncome = Convert.ToDouble(Console.ReadLine());
            Console.Write("Please enter your estimated monthly tax deducted :");
            double taxDeducted = Convert.ToDouble(Console.ReadLine());
            Console.ReadLine();

            //Storing the expenses in an array.
            //This gets input from users and stores it within the array.

            double[] expenses = new double[6]; //Declaring the size of the array.
            int a = 0;
            double b = Convert.ToDouble(a); //Coverting to a double in order to take the double from the user input.

            for (a = 0; a < expenses.Length; a++) //For loop to get a value from the user .
            {
                Console.Write("\nPlease enter your monthly expenditures in the order of (1) groceries, " +
                    "(2) water and lights, (3) travel costs, (4) cellphone, (5) telephone, (6) other expenses\t:");
                expenses[a] = Convert.ToDouble(Console.ReadLine());
            }

            Console.WriteLine("-----------------------------------------------------------------------------------------------");


            //Decison for user to choose between renting and buying.
            Console.Write("Please press (1) if you would like to RENT the accomodation or press (0) if you would like to BUY the property:");
            string choice = Console.ReadLine();
            int decision = Int32.Parse(choice);

            //If-else statement to determine what would happen if the user selects a specific choice.
            if (decision > 0)
            {
                Console.Write("Please enter your monthly rental amount :");
                double monthlyRental = Convert.ToDouble(Console.ReadLine());

                double monthlyMoneyAvail;
                monthlyMoneyAvail = monthlyIncome - taxDeducted - (expenses[0] + expenses[1] + expenses[2] + expenses[3] + expenses[4]
                    + expenses[5]) - monthlyRental; //Equation to calaculate the monthly available money after deductions.

                Console.WriteLine("Your available monthly money after deductions is :" + monthlyMoneyAvail);
            }

            else
            {
                Console.Write("Please enter the purchase price of the property :");
                double purchasePrice = Convert.ToDouble(Console.ReadLine());

                Console.Write("Please enter the total deposit :");
                double deposit = Convert.ToDouble(Console.ReadLine());

                Console.Write("Please enter the interest rate :");
                double interest = (Convert.ToDouble(Console.ReadLine())) / 100;

                Console.Write("Please enter the number of months to repay the loan between 240 and 360 :");
                double monthsToRepay = (Convert.ToDouble(Console.ReadLine())) / 12;
                Console.WriteLine("-------------------------------------------------------------------------------------------");
                

                //Main method
                HomeLoan h = new HomeLoan();
                //calling the abstract method.
                h.homeLoanRepayment();

                double repayment = (purchasePrice - deposit * (1 + (interest * monthsToRepay)));
                double grossMonthlyIncome;
                grossMonthlyIncome = monthlyIncome / 3;

                //if statement to see if the home loan would be approved or not.
                if (repayment > grossMonthlyIncome)
                {
                    Console.Write("ERROR MESSAGE: The approval of the home loan is unlikely");
                    Console.WriteLine("--------------------------------------------------------------------------------");
                }

                else
                {
                    Console.Write("The monthly home loan repayments are :" + repayment);
                    Console.WriteLine("\n----------------------------------------------------------------------------\t");

                    double monthlyMoneyAvail2;
                    monthlyMoneyAvail2 = monthlyIncome - taxDeducted - (expenses[0] + expenses[1] + expenses[2] + expenses[3] + expenses[4]
                    + expenses[5]) - repayment;

                    Console.Write("\nYour available monthly money after deductions is :\t" + monthlyMoneyAvail2);

                    Console.WriteLine("\n----------------------------------------------------------------------------\t");
                }
            }
        }
     }
  }

 

    using System;
using System.Collections.Generic;
using System.Text;

namespace PersonalBudgetPlanning
{
    
    //Declaring the abstract class Expense in which home loan will be derived from.
    abstract class Expense
    {
        //Method to calculate the home loan repayment within the home loan class.
        public abstract double homeLoanRepayment();
    }

    //This class is the class that will inherit from the Expense class.
    //Child class
    class HomeLoan : Expense
    {
        double deposit;
        double interest;
        double purchasePrice;
        double monthsToRepay;
        double repayment;
        private int monthlyIncome;

        public HomeLoan()
        {
        }

        public  HomeLoan(double deposit, double interest, double purchasePrice, double monthsToRepay, double repayment)
        {
            //if statement to see whether the homeloan will be likely or not.
            if (repayment > (monthlyIncome / 3))
            {
                Console.Write("ERROR MESSAGE: The approval of the home loan is unlikely");
            }
            else
            {
                Console.Write("");
            }

                }
            
        //Method to calculate the total home loan repayment.
        public override double homeLoanRepayment()
        {
            return repayment = (purchasePrice - deposit * (1 + (interest * monthsToRepay)));
         }
       }
      }
    

    =========================DESCRIPTION==============================
This particular project is a personal budget planning application that is used to solve the problem of not being able to fully calculate and plan out your budget. This application provides an easier seamless way of calculating all of the important aspects of creating a budget, by asking the user to input their expenses, monthly income, tax deductions and also whether they are renting and paying a monthly rental or they are buying and paying a monthly repayment. The application uses the users input and calculates how much is available at the end of the month along with how much they actually pay on either their monthly rental or monthly repayment.

The motivation behind the project for me was to be able to create a user friendly application that won't confuse the user along with the coder who wrote this program. From a personal experience alot of people do struggle with being able to plan out their finances and create a budget because it is so time consuming. With this project i just wanted to create something that will be less time consuming for the user and accurate as possible.

=======================HOW THE CODE WORKS==================================

The code of the application consists of a parent class and a child class. The parent class i have called "PersonalBudgetPlanning" as seen on line 8. This class is the main class where all of the aspects of the application are found. Immediately in the Main, I have created a command line prompt that will prompt the user to enter their gross monthly income before deductions and their estimated monthly tax deducted. I have stored/convert these inputs into a double data type and this is purely because when working with money there is almost most of the time cents. As per instructed in the brief I was given the expenses that the user would enter based on specific categories, had to all be stored within an array. This enabled for the flexibility of the user input in terms of expenses. I had declared the array with a size that is somewhat flexible. I have used a for loop in order to obtain a value from he user and immediately store that into the array.

Apart from the user inputting their values a decison had to be made. The brief i had recieved, indicated that the user should be prompt to choose whether they want to rent the accomodation or buy the property. In order to handle this situation i had created an If-else statement. The if-else statment would execute a block of code when evaluated to be true, however when false the else statement would be excuted. In my above code the user would be prompted to press (1) if they want to rent the accomodation and press (2) if they want to buy the property. In order for the code to be executed i had created a condition as shown on line 45 that will take the user input that i have declared as "decision" and compare it against the value of 0. If the user inputs (1) then the condition will compare if 1 is greater that 0 and this will then execute the code in the if body which prompts the user to enter their monthly rental amount. Once the user enters their monthly rental amount and their input is converted to a double then the system would have to calaculate the monthly money available after deductions. For this i have created an equation to be able to calculate the monthly money available, i first declared the variable i was going to use called "double monthlyMoneyAvail" i then equated this to the monthly income subtracted by the tax deducted subtracted by the expenses that have been stored in the array and then subtraced by the monthly rental. A message will then be dispayed to inform the user how much is available after the deductions.
If the users inputs 0 the condition will then be determined and found to be false, the second block of code will then execute, which will then prompt the user to enter values that have to do with a home loan. I have divided the user input of the interest by 100 because interest rate is always a percentage and the number of months also had to be divided by 12 because in order for the monthly repayment to be calculated the months need to be converted into years hence the division that is occuring.

After this else statment i had to go an created an abstract class called "Expense" from which "Home loan" could be derived from. As seen on line 117 I had to first declare the class "Expense" as abstract, within that class i had then declared the absract method called "homeLoanRepayment", this method will later calculate the monthly repayment. On line 125 i had to implement the child class within the "Expense" class that will inherit attributes. This child class consists of a "HomeLoan" method that contains an if statement that is also in the main class. This if statment is used to see whether the home loan would be approved or not based on whether the users repayment amount is greater than a third of the users gross monthly income hence in the condition the monthly income is being divide by 3. If the condition evaluates to true then an alert message will be shown to inform the user that the approval of the home loan is unlikely. After the if statement the homeLoanRepament method is used to calculate the monthly repayment, in order to achieve this calculation i had used the simple interest formula because the user will constantly have interest added to their loan.

On line 73 I am calling the abstract class into the main along with its method. I have just also placed the if statment within the absract class in this class as well and also calculated the monthly money available for the home loan option by using the same method in line 51 and replacing a few aspects.

The language used throughout this entire code is C# (.NET FRAMEWORK), built with Visual Studio 2019 and i have used the standard coding style.

If you would like to test out the project check out the code above, copy it into your visual studio and run it!

--HAPPY CODING!!
All of my coding references were found on https://www.geeksforgeeks.org/.

