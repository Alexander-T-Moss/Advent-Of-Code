If You're Using Replit
--

Copy this into your Replit ```main.cs``` (replacing all of what was in there originally) and make sure your input file is called ```Input.txt```
```
using System;
using System.Linq;

class Solution
{
  String Input;
  
  public Solution(string input)
  {
    Input = input;
  }
  
  public int Answer(int partNumber = 1)
  {
    int characterDistinctionCount;
    if(partNumber == 1)
      characterDistinctionCount = 4;
    else
      characterDistinctionCount = 14;

    for(int x = characterDistinctionCount; x < Input.Length; x++)
    {
      if(!Input.Substring(x-characterDistinctionCount, characterDistinctionCount).GroupBy(x => x).Any(g => g.Count() > 1))
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
    int Star1 = mySolution.Answer(1);
    timer.Stop();
    Console.WriteLine("Star 1: " + Star1 + $" // Found In {timer.ElapsedMilliseconds} ms");

    // Run code for solution two and time how long it takes
    timer.Reset();
    timer.Start();
    int Star2 = mySolution.Answer(2);
    timer.Stop();
    Console.WriteLine("Star 2: " + Star2 + $" // Found In {timer.ElapsedMilliseconds} ms");
  }
}
```
