using System;

namespace Nepal Coffee
{
    class Program
    {
        static void Main(string[] args)
        {
            // Declaring N and allocating a value
            int n = 5;
            // declaring arrays to store data
            String[] name = new string[n];
            int[] quantity = new int[n];
            String[] reseller = new string[n];
            double[] charge = new double[n];
            double price;
            double min = 9999999;
            String minName = "";
            double max = -1;
            String maxName = "";
            int beanCount;
            // Welcome message
            Console.WriteLine("\t\t\t\tWelcome to use Nepal Coffee Program\n");

            // Loop to get the inputs
            for (int i = 0; i < n; i++)
            {
                Console.Write("Enter customer name: ");
                name[i] = Console.ReadLine();

                quantity[i] = 0;
                // The loop will continue if an entered value for coffee beans bag is not a valid number and the entered number is not between 1 and 200
                bool validCoffeeBeanCount = false;
                while (validCoffeeBeanCount == false)
                {
                    Console.Write("Enter the number of coffee beans bags (bag/1kg): ");
                    if (Int32.TryParse(Console.ReadLine(), out beanCount))
                    {
                        if (beanCount < 1 || beanCount > 200)
                        {
                            Console.WriteLine("Invalid Input!\nCoffee bags between 1 and 200 can be ordered.\n");
                            validCoffeeBeanCount = false;
                        }
                        else
                        {
                            validCoffeeBeanCount = true;
                            quantity[i] = beanCount;
                        }
                    }
                    else
                    {
                        Console.Write("Invalid entry. Only numeric values allowed for coffee bean bags count: \n");
                        validCoffeeBeanCount = false;
                    }
                }

                // determining the price
                if (quantity[i] <= 5)
                {
                    price = 36 * quantity[i];
                }
                else if (quantity[i] <= 15)
                {
                    price = 34.5 * quantity[i];
                }
                else
                {
                    price = 32.7 * quantity[i];
                }

                Console.Write("Enter yes/no to indicate whesther you are a reseller: ");
                reseller[i] = Console.ReadLine();

                if (reseller[i].ToLower() == "yes")
                {
                    // 20% discount
                    charge[i] = price * 0.8;
                }
                else
                {
                    charge[i] = price;
                }
                Console.WriteLine(String.Format("The total sales value from {0} is ${1}", name[i], charge[i].ToString("00.00")));
                Console.WriteLine("-----------------------------------------------------------------------------");

                // finding max min value
                if (min > charge[i])
                {
                    min = charge[i];
                    minName = name[i];
                }

                if (max < charge[i])
                {
                    max = charge[i];
                    maxName = name[i];
                }
            }

            // summary heading
            Console.WriteLine("\t\t\t\t\tSummary of sales\n");
            Console.WriteLine("-----------------------------------------------------------------------------");
            Console.WriteLine("-----------------------------------------------------------------------------");

            // displaying table header
            Console.WriteLine(String.Format("{0,15}{1,10}{2,10}{3,10}",
            "Name", "Quantity", "Reseller", "Charge"));

            // displaying table data
            for (int i = 0; i < n; i++)
            {
                Console.WriteLine(String.Format("{0,15}{1,10}{2,10}{3,10}",
                name[i], quantity[i], reseller[i], charge[i].ToString("00.00")));
            }

            Console.WriteLine("-----------------------------------------------------------------------------");
            Console.WriteLine("-----------------------------------------------------------------------------");
            Console.WriteLine(String.Format("The customer spending most is {0} ${1}", maxName, max.ToString("00.00")));
            Console.WriteLine(String.Format("The customer spending least is {0} ${1}", minName, min.ToString("00.00")));

        }
    }
}
