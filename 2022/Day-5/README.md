If You're Using Replit
--

Copy this into your Replit ```main.cs``` (replacing all of what was in there originally) and make sure your input file is called ```Input.txt``` and your stacks part of the input is in ```Crates.txt```
```
using System;
using System.Collections.Generic;
using System.IO;

class Stack
{
  List<string> Crates;

  public Stack()
  {
    Crates = new();
  }

  public string GetCrate()
  {
    string topCrate = Crates[^1];
    Crates.RemoveAt(Crates.Count - 1);
    return topCrate;
  }

  public string[] GetCrates(int numberOfCrates)
  {
    List<string> crates = new();

    for(int x = 0; x < numberOfCrates; x++)
    {
      crates.Add(GetCrate());
    }

    string[] ReversedCrates = crates.ToArray();
    Array.Reverse(ReversedCrates);
    
    return ReversedCrates;
  }

  public void AddCrate(string crate)
  {
    Crates.Add(crate);
  }

  public void AddCrates(string[] crates)
  {
    foreach(string line in crates)
    {
      AddCrate(line);
    }
  }
}

class Solution
{
  Stack[] Stacks;
  string[] Input;
  
  public Solution(string[] input, string[] crates)
  {
    Input = input;
    AddCrates(crates);
  }

  public void AddCrates(string[] crates)
  {
    // Initialize Stacks
    Stacks = new Stack[crates[^1].Replace(" ", String.Empty).Length];

    for(int x = 0; x < Stacks.Length; x++)
    {
      Stacks[x] = new();
    }

    // Add crates to their respective stack
    for(int x = crates.Length - 2; x >= 0; x--)
    {
      for(int i = 0; i < Stacks.Length; i++)
      {
        int stackIndex = (i * 4) + 1;

        if(crates[x][stackIndex] != ' ')
          Stacks[i].AddCrate(Convert.ToString(crates[x][stackIndex]));
      }
    }
  }
  public string Star1()
  {
    foreach(string line in Input)
    {
      string[] lineInfo = line.Split(' ');
      for(int x = 0; x < Convert.ToInt32(lineInfo[1]); x++)
      {
        Stacks[Convert.ToInt32(lineInfo[5]) - 1].AddCrate(Stacks[Convert.ToInt32(lineInfo[3]) - 1].GetCrate());
      }
    }
    
    string topCrates = "";
    foreach(Stack stack in Stacks)
    {
      topCrates += stack.GetCrate();
    }
    return topCrates;
  }

  public string Star2()
  {
    foreach(string line in Input)
    {
      string[] lineInfo = line.Split(' ');
      
        Stacks[Convert.ToInt32(lineInfo[5]) - 1].AddCrates(Stacks[Convert.ToInt32(lineInfo[3]) - 1].GetCrates(Convert.ToInt32(lineInfo[1])));
    }
    
    string topCrates = "";
    foreach(Stack stack in Stacks)
    {
      topCrates += stack.GetCrate();
    }
    return topCrates;
  }
}

class Program {
  public static void Main (string[] args) {
    
    string[] InputArray = File.ReadAllLines(@"Input.txt");
    string[] Crates = File.ReadAllLines(@"Crates.txt");

    Solution mySolution1 = new(InputArray, Crates);
    Console.WriteLine(mySolution1.Star1());

    Solution mySolution2 = new(InputArray, Crates);
    Console.WriteLine(mySolution2.Star2());
  }
}
```
