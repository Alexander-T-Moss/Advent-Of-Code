If You're Using Replit
--

Copy this into your Replit ```main.cs``` (replacing all of what was in there originally) and make sure your input file is called ```Input.txt```
```cs
using System;
using System.Collections.Generic;
using directories;

class FileSystem
{
  List<Directory> AllDirectories = new();
  Directory TopDirectory;
  
  public FileSystem(string[] input)
  {
    Directory currentDirectory = null;
    
    foreach(string command in input)
    {
      string[] commandParts = command.Split(' ');
      
      // $ cd Logic
      if(command.Contains("$ cd"))
      {
        if(currentDirectory != null)
          if(commandParts[2] != "..")
            currentDirectory = currentDirectory.OpenDirectory(commandParts[2]);
          else
            currentDirectory = currentDirectory.GetParentDirectory();
        else
        {
          currentDirectory = new(command.Split(' ')[2], null);
          AllDirectories.Add(currentDirectory);
          TopDirectory = currentDirectory;
        }
      }
      
      // File adding logic
      else if(commandParts[0] != "$")
        currentDirectory.AddItem(command);
    }

    // Put all directories in the file system into a list
    AllDirectories = TopDirectory.GetConnectedDirectories();    
  }

  public int Star1()
  {
    int answer = 0;
    foreach(Directory directory in AllDirectories)
    {
      int directorySize = directory.GetDirectorySize();
      if(directorySize <= 100000)
        answer += directorySize;
    }
    return answer;
  }

  public int Star2()
  {
    int spaceNeeded = TopDirectory.GetDirectorySize() - 40000000;

    Directory directoryToDelete = AllDirectories[0];

    foreach(Directory directory in AllDirectories)
    {
      if(directory.GetDirectorySize() >= spaceNeeded && directoryToDelete.GetDirectorySize() > directory.GetDirectorySize())
        directoryToDelete = directory;
    }
    return directoryToDelete.GetDirectorySize();
  }
}

class Program {
  public static void Main (string[] args) {
    
    string[] InputArray = System.IO.File.ReadAllLines(@"Input.txt");

    FileSystem myFileSystem = new(InputArray);

    Console.WriteLine("Star 1: " + myFileSystem.Star1());
    Console.WriteLine("Star 2: " + myFileSystem.Star2());
  }
}
```

And make a new file called ```directories.cs``` and put this code in their
```c#
using System;
using System.Collections.Generic;

namespace directories
{  
  class Directory
  {
    string Name;
    List<Directory> Directories;
    Directory ParentDirectory;
    List<string> Files;

    // Directory constructor
    public Directory(string name, Directory parentDirectory)
    {
      Name = name;
      Directories = new();
      Files = new();
      ParentDirectory = parentDirectory; 
    }

    // Return name of this directory
    public string GetName()
    {
      return Name;
    }
    
    // Return list of directories in this directory
    public List<Directory> GetDirectories()
    {
      return Directories;
    }

    // Return a directory in this directory
    public Directory OpenDirectory(string directoryName)
    {
      foreach(Directory directory in Directories)
      {
        if(directory.GetName() == directoryName)
          return directory;
      }
      return null;
    }

    // Return parent directory
    public Directory GetParentDirectory()
    {
      return ParentDirectory;
    }

    public List<Directory> GetConnectedDirectories()
    {
      List<Directory> directories = new();

      foreach(Directory directory in Directories)
      {
        if(directory.GetDirectories().Count == 0)
        {
          directories.Add(directory);
        }
        
        else
        {
          directories.Add(directory);
          directories.AddRange(directory.GetConnectedDirectories());
        }
      }
      return directories; 
    }

    // Add either a directory or file to this directory
    public void AddItem(string item)
    {
      if(item.Split(' ')[0] == "dir")
      {
        Directories.Add(new(item.Split(' ')[1], this));
      }
      
      else   
      {
        Files.Add(item);
      }
    }

    // Return size of this directory - including all sub-directories
    public int GetDirectorySize()
    {
      int directorySize = 0;
      foreach(string file in Files)
      {
        directorySize += Convert.ToInt32(file.Split(' ')[0]);
      }
      foreach(Directory directory in Directories)
      {
        directorySize += directory.GetDirectorySize();
      }
      return directorySize;
    }
  }
}
```
