If You're Using Replit
--

Copy this into your Replit ```main.cs``` (replacing all of what was in there originally) and make sure your input file is called ```Input.txt```
```c#
using System;
using System.IO;

class Solution
{
  string[] Input;
  
  
  public Solution(string[] input)
  {
    Input = input;
  }

  public void Star1()
  {
    string[] outcomes = new string[10] {"", "B X", "C Y", "A Z", "A X", "B Y", "C Z", "C X", "A Y", "B Z"};
    int score = 0;
    
    foreach(string line in Input)
    {
      score += Array.FindIndex(outcomes, element => element.StartsWith(line));
    }
    Console.WriteLine("Star 1: " + score);
  }

  public void Star2()
  {
    string[] outcomes = {"XBCA0", "YABC3", "ZCAB6"};
    int score = 0;
    
    foreach(string line in Input)
    {
      foreach(string outcome in outcomes)
      {
        if(line.Substring(2,1) == outcome[0].ToString())
          score += Convert.ToInt32(outcome[4].ToString()) + outcome.IndexOf(line.Substring(0,1));
      }
    }
    Console.WriteLine("Star 2: " + score);
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
