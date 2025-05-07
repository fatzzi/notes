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

```
    // Capture x by value
    auto lambda = [x]() {
        std::cout << "Captured by value: " << x << std::endl;
    };
    
```
## Key Points:

- Creates independent copy
- Original can go out of scope safely
- Cannot modify captured value unless mutable is used

## 2. Capture by Reference
Allows access and modification of the original variable.

```cpp
    
    // Capture x by reference
    auto lambda = [&x]() {
        x += 5;
        std::cout << "Captured by reference: " << x << std::endl;
    };


```
**Warning:**
Undefined behavior if original variable goes out of scope before lambda executes.

## 3. Capture All by Value ([=])
Captures all accessible variables by value.

```cpp

    auto lambda = [=]() {
        std::cout << "a = " << a << ", b = " << b << std::endl;
    };
    
```
## 4. Capture All by Reference ([&])
Captures all accessible variables by reference.
```cpp
    auto lambda = [&]() {
        a += 5;
        b += 10;
        std::cout << "a = " << a << ", b = " << b << std::endl;
    };
    

```
# Calling Lambdas
## Immediate Invocation (IIFE)
Execute immediately after definition:

```cpp
int main() {
    []() {
        std::cout << "Hello, World!" << std::endl;
    }();  // Immediately invoked
}
```
## With Parameters
Pass arguments directly to IIFE:
```cpp
[](int a, int b) {
    std::cout << "Sum: " << a + b << std::endl;
}(3, 4);  // Output: Sum: 7

```

## With STL algorithms
```cpp
std::sort(vec.begin(), vec.end(), [](int a, int b){ return a < b; });
```

## Summary

Lambda expressions in C++ are anonymous, inline functions that allow you to define function-like behavior directly within your code, making it concise and expressive, especially for short operations like sorting or filtering. Their syntax includes a capture clause [ ] for accessing variables from the surrounding scope (by value or reference), parameter list (), optional return type ->, and a function body {}. They can capture variables explicitly (e.g., [x], [&x]) or implicitly (e.g., [=], [&]), and can even capture the this pointer in member functions. Lambdas are useful in algorithms, callbacks, and when passing behavior as parameters. They support immediate invocation and can modify captured values using the mutable keyword. Return types are usually deduced automatically but can be specified explicitly when needed.

For more examples of how they are used check out [examples](https://github.com/fatzzi/notes/blob/main/lambda_expression_examples.md)!





