# BinaryEvaluator
A basic C# program to evaluate two given binary inputs (IE `01`, `11`, etc.) for a chosen operation among the following: `AND`, `OR`, `XOR`.
Code can be executed at [https://BinaryEvaluator.griffingoing.repl.run](https://BinaryEvaluator.griffingoing.repl.run)

## Example output given valid inputs

![example output with valid inputs](https://github.com/GriffinGoing/BinaryEvaluator/blob/master/withValidInput.png)

# Example output given invalid inputs


## Code (found in `main.cs`, included here for single-file presentation
```
using System;
using System.Text.RegularExpressions;

class MainClass {

  //method to evaluate the chosen operation and inputs
  private static bool evaluate(string binaryOperation, string binaryInput) {
    switch(binaryOperation) {
      case "AND":
        return (binaryInput == "11");

      case "OR":
        return !(binaryInput == "00");

      case "XOR":
        return (binaryInput == "10" || binaryInput == "01");
    }

    //return false if things don't pan out
    return false;
  }

  //method to validate chosen operations for validity
  private static bool isValidBinaryOperation(string binaryOperation) {
    //regex to match only valid dual binary inputs
     Regex validInputs = new Regex("^(AND|OR|XOR|0)$");

    if (validInputs.IsMatch(binaryOperation)) {
      return true;
    }

    else {
      return false;
    }
  }

  //method to validate binaries for validity
  private static bool isValidBinaryInput(string binaryInput) {
    //regex to match only valid dual binary inputs
     Regex validInputs = new Regex("^[01]{2}$");

    if (validInputs.IsMatch(binaryInput)) {
      return true;
    }

    else {
      return false;
    }
  }

  public static void Main (string[] args) {
    // strings for user input to evaluate
    string binaryOperation;
    string binaryInput;

    //program interface header
    Console.WriteLine("***************************************");
    Console.WriteLine("*** B I N A R Y   E V A L U A T O R ***");
    Console.WriteLine("***************************************");

    do {
      //get binary operation from user
      do {
        Console.WriteLine("Enter the binary operation you wish to evaluate for (AND, OR, XOR), or '0' to exit: ");
        binaryOperation = Console.ReadLine().ToUpper();

        if (!isValidBinaryOperation(binaryOperation)) {
          Console.WriteLine($"*** '{binaryOperation}' is not valid input. Re-attempting... ***");
        }

      } while (!isValidBinaryOperation(binaryOperation));

      //get binaries from user if exit command was not given 
      if (binaryOperation != "0") {
        do {
        Console.WriteLine("Enter 2 binaries (0 or 1) with no separation: ");
        binaryInput = Console.ReadLine();

        if (!isValidBinaryInput(binaryInput)) {
          Console.WriteLine($"*** '{binaryInput}' is not valid input. Re-attempting... ***");
        }
        } while(!isValidBinaryInput(binaryInput));

        Console.WriteLine($"'{binaryOperation}' operation with input '{binaryInput}' evaluates to {evaluate(binaryOperation, binaryInput)}");
        Console.WriteLine("-------------------------------------------------");
      }     
    } while (binaryOperation != "0");
    
    Console.WriteLine("***************************************");
    Console.WriteLine("************ E X I T I N G ************");
    Console.WriteLine("***************************************");
  }
}
```
