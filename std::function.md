# `std::function`

`std::function` provides a type-safe (ensures the callable object matches the expected signature) way to store and invoke all callable objects like functions, function pointers, lambda expressions, and functors. It is defined in the `<functional>` header.

Think of it as a box that can hold anything that behaves like a function and lets you call it later.

## Syntax

```cpp
#include <functional>

std::function<return_type(parameter_types)> functionName;
std::function<int(int, int)> op;  // A callable that takes two ints and returns an int
```
## lambda
``` cpp
std::function<void()> sayHello = []() {
    std::cout << "Hello!" << std::endl;
};
sayHello();  // Call the lambda
```

## Storing Function Pointer

```cpp
int add(int a, int b) { return a + b; }

std::function<int(int, int)> op = add;
std::cout << op(3, 4);  // Output: 7
```

This is actually in terms of output equivalent to:

``` cpp
int (*funcPtr)(int, int);
funcPtr = add; // or funcPtr = &add; (the & is optional)
```

But under the hood they are very different. std::function can store all callable objects while a normal raw function cannot. For example, we have a lambda:

```cpp
int x = 5;
auto lambda = [x](int a) {
    return a + x;
};
```

Since it captures x, you cannot store this in a function pointer. In std::function<int(int)>, however, can store it.

## Storing a Functor
``` cpp
#include <iostream>
#include <functional>

class Multiplier {
public:
    Multiplier(int factor) : factor(factor) {}

    int operator()(int x) const {
        return x * factor; // Multiply by the factor
    }

private:
    int factor;
};

int main() {
    // Store a functor in std::function
    std::function<int(int)> multiplyByTwo = Multiplier(2);

    // Call the functor
    std::cout << "Result: " << multiplyByTwo(5) << std::endl; // Output: Result: 10

    return 0;
}
```

## With STL algorithms
``` cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <functional>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};

    // Define a std::function to use with std::for_each
    std::function<void(int)> print = [](int x) {
        std::cout << x << " "; // Print each number
    };

    // Use std::for_each with std::function
    std::for_each(numbers.begin(), numbers.end(), print);
    std::cout << std::endl; // Output: 1 2 3 4 5

    return 0;
}
```


