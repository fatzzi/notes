# Function Pointers

Function pointers are variables that store the addresses of functions. They are used to:
- Call functions indirectly
- Pass functions as arguments
- Implement callbacks

**Note:** They can only point to/store plain functions and stateless lambdas.

## Declaration

The pointer must be declared with a signature that matches the function it points to. Assigning a function pointer with a different signature can lead to undefined behavior.

### Syntax
```cpp
return_type (*pointer_name)(parameter_types);
```
### Simple Function Pointer Example
```cpp
int add(int a, int b) {
    return a + b;
}

// Declaration of a function pointer
int (*funcPtr)(int, int);
```
### Assigning a Function to a Pointer
In C++, the compiler implicitly converts the function name to a pointer to that function. The address-of operator (&) is optional:

```cpp
funcPtr = add;    // Implicit conversion
funcPtr = &add;   // Explicit (also valid)
```
The compiler understands that the address of function add is being assigned to funcPtr.

### Calling Through a Function Pointer
```cpp
int result = funcPtr(3, 4);  // Calls add(3, 4)
```
### Array of Function Pointers (Dynamic Function Calls)
You can create arrays of function pointers to call different functions based on runtime conditions.

```cpp
// Function declarations
int add(int a, int b) { return a + b; }
int subtract(int a, int b) { return a - b; }
int multiply(int a, int b) { return a * b; }

// Array of function pointers
int (*operations[3])(int, int) = {add, subtract, multiply};

// Using the array
for (int i = 0; i < 3; i++) {
    int result = operations[i](5, 3);
    std::cout << "Result: " << result << std::endl;
}
```

### Callbacks
A callback is a function passed as an argument to another function and called at a later time.

```cpp
#include <iostream>

// Function that takes a callback
void executeCallback(void (*callback)(int), int value) {
    callback(value);
}

// Callback function
void myCallback(int x) {
    std::cout << "Callback called with value: " << x << std::endl;
}

int main() {
    executeCallback(myCallback, 10);
    return 0;
}
```
### Pointer to Member Functions
```cpp
#include <iostream>

class MyClass {
public:
    void display() {
        std::cout << "Hello from MyClass!" << std::endl;
    }
};

int main() {
    MyClass obj;
    // Pointer to member function
    void (MyClass::*memberFuncPtr)() = &MyClass::display;

    // Calling the member function
    (obj.*memberFuncPtr)();  // Output: Hello from MyClass!

    return 0;
}
```

### Key Notes:
- Member function pointers require the `.*` or `->*` syntax for invocation  
- The class name must be specified in the pointer declaration (`MyClass::`)  
- The address-of operator (`&`) is mandatory when taking the address of a member function



