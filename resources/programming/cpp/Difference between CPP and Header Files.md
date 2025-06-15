# Difference between CPP and Header Files

## Header Files (.h or .hpp)

**These are like blueprints or instruction manuals**

- They tell you WHAT exists, but not HOW it works
- Contains **declarations** - like a table of contents
- Shows function names, what they take as input, what they return
- Shows class/struct layouts
- Like saying "There's a function called `calculateTax` that takes a number and returns a number" - but doesn't show the actual math

Example:

```cpp
// math_helper.h
int add(int a, int b);        // "Hey, there's an add function somewhere!"
int multiply(int a, int b);   // "And a multiply function too!"
```

## CPP Files (.cpp)

**These are like the actual construction work**

- They contain the ACTUAL code that does the work
- Contains **definitions** - the real implementation
- Shows HOW functions actually work
- Like showing the actual math: "To calculate tax, multiply by 0.08"

Example:

```cpp
// math_helper.cpp
#include "math_helper.h"

int add(int a, int b) {
    return a + b;           // HERE's how adding actually works!
}

int multiply(int a, int b) {
    return a * b;           // HERE's how multiplying works!
}
```

## Why Split Them?

**Speed**: When you change HOW something works (CPP), you only recompile that file. If everything was in one file, you'd have to recompile EVERYTHING every time.

**Organization**: It's like having a book with a table of contents (header) and chapters (CPP files). Much easier to find stuff!

**Sharing**: You can give someone just the header file and say "Here's what my code can do" without showing them your secret sauce.

## Real World Analogy

- **Header file** = Restaurant menu (shows what's available)
- **CPP file** = Kitchen (where the actual cooking happens)

You look at the menu to see what you can order, but you don't need to see the kitchen to know the food exists!