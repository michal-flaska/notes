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