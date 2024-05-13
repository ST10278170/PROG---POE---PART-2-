# PROG---POE---PART-2-

This is for PART 2 POE PROG Work....

In order to RUN the CODE, (1) First Build the Solution. (2) Then once the Solution is Built, (3) Run the CODE AND Wait.

(4) Finally Test the Code...

using System.Drawing;
using System.Reflection.Metadata.Ecma335;
using System.Security.Cryptography.X509Certificates;
using System.Transactions;

// Class to Run the Program for POE PART 2 - PROG //

public class Program
{
    static void Main(string[] args)
    {
        // This opens the Program up //
        List<Recipe> recipes = new List<Recipe>();

        while (true)
        {
            // Main menu for the Recipe Application Starting //
            // Display Menu Options //
            Console.WriteLine("Enter '1' - To Enter Recipe Details");
            Console.WriteLine("Enter '2' - To Display Recipe Details");
            Console.WriteLine("Enter '3' - To Display a Specific Recipe's Details");
            Console.WriteLine("Enter '4' - To Scale the Recipe");
            Console.WriteLine("Enter '5' - To Reset Scale Quantities");
            Console.WriteLine("Enter '6' - To Clear Recipe");
            Console.WriteLine("Enter '7' - To Exit Application");
            

            Console.Write("Enter the Number Value of what you wish to do: ");
            string choice = Console.ReadLine();
            // Switch Case Below to show the cases options of what a User Can do on the Application //
            switch (choice)
            {
                // Switch Case to Enter a Recipe //
                case "1":
                    addRecipe(recipes);
                    break;

                // Switch Case to Display the Inserted Recipe's Details //
                case "2":
                    recipeDisplay(recipes);
                    break;

                // Switch Case to Display a Specific Recipe Details //
                case "3":
                    recipeDisplayDetails(recipes);
                    break;

                // Switch Case to Scale the Recipe //
                case "4":
                    recipeScale(recipes);
                    break;

                // Switch Case to Reset the Scale of an Recipe Quantities //
                case "5":
                    recipeScaleReset(recipes);
                    break;

                // Switch Case to Clear the Recipe //
                case "6":
                    recipeClear(recipes);
                    break;

                // Switch Case to Exit the Application //
                case "7":
                    Console.WriteLine("Exiting the Application", Console.ForegroundColor = ConsoleColor.Blue);
                    Console.ForegroundColor = ConsoleColor.Red;
                    return;

                // If a Value is less than 0 (zero) & higher than 7 (seven) entered, display this Message: //
                default:
                    Console.Write("Invaild choice. Please choose a Valid Number available: ", Console.ForegroundColor);
                    break;
            }
        }
    }

    static void addRecipe(List<Recipe> recipes)
    {
        Recipe recipe = new Recipe();

        Console.Write("Enter the Recipe Name: ");
        recipe.RecipeName = Console.ReadLine();

        Console.Write("Enter the Number of Ingredients: ");
        int ingredient_No = Convert.ToInt32(Console.ReadLine());

        for (int i = 0; i < ingredient_No; i++)
        {
            Console.WriteLine($" Enter the Details for Ingredients {i + 1}: ");

            Console.Write($" Enter the Name of the Ingredients {i + 1}: ");
            string ingredientName = Console.ReadLine();

            Console.Write($" The Quanitiy of the Ingredients: ");
            double ingredientAmount = Convert.ToDouble(Console.ReadLine());

            Console.Write($" The Unit of Measurement for the Ingredients: ");
            string ingredientMeasurement = Console.ReadLine();

            Console.Write($" The Calories in the Ingredients: ");
            double ingredientCalories = Convert.ToDouble(Console.ReadLine());

            Console.Write($" The Food Group the Ingredient belongs too: ");
            string ingredientFoodGroup = Console.ReadLine();

            recipe.addIngredient(ingredientName, ingredientAmount, ingredientMeasurement, ingredientCalories, ingredientFoodGroup);

        }

        Console.Write("Enter the Number of Steps for a User to Follow:  ");
        int steps_No = Convert.ToInt32(Console.ReadLine());

        // Below the Array is Initialized for All Steps & Full Descriptions of Steps //
        Console.WriteLine("Write a Description for each Step");

        for (int s = 0; s < steps_No; s++)
        {
            Console.WriteLine($" Step {s + 1}: ");
            recipe.addStep(Console.ReadLine());
        }

        recipe.calculateTotalCalories();
        if (recipe.TotalCalories > 300)
        {
            Console.WriteLine("Warning! Total Calories have exceeded 300!", Console.ForegroundColor = ConsoleColor.Blue);
            Console.ForegroundColor = ConsoleColor.Red;
        }

        recipes.Add(recipe);
    }

