If You're Using Replit
--

Copy this into your Replit ```main.cs``` (replacing all of what was in there originally) and make sure your input file is called ```Input.txt```
```c#
using System;
using System.Linq;

class Solution
{
  String Input;
  
  public Solution(string input)
  {
    Input = input;
  }
  
  public int Answer(int markerSize)
  {
    // Iteration for all possible markers
    for(int x = markerSize; x < Input.Length; x++)
    {
      // Get marker
      string marker = Input.Substring(x-markerSize, markerSize);

      // Check if marker has no repeats
      if(marker.Distinct().Count() == markerSize)
        return x;
    }
    return -1;
  }
}

class Program {
  public static void Main (string[] args) {
    
    string Input = System.IO.File.ReadAllText(@"Input.txt");
    var timer = new System.Diagnostics.Stopwatch();

    Solution mySolution = new(Input);

     // Run code for solution one and time how long it takes
    timer.Start();
    int Star1 = mySolution.Answer(4);
    timer.Stop();
    Console.WriteLine("Star 1: " + Star1 + $" // Found In {timer.ElapsedMilliseconds} ms");

    // Run code for solution two and time how long it takes
    timer.Reset();
    timer.Start();
    int Star2 = mySolution.Answer(14);
    timer.Stop();
    Console.WriteLine("Star 2: " + Star2 + $" // Found In {timer.ElapsedMilliseconds} ms");
  }
}
```
