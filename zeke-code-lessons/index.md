# Lesson One 'Hello World'

[Online Link](https://docs.microsoft.com/en-us/dotnet/core/tutorials/with-visual-studio-code)

This will be a simple lesson to create an application that 'prints' \(output, but we'll review what print means\) 'Hello World' in c\#

We will do the following

1. Download the .net core SDK
   * SDK stand for Software Development Kit
   * [Download Link](https://dotnet.microsoft.com/download)
2. Download Visual Studio Code
   * This will be the 'IDE' we will use to actually code
   * IDE stands for Interactive Development Environment
3. Create a simple application that will print 'Hello World'

## Downlaod .Net Core SDK

### What is .Net? \(Needs work\)

[.Net](https://en.wikipedia.org/wiki/.NET_Framework) is a microsoft 'framework' that Microsoft created that allows software to run

* The idea is that if you want to create something in the Microsoft ecosystem, you can create it in .net and it will work on any supported system

.Net Core is the version of .Net that is 'Open Source'

* Open Source simply means you don't have to pay to use it
* Publicly available

To create something in .Net originally, you had to 'pay to play'

* Microsoft got smart and created .Net Core that is 'Open Source'

### .Net Core

.Net core is almost identical to regular .Net

* Eventually Microsoft will only support Core
* [Download Link](https://dotnet.microsoft.com/download)
  * We will be downloading the most recent version of the SDK
    * Don't worry about the version that is compatible with 'Visual Studio'
* Confirm the Download Worked \(and intro to command lines!\)
  * Open the Windows command line
    * Hit the window button, and type 'cmd'
  * Once it's open, type 'dotnet'

    ![](../.gitbook/assets/dotnetinstallcmd.png)

### VS Code

VS Code is primarily a file editor, but it's fast becoming the 'go-to' editor for applictions written in: .net core, java

It also can read and edit almost any file, along with a huge list of extensions

1. [Download](https://code.visualstudio.com/)
2. Install the c\# extension
   * Go the 'Extensions' tab \(Left Nav panel, square\)
   * Type c\# into search

### Hello World

1. Have them open a folder in VS Code
   * Name it 'helloWorld'
2. Open Terminal: View -&gt; Terminal
   * Or: Right click folder -&gt; Open in Terminal
3. Type

   ```text
    dotnet new console
   ```

4. Should have a new c\# project created with some new files
   * May need to resolve build assets

     ```text
     dotnet restore
     ```
5. Run the program
   * Either type:

     ```text
     dotnet run
     ```

   * Or press F5

### Debugging

Debugging is when we put 'breaks' in our code so that we can see what's happening at a specific point

Debugging is one of the most powerful and usefull pieces of a programming framework

1. Go to 'Program.cs'
2. Find the line that says "Hello World"
3. You'll see line numbers. Click to the left of the number
   * A red dot should appear
4. Press 'F5'
   * The code will stop where you put the red dot

This is called 'setting a breakpoint'

* Literally putting a place in code where running stops
* F10 is 'Step Over'
  * Goes to the next line
* F11 is 'Step Into'
  * We'll get into that later

There are also controls at the top of the app:

![](https://github.com/eventhorizn/wiki/tree/f1299670bd333a04f198f24dc55f1882d579d4c4/zekeCodeLessons/lessonOne/images/debugControls.png)

### Adding a Class

A Class is a file with a .cs file type \(ie Program.cs\)

Usually we create a class to represent a single thing

* A 'shape' class, or a 'Person' class
* In the 'helloWorld' folder right click and 'New File'
  * Name the file 'MyClass.cs'
* Add the below code

  ```csharp
   using System;

   namespace helloWorld
   {
       public class MyClass
       {
           public string ReturnMessage()
           {
               return "Happy coding!";
           }
       }
   }
  ```

* The section 'ReturnMessage' is called a 'function'
* In the 'Program.cs' class file replace the code in the 'Main' function with:

  ```csharp
       MyClass c1 = new MyClass();
       Console.WriteLine($"Hello World! {c1.ReturnMessage()}");
  ```

So, we created a new class, 'instantiated' it in our Main class and refrenced a 'function' within that class

