If You're Using Replit
--

Copy this into your Replit ```main.cs``` (replacing all of what was in there originally) and make sure your input file is called ```Input.txt```
```
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
    string[] outcomes = {"B X", "C Y", "A Z", "A X", "B Y", "C Z", "C X", "A Y", "B Z"};
    int score = 0;
    foreach(string line in Input)
    {
      score += Array.FindIndex(outcomes, s => s.StartsWith(line)) + 1;
    }
    Console.WriteLine("Star 1: " + score);
  }

  public void Star2()
  {
    int score = 0;
    foreach(string line in Input)
    {
      if(line != "")
      {
        if(line.Substring(2, 1) == "X")
        {
          score += 0;
          if(line.Substring(0,1) == "A")
            score += 3;
          else if(line.Substring(0,1) == "B")
            score += 1;
          else
            score += 2;
        }
        else if(line.Substring(2, 1) == "Y")
        {
          score += 3;
          if(line.Substring(0,1) == "A")
            score += 1;
          else if(line.Substring(0,1) == "B")
            score += 2;
          else
            score += 3;
        }
        else
        {
          score += 6;
          if(line.Substring(0,1) == "A")
            score += 2;
          else if(line.Substring(0,1) == "B")
            score += 3;
          else
            score += 1;
        }
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
