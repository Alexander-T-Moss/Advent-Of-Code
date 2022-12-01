If your using Replit
--

Copy this into your replit ```main.cs``` and make sure your input file is called ```Input.txt```
```
using System;
using System.IO;
using System.Linq;

class Solution
{
  string[] Input;
  
  public Solution(string[] input)
  {
    Input = input;
  }

  public void Star1()
  {
    int[] totalCalories = new int[Int16.MaxValue];
    int elfNumber = 0;

    // Sum each elfs calories
    foreach(string line in Input)
    {
      if(line != "")
        totalCalories[elfNumber] += Convert.ToInt32(line);
      else
        elfNumber++;
    }
    Console.WriteLine("Star 1: " + totalCalories.Max());
  }

  public void Star2()
  {
    int[] totalCalories = new int[Int16.MaxValue];
    int elfNumber = 0;

    // Sum each elfs calories
    foreach(string line in Input)
    {
      if(line != "")
        totalCalories[elfNumber] += Convert.ToInt32(line);
      else
        elfNumber++;
    }

    // Find sum of top 3 elements in totalCalories
    int maxCal = 0;
    for(int x = 0; x < 3; x++)
    {
      maxCal += totalCalories.Max();
      int maxCalIndex = Array.IndexOf(totalCalories, maxCal);
      totalCalories = totalCalories.Where((e, i) => i != maxCalIndex).ToArray();
    }
    
    Console.WriteLine("Star 2: " + maxCal);
  }
}

class Program {
  public static void Main (string[] args) {
    
    string[] InputArray = File.ReadAllLines(@"Input.txt");

    Solution mySolution = new(InputArray);

    mySolution.Star1();
    mySolution.Star2();
  }
}
```
