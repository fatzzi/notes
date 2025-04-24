# Lambda Expressions

A lambda function (or lambda expression) in C++ is a type of anonymous function that can be defined inline, allowing for the creation of function objects (functors) without the need for a separate function declaration. Lambda functions can capture variables from their surrounding scope and can be used wherever function pointers or function objects are expected.

## Syntax

```cpp
[capture](parameters) -> return_type {
    // function body
}
```

## Lambda Components

### Capture
Specifies which variables from the surrounding scope are accessible inside the lambda:
- Capture by value (`[x]`): Creates a copy of the variable
- Capture by reference (`[&x]`): References the original variable

### Parameters
Defines the input arguments, similar to regular function parameters:
- Can explicitly specify types (`int x, float y`)
- Can use `auto` for generic lambdas
- Optional when no parameters are needed

### Return Type
Determines what the lambda returns:
- Optional specification (`-> type`)
- Automatically deduced if omitted
- Must be specified explicitly for complex return cases

### Function Body
Contains the executable code:
- Enclosed in curly braces `{}`
- Can contain any valid C++ statements
- May include multiple return statements (with consistent types)

# Lambda Captures in C++

## 1. Capture by Value
Creates a copy of the variable. Modifications inside the lambda don't affect the original.

```cpp
#include <iostream>

int main() {
    int x = 10;
    
    // Capture x by value
    auto lambda = [x]() {
        std::cout << "Captured by value: " << x << std::endl;
    };
    
    lambda();  // Output: Captured by value: 10
    
    x = 20;    // Change original
    lambda();  // Output: Captured by value: 10 (unchanged)
    
    return 0;
}
```
## Key Points:

- Creates independent copy
- Original can go out of scope safely
- Cannot modify captured value unless mutable is used

## 2. Capture by Reference
Allows access and modification of the original variable.

```cpp
#include <iostream>

int main() {
    int x = 10;
    
    // Capture x by reference
    auto lambda = [&x]() {
        x += 5;
        std::cout << "Captured by reference: " << x << std::endl;
    };
    
    lambda();  // Output: Captured by reference: 15
    std::cout << "Original x: " << x << std::endl;  // Output: Original x: 15
    
    return 0;
}
```
**Warning:**
Undefined behavior if original variable goes out of scope before lambda executes.

## 3. Capture All by Value ([=])
Captures all accessible variables by value.

```cpp
#include <iostream>

int main() {
    int a = 5, b = 10;
    
    auto lambda = [=]() {
        std::cout << "a = " << a << ", b = " << b << std::endl;
    };
    
    lambda();  // Output: a = 5, b = 10
    a = 20;
    lambda();  // Output: a = 5, b = 10 (unchanged)
    
    return 0;
}
```
## 4. Capture All by Reference ([&])
Captures all accessible variables by reference.
```cpp
#include <iostream>

int main() {
    int a = 5, b = 10;
    
    auto lambda = [&]() {
        a += 5;
        b += 10;
        std::cout << "a = " << a << ", b = " << b << std::endl;
    };
    
    lambda();  // Output: a = 10, b = 20
    std::cout << "After lambda: a = " << a << ", b = " << b << std::endl;
    
    return 0;
}
```
## 5. Mixed Capture
Combine specific value and reference captures.
```cpp
#include <iostream>

int main() {
    int a = 5, b = 10;
    
    auto lambda = [a, &b]() {
        std::cout << "a = " << a << ", b = " << b << std::endl;
        b += 5;  // Only b can be modified
    };
    
    lambda();  // Output: a = 5, b = 10
    std::cout << "After lambda: a = " << a << ", b = " << b << std::endl;
    
    return 0;
}
```
## 6. Capturing this Pointer
Access class members from within member functions.
```cpp
#include <iostream>

class MyClass {
public:
    int value = 10;
    
    void show() {
        auto lambda = [this]() {
            std::cout << "Value: " << value << std::endl;
        };
        lambda();
    }
};

int main() {
    MyClass obj;
    obj.show();  // Output: Value: 10
    return 0;
}
```

## Mutable Lambdas
Allows modification of value-captured variables.

```cpp
#include <iostream>

int main() {
    int x = 10;
    
    auto lambda = [x]() mutable {
        x += 5;
        std::cout << "Inside: " << x << std::endl;
    };
    
    lambda();  // Output: Inside: 15
    std::cout << "Outside: " << x << std::endl;  // Output: Outside: 10
    
    return 0;
}
```
**Note:** mutable only affects the lambda's copy, not the original variable.
## Return Type

### **Auto Deduction**
When you define a lambda **without specifying a return type**, the compiler automatically deduces the return type based on the return statements:

```cpp
#include <iostream>

int main() {
    auto lambda = [](int a, int b) {
        return a + b;  // Return type deduced as int
    };

    std::cout << "Result: " << lambda(5, 3) << std::endl;  // Output: Result: 8
    return 0;
}
```

### Explicit Return Type
Specify the return type using -> syntax when:

- The return type can't be easily deduced
- You want to enforce a specific type

```cpp
#include <iostream>

int main() {
    auto lambda = [](int a, int b) -> double {
        return static_cast<double>(a) / b;  // Forces double return
    };

    std::cout << "Result: " << lambda(5, 2) << std::endl;  // Output: Result: 2.5
    return 0;
}
```

### **Error:** Multiple Return Types
If a lambda has multiple return statements with different types, the compiler will attempt to deduce a common return type. If it cannot, it will result in a compilation error.
```cpp
#include <iostream>

int main() {
    auto lambda = [](bool condition) {
        if (condition) {
            return 42;    // int
        } else {
            return 3.14;  // double
        }
    };
    
    // Causes compilation error:
    // std::cout << lambda(true) << std::endl;
    return 0;
}
```
# Calling Lambdas
## Immediate Invocation (IIFE)
Execute immediately after definition:

```cpp
#include <iostream>

int main() {
    []() {
        std::cout << "Hello, World!" << std::endl;
    }();  // Immediately invoked
    
    return 0;
}
```
## With Parameters
Pass arguments directly to IIFE:
```cpp
[](int a, int b) {
    std::cout << "Sum: " << a + b << std::endl;
}(3, 4);  // Output: Sum: 7

```






