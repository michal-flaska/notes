# C++ Starter Pack

## Table of Contents
1. [What is C++?](#what-is-c)
2. [Setting Up Environment](#setting-up-environment)
3. [First C++ Program](#first-c-program)
4. [Basic Concepts](#basic-concepts)
5. [Variables and Data Types](#variables-and-data-types)
6. [Input and Output](#input-and-output)
7. [Control Structures](#control-structures)
8. [Functions](#functions)
9. [Practice Exercises](#practice-exercises)
10. [Learning Resources](#learning-resources)
11. [Next Steps](#next-steps)

## What is C++?

C++ is a powerful programming language that's used to create:
- Desktop applications (like games, media players)
- Operating systems
- Web browsers
- Mobile apps
- System software

**Think of it this way:** If HTML is like the structure of a house and CSS is the decoration, C++ is like the tools and machinery used to build the entire house!

## Setting Up Environment

### Option 1: Online Compilers (Easiest to start)
- **Replit**: Go to replit.com, create account, choose C++
- **OnlineGDB**: onlinegdb.com/online_c++_compiler
- **Programiz**: programiz.com/cpp-programming/online-compiler

### Option 2: Local Setup
1. **Windows**: Download Visual Studio or Dev-C++
2. **Mac**: Install Xcode from App Store
3. **Linux**: Install g++ compiler: `sudo apt install g++`

## First C++ Program

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

**Let's break this down:**
- `#include <iostream>`: Like importing a library (similar to linking CSS to HTML)
- `using namespace std;`: Tells the program to use standard functions
- `int main()`: The main function - where program starts
- `cout`: Prints text to screen (like `console.log` in JavaScript)
- `return 0;`: Tells the program it finished successfully

## Basic Concepts

### 1. Comments
```cpp
// This is a single-line comment
/* This is a 
   multi-line comment */
```

### 2. Semicolons
Every statement in C++ ends with a semicolon `;` - it's like a period in English!

### 3. Case Sensitivity
C++ is case-sensitive: `Hello` and `hello` are different!

## Variables and Data Types

Think of variables as labeled boxes that store different types of information:

```cpp
#include <iostream>
using namespace std;

int main() {
    // Numbers
    int age = 25;              // Whole numbers
    double price = 19.99;      // Decimal numbers
    
    // Text
    char grade = 'A';          // Single character
    string name = "John";      // Text (words/sentences)
    
    // True/False
    bool isStudent = true;     // Boolean (true or false)
    
    // Display the variables
    cout << "Name: " << name << endl;
    cout << "Age: " << age << endl;
    cout << "Grade: " << grade << endl;
    cout << "Price: $" << price << endl;
    cout << "Is student: " << isStudent << endl;
    
    return 0;
}
```

## Input and Output

### Output (Displaying information)
```cpp
cout << "Hello World!";           // Print text
cout << "Hello" << " " << "World"; // Print multiple things
cout << "Number: " << 42 << endl; // Print text and number
```

### Input (Getting information from user)
```cpp
#include <iostream>
using namespace std;

int main() {
    string name;
    int age;
    
    cout << "What's your name? ";
    cin >> name;
    
    cout << "What's your age? ";
    cin >> age;
    
    cout << "Hello " << name << "! You are " << age << " years old." << endl;
    
    return 0;
}
```

## Control Structures

### If Statements (Making Decisions)
```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    cout << "Enter your age: ";
    cin >> age;
    
    if (age >= 18) {
        cout << "You are an adult!" << endl;
    } else if (age >= 13) {
        cout << "You are a teenager!" << endl;
    } else {
        cout << "You are a child!" << endl;
    }
    
    return 0;
}
```

### Loops (Repeating Actions)

**For Loop** (when you know how many times to repeat):
```cpp
// Print numbers 1 to 5
for (int i = 1; i <= 5; i++) {
    cout << i << " ";
}
// Output: 1 2 3 4 5
```

**While Loop** (repeat while condition is true):
```cpp
int count = 1;
while (count <= 3) {
    cout << "Count: " << count << endl;
    count++;
}
```

## Functions

Functions are like mini-programs that do specific tasks:

```cpp
#include <iostream>
using namespace std;

// Function to add two numbers
int addNumbers(int a, int b) {
    return a + b;
}

// Function to greet someone
void greetPerson(string name) {
    cout << "Hello, " << name << "!" << endl;
}

int main() {
    // Using the functions
    int result = addNumbers(5, 3);
    cout << "5 + 3 = " << result << endl;
    
    greetPerson("Alice");
    
    return 0;
}
```

## Practice Exercises

### Exercise 1: Personal Info
Create a program that asks for your name, age, and favorite color, then displays them nicely.

### Exercise 2: Simple Calculator
Create a program that asks for two numbers and shows their sum, difference, product, and quotient.

### Exercise 3: Grade Calculator
Create a program that asks for a test score and displays the letter grade:
- 90-100: A
- 80-89: B
- 70-79: C
- 60-69: D
- Below 60: F

### Exercise 4: Multiplication Table
Create a program that asks for a number and displays its multiplication table (1-10).

## Learning Resources

### Free Online Resources
- **Codecademy C++**: Interactive lessons
- **LearnCpp.com**: Comprehensive tutorials
- **CPlusPlus.com**: Reference and tutorials
- **YouTube**: Search "C++ for beginners"

### Books for Beginners
- "C++ Primer Plus" by Stephen Prata
- "Programming: Principles and Practice Using C++" by Bjarne Stroustrup

### Practice Platforms
- **HackerRank**: hackerrank.com
- **LeetCode**: leetcode.com (start with easy problems)
- **Codewars**: codewars.com