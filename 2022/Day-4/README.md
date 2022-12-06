If You're Using Replit
--

Copy this into your Replit ```main.cs``` (replacing all of what was in there originally) and make sure your input file is called ```Input.txt```
```c#
using System;
using System.Collections.Generic;

class Solution
{
  List<string> Input = new();
  
  public Solution(string[] input)
  {
    foreach(string line in input)
    {
      Input.Add(line.Replace('-', ','));
    }
  }

  public int Star1()
  {
    int overlap = 0;
    foreach(string line in Input)
    {
      string[] tempArray = line.Split(',');
      int[] boundaries = Array.ConvertAll(tempArray, s => int.Parse(s));
      
      if(boundaries[0] >= boundaries[2] && boundaries[1] <= boundaries[3])
        overlap++;
      
      else if(boundaries[2] >= boundaries[0] && boundaries[3] <= boundaries[1])
        overlap++;
    }
    return overlap;
  }

  public int Star2()
  {
    int overlap = 0;
    foreach(string line in Input)
    {
      string[] tempArray = line.Split(',');
      int[] boundaries = Array.ConvertAll(tempArray, s => int.Parse(s));
      
      if(boundaries[0] >= boundaries[2] && boundaries[0] <= boundaries[3])
        overlap++;
      
      else if(boundaries[1] >= boundaries[2] && boundaries[1] <= boundaries[3])
        overlap++;

      else if(boundaries[2] >= boundaries[0] && boundaries[2] <= boundaries[1])
        overlap++;

      else if(boundaries[3] >= boundaries[0] && boundaries[3] <= boundaries[1])
        overlap++;
    }
    return overlap;
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
