If You're Using Replit
--

Copy this into your Replit ```main.cs``` (replacing all of what was in there originally) and make sure your input file is called ```Input.txt```
```
using System;

class Solution
{
  string[] Input;
  
  public Solution(string[] input)
  {
    Input = input;
  }

   // Simple function to convert item to priority number
  public int GetPriority(char item)
  {
    if(Char.IsUpper(item))
      return Convert.ToInt32(item) - 38;
    else
      return Convert.ToInt32(item) - 96;
  }

   // Solution for part 1
  public int Star1()
  {
    int priority = 0;
    
    foreach(string line in Input)
    {
      string secondHalf = line.Substring(line.Length/2, line.Length/2);
      foreach(char item in line.Substring(0, line.Length / 2))
      {
        if(secondHalf.Contains(item))
        {
          secondHalf = secondHalf.Replace(item, ' ');
          priority += GetPriority(item);
        }
      }
    }
    return priority;
  }
  
   // Solution for part 2
  public int Star2()
  {
    int priority = 0;
    
    for(int groupNumber = 2; groupNumber < Input.Length; groupNumber += 3)
    {
      string leadGroupBag = Input[groupNumber];
      foreach(char item in Input[groupNumber - 2])
      {
        if(Input[groupNumber-1].Contains(item) && leadGroupBag.Contains(item))
        {
          leadGroupBag = leadGroupBag.Replace(item, ' ');
          priority += GetPriority(item);
        }
      }
    }
    return priority;
  }
}

class Program {
  public static void Main (string[] args) {
    
    string[] InputArray = System.IO.File.ReadAllLines(@"Input.txt");
    var timer = new System.Diagnostics.Stopwatch();

    Solution mySolution = new(InputArray);

     // Run code for solution one and time how long it takes
    timer.Start();
    int Star1 = mySolution.Star1();
    timer.Stop();
    Console.WriteLine("Star 1: " + Star1 + $" // Found In {timer.ElapsedMilliseconds} ms");

    // Run code for solution two and time how long it takes
    timer.Reset();
    timer.Start();
    int Star2 = mySolution.Star2();
    timer.Stop();
    Console.WriteLine("Star 2: " + Star2 + $" // Found In {timer.ElapsedMilliseconds} ms");
  }
}
```