    static void recipeDisplay(List<Recipe> recipes)
    {
        // Should there be no recipes then nothing to Display otherwise, Display the Recipe to the User //
        if (recipes.Count > 0)
        {
            // Display all Ingredients //
            Console.WriteLine(" List of Recipes: ");
            foreach (var recipe in recipes.OrderBy(r => r.RecipeName))
            {
                Console.WriteLine(recipe.RecipeName);
            }

        }

        // Else Nothing is ment too be Displayed //
        else
        {
            Console.WriteLine("There is Nothing to Display", Console.ForegroundColor = ConsoleColor.Blue);
            Console.ForegroundColor = ConsoleColor.Red;
            return;
        }

    }

    static void recipeDisplayDetails(List<Recipe> recipes)
    {
        // Should there be no recipes then nothing to Display otherwise, Display the Recipe to the User //
        if (recipes.Count > 0)
        {
            // Ask the User which Recipe he/she wants to see: //
            Console.WriteLine("Enter the Name of the Recipe you want to see: ");
            string recipeName = Console.ReadLine();

            // Searching for the Recipe in the list, NOT interfering with other Switch-Casing //
            Recipe recipe = recipes.Find(r => r.RecipeName.Equals(recipeName, StringComparison.OrdinalIgnoreCase));
            if (recipe == null)
            {
                Console.WriteLine("Recipe NOT found", Console.ForegroundColor = ConsoleColor.Blue);
                Console.ForegroundColor = ConsoleColor.Red;
            }

            recipe.recipeDisplay();
        }

        // Else no Recipe to Display //
        else
        {
            Console.WriteLine("There is nothing to Display", Console.ForegroundColor = ConsoleColor.Blue);
            Console.ForegroundColor = ConsoleColor.Red;
            return;
        }
    }

    static void recipeScale(List<Recipe> recipes)
    {
        // If the Recipe isn't unavailable, then change the Scale Settings below: //
        if (recipes.Count > 0)
        {
            // Select the Recipe the User wants to Scale: //
            Console.WriteLine("Enter the Name of the Receipe you want to Scale: ");
            string recipeName = Console.ReadLine();

            Recipe recipe = recipes.Find(r => r.RecipeName.Equals(recipeName, StringComparison.OrdinalIgnoreCase));

            if (recipe == null)
            {
                Console.WriteLine("Recipe NOT found", Console.ForegroundColor = ConsoleColor.Blue);
                Console.ForegroundColor = ConsoleColor.Red;
                return;
            }

            Console.Write("Enter the Scaling Factor(0.5 , 2 , 3): ");
            double scaleAmount = Convert.ToDouble(Console.ReadLine());

            recipe.recipeScale(scaleAmount);
            Console.WriteLine("Recipe Successfully Scaled!");

        }

        // Else No Recipe to Scale //
        else
        {
            Console.WriteLine("There is No Recipe to Scale", Console.ForegroundColor = ConsoleColor.Blue);
            Console.ForegroundColor = ConsoleColor.Red;
            return;
        }
    }

    static void recipeScaleReset(List<Recipe> recipes)
    {
        // If the Recipe isn't empty, then change the Scale Settings for the Recipe: //
        if (recipes.Count > 0)
        {
            // A User can Select the Reset Scale option //
            Console.Write("Enter the Name of the Recipe you want to Reset the Scale of: ");
            string recipeName = Console.ReadLine();

            Recipe recipe = recipes.Find(r => r.RecipeName.Equals(recipeName, StringComparison.OrdinalIgnoreCase));

            if (recipe == null)
            {
                Console.WriteLine("Recipe with the Name NOT found");
                return;
            }

            recipe.recipeScaleReset();
            Console.WriteLine("Recipe Scale Successfully Reset!");
        }

        // Else No Recipe to Reset the Scale of //
        else
        {
            Console.WriteLine("There is No Recipe too Reset any Scale of");
            return;
        }
    }


    static void recipeClear(List<Recipe> recipes)
    {
        //If the Recipe NOT available, then Clear it Away //
        if (recipes.Count > 0)
        {
            // Select the Recipe the User wants to Rescale OR Clear Away Completly //
            Console.Write("Enter the Name of the Recipe you want to Remove: ");
            string recipeName = Console.ReadLine();

            Recipe recipe = recipes.Find(r => r.RecipeName.Equals(recipeName, StringComparison.OrdinalIgnoreCase));

            if (recipe == null)
            {
                Console.WriteLine("Recipe with that Name NOT found");
                return;
            }

            recipes.Clear();
            Console.WriteLine("Recipe Successfully Removed!");
        }

        // Else No Recipe to Reset the Scale of OR Remove Away //
        else
        {
            Console.WriteLine("There is No Recipe to Remove");
            return;
        }
    }
}
