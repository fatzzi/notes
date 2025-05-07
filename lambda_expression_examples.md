Example codes for lamda expressions

## 1. Capture by Value
```cpp
int x = 10;
auto lambda = [x]() {
    std::cout << "Captured by value: " << x << std::endl;
};
lambda();  // Output: 10
```
# Key Points:

- Creates independent copy
- Original can go out of scope safely
- Cannot modify captured value unless mutable is used


## 2. Capture by Reference
```cpp
int x = 10;
auto lambda = [&x]() {
    x += 5;
    std::cout << "Captured by reference: " << x << std::endl;
};
lambda();  // Output: 15
```
**Warning:**
Undefined behavior if original variable goes out of scope before lambda executes.

## 3. Capture All by Value [=]
```cpp
int a = 5, b = 10;
auto lambda = [=]() {
    std::cout << "a = " << a << ", b = " << b << std::endl;
};
lambda();  // Output: a = 5, b = 10
```
## 4. Capture All by Reference [&]
```cpp
int a = 5, b = 10;
auto lambda = [&]() {
    a += 5;
    b += 10;
    std::cout << "a = " << a << ", b = " << b << std::endl;
};
lambda();  // Output: a = 10, b = 20
```
## 5. Mixed Capture
```cpp
int a = 5, b = 10;
auto lambda = [a, &b]() {
    std::cout << "a = " << a << ", b = " << b << std::endl;
    b += 5;
};
lambda();  // Output: a = 5, b = 10
```
## 6. Capturing this in Classes

Access class members from within member functions.
```cpp
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
```
## 7. Mutable Lambda

Allows modification of value-captured variables.

```
int x = 10;
auto lambda = [x]() mutable {
    x += 5;
    std::cout << "Inside: " << x << std::endl;
};
lambda();  // Output: Inside: 15
std::cout << "Outside: " << x << std::endl;  // Output: Outside: 10
```
**Note:** mutable only affects the lambda's copy, not the original variable.

## 8. Return Type Deduction with auto
```
auto lambda = [](int a, int b) {
    return a + b;
};
std::cout << lambda(5, 3);  // Output: 8
```
## 9. Explicit Return Type
```
auto lambda = [](int a, int b) -> double {
    return static_cast<double>(a) / b;
};
std::cout << lambda(5, 2);  // Output: 2.5
```
## 10. Multiple Return Types – Compilation Error
```
auto lambda = [](bool condition) {
    if (condition)
        return 42;      // int
    else
        return 3.14;    // double
};
// Compilation Error: inconsistent return types
```
If a lambda has multiple return statements with different types, the compiler will attempt to deduce a common return type. If it cannot, it will result in a compilation error.

## 12. Immediate Invocation (IIFE)
```
[]() {
    std::cout << "Hello, World!" << std::endl;
}();  // Immediately invoked
```
## 13. IIFE with Parameters
```
[](int a, int b) {
    std::cout << "Sum: " << a + b << std::endl;
}(3, 4);  // Output: Sum: 7
```
