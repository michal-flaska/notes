# Pointers in C++

## Creating pointers:

```cpp
#include <iostream>

int main(){

    std::string food = "Pizza";  // A food variable of type string
    std::string* ptr = &food;    // A pointer variable, with the name ptr, that stores the address of food

    // Output the value of food (Pizza)
    std::cout << food << "\n";

    // Output the memory address of food (0x6dfed4)
    std::cout << &food << "\n";

    // Output the memory address of food with the pointer (0x6dfed4)
    std::cout << ptr << "\n";

    return 0;
}
```

## Dereferencing pointers:

```cpp
#include <iostream>

int main(){

    std::string food = "Pizza";  // Variable declaration
    std::string* ptr = &food;    // Pointer declaration

    // Reference: Output the memory address of food with the pointer (0x6dfed4)
    std::cout << ptr << "\n";

    // Dereference: Output the value of food with the pointer (Pizza)
    std::cout << *ptr << "\n";

    return 0;
}
```

## Modifying pointers:
```cpp

#include <iostream>

int main(){

    std::string food = "Pizza";
    std::string* ptr = &food;

    // Output the value of food (Pizza)
    std::cout << food << "\n";

    // Output the memory address of food (0x6dfed4)
    std::cout << &food << "\n";

    // Access the memory address of food and output its value (Pizza)
    std::cout << *ptr << "\n";

    // Change the value of the pointer
    *ptr = "Hamburger";

    // Output the new value of the pointer (Hamburger)
    std::cout << *ptr << "\n";

    // Output the new value of the food variable (Hamburger)
    std::cout << food << "\n";

    return 0;
}
```